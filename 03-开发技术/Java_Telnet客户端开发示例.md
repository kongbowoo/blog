# Java Telnet 客户端开发示例

> 概述：记录使用 Apache Commons Net 的 `TelnetClient` 在 Java 中连接 Telnet 服务器、发送命令并读取输出的完整示例，并附 SSH 方式的实现思路。

## 1. 使用 Apache TelnetClient 发送命令并读取数据

依赖：`commons-net`（Apache Commons Net）。

```java
package cn.keyidea.telnet;

import java.io.InputStream;
import java.io.PrintStream;

import org.apache.commons.net.telnet.TelnetClient;

public class TelnetUtil {
    // telnet 有 VT100 VT52 VT220 VTNT ANSI 等终端协议
    private TelnetClient telnet = new TelnetClient("VT220");
    private InputStream in;
    private PrintStream out;
    private static final String DEFAULT_AIX_PROMPT = "C:\\Users\\Administrator>";
    // telnet 端口
    private String port;
    // 用户名
    private String user;
    // 密码
    private String password;
    // IP 地址
    private String ip;
    // 缺省端口
    private static final int DEFAULT_TELNET_PORT = 23;

    public TelnetUtil(String ip, String user, String password) {
        this.ip = ip;
        this.port = String.valueOf(TelnetUtil.DEFAULT_TELNET_PORT);
        this.user = user;
        this.password = password;
    }

    public TelnetUtil(String ip, String port, String user, String password) {
        this.ip = ip;
        this.port = port;
        this.user = user;
        this.password = password;
    }

    /**
     * @return boolean 连接成功返回 true，否则返回 false
     */
    private boolean connect() {
        boolean isConnect = true;
        try {
            telnet.connect(ip, Integer.parseInt(port));
            in = telnet.getInputStream();
            out = new PrintStream(telnet.getOutputStream());
            /** Log the user on */
            readUntil("login: ");
            write(user);
            readUntil("password: ");
            write(password);
            /** Advance to a prompt */
            readUntil(DEFAULT_AIX_PROMPT);
        } catch (Exception e) {
            isConnect = false;
            e.printStackTrace();
            return isConnect;
        }
        return isConnect;
    }

    public void su(String user, String password) {
        try {
            write("su" + " - " + user);
            readUntil("Password:");
            write(password);
            readUntil(DEFAULT_AIX_PROMPT);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    public String readUntil(String pattern) {
        try {
            char lastChar = pattern.charAt(pattern.length() - 1);
            StringBuffer sb = new StringBuffer();
            char ch = (char) in.read();
            while (true) {
                sb.append(ch);
                if (ch == lastChar) {
                    if (sb.toString().endsWith(pattern)) {
                        // 处理编码，避免界面显示乱码
                        byte[] temp = sb.toString().getBytes("iso8859-1");
                        return new String(temp, "GBK");
                    }
                }
                ch = (char) in.read();
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
        return null;
    }

    public void write(String value) {
        try {
            out.println(value);
            out.flush();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    public String sendCommand(String command) {
        try {
            write(command);
            return readUntil(DEFAULT_AIX_PROMPT);
        } catch (Exception e) {
            e.printStackTrace();
        }
        return null;
    }

    private void disconnect() {
        try {
            telnet.disconnect();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    private String getIPConfig() {
        this.connect();
        String result = this.sendCommand("ipconfig");
        this.disconnect();
        // 去除命令提示符
        return result.substring(0, result.indexOf(DEFAULT_AIX_PROMPT));
    }

    private String getDir() {
        this.connect();
        String result = this.sendCommand("dir");
        this.disconnect();
        // 去除命令提示符
        return result.substring(0, result.indexOf(DEFAULT_AIX_PROMPT));
    }

    public static void main(String[] args) {
        TelnetUtil telnet = new TelnetUtil("127.0.0.1", "administrator", "1");
        System.out.println(telnet.getDir());
        System.out.println(telnet.getIPConfig());
    }
}
```

### 关键点说明

- **终端类型**：`new TelnetClient("VT220")` 指定终端仿真协议，可根据目标设备选择 VT100、VT52、VT220、VTNT、ANSI 等。
- **提示符匹配**：`readUntil` 通过匹配命令提示符（`DEFAULT_AIX_PROMPT`）判断命令执行结束，实际使用时需按目标系统的提示符调整。
- **编码处理**：示例中对输出做了 `iso8859-1 -> GBK` 的转码，用于解决中文乱码；目标系统编码不同时需相应调整。

### 来源

> 作者：dc15822445347 来源：CSDN
> 原文：<https://blog.csdn.net/dc15822445347/article/details/27123659>
> 转载请附上原文链接。

## 2. SSH 登录的实现方法

SSH 的实现可使用 `jsch`（依赖包：`jsch-0.1.42.jar`），思路与 Telnet 类似：建立会话 -> 用户名密码认证 -> 打开执行通道 -> 发送命令并读取输出。

```java
// 伪代码示意
JSch jsch = new JSch();
Session session = jsch.getSession(user, ip, 22);
session.setPassword(password);
session.setConfig("StrictHostKeyChecking", "no");
session.connect();
ChannelExec channel = (ChannelExec) session.openChannel("exec");
channel.setCommand(command);
channel.connect();
// 读取 channel.getInputStream() 获取命令输出
```

> 注：生产环境建议关闭密码明文传递的配置，优先使用密钥认证。
