# Telnetサーバ構築マニュアル

### telnetdインストール

```bash
sudo apt update
sudo apt install telnetd -y
```

### inetdの状態確認

```bash
sudo systemctl status inetd
```

### telnetサービス設定確認

設定ファイル /etc/inetd.conf を確認する。
```bash
sudo vi /etc/inetd.conf
```

以下の行を有効にする

```bash
telnet stream tcp nowait telnetd /usr/sbin/tcpd /usr/sbin/telnetd
```

### inetd再起動

```bash
sudo systemctl restart inetd
```
以下のコマンドでActiveがactive(running)になっているか確認
```bash
sudo systemctl status inetd
```

### ポート確認
```bash
sudo ss -tlnp | grep :23
```

### 接続確認
同マシンの場合
```bash
telnet localhost
```
別のマシンの場合
```bash
telnet ＜IPアドレス＞
```