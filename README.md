# auto_tunnelblick_googleauth
One click to connect to a tunnelblick VPN that requires Google Authenticator.

解决使用Tunnelblick VPN时需要手动输入OTP Code的烦恼。

# 使用方法

## 首次使用

```bash
git clone https://github.com/wangyufeng0615/auto_tunnelblick_googleauth.git
cd auto_tunnelblick_googleauth
chmod +x vpn.sh
./vpn.sh setup vpn_name account password otp_key
```
其中，这些参数的含义是：
- vpn_name: 你导入到tunnelblick里的vpn配置的名字，一定要输入正确。
- account: 你的VPN账号。
- password: 你的VPN密码。
- otp_key: 你导入到Google身份验证器里的原始OTP Key。一般长16位。如果你拿到的是一个二维码，将二维码解码后就可以看到Key了。

如果输入有误，重新以正确的参数执行setup即可。

## 开启VPN
```./vpn.sh on VPN_NAME```
将`VPN_NAME`替换为你VPN的名称，注意不是用户名。

ps. 如果只常用一个VPN，可设置alias进一步简化操作。

## 关闭VPN
```./vpn.sh off VPN_NAME```

# 原理及安全性

这个脚本会将你的VPN名称、用户名、密码和OTP原始Key，存到系统自带的keychain中。连接VPN时，使用你的OTP Key，生成OTP Code并和你的VPN密码拼接起来（这一步和Google Authenticator的原理并无二致），并通过Applescript传递给Tunnelblick，令其连接指定VPN。

这种方案的有点是安全性好，毕竟我们日常使用的大量密码也都存在keychain里。

缺点则是损失了一定的便捷性，有时仍然需要输入macOS的用户密码。

## License

MIT
