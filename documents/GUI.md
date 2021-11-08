# GUI
## SSH接続時のGUIアプリの実行
### Ultra96(-V2)のセットアップ
```
// SSHサーバのインストール
$ sudo apt update
$ sudo apt install openssh-server

// X Window Systemのインストール
$ sudo apt install xserver-xorg

// X転送を有効にする
$ vim /etc/ssh/sshd_config
...
X11Forwarding yes
...

// sshdの再起動(Ultra96(-V2)を再起動するのが確実)
$ systemctl restart sshd
```

### MobaXtermを使用してWindowsPCで表示する場合(動作確認済)
MobaXtermはXサーバの機能も含むので簡単にGUIアプリ表示が可能．
1. MobaXtermのインストール
2. ファイアウォールは使用するネットワークに応じてPrivate/Publicに許可を与える．
3. `Settings`->`Configuration`->`X11`->`X11 remote access: full`に変更
4. `Session`->`SSH`->IP等記入してUltra96(-V2)にssh接続する
5. メッセージ画面に以下のように表示されるのを確認
```
X11-forwarding: ✓ (remote display is forwarded through SSH)
```
6. 画面出力先の確認(デフォルトのままでOKなはず)
```
$ echo $DISPLAY
> localhost:10.0
```
7. GUIアプリの動作確認
```
$ sudo apt install x11-apps
$ xeyes

$ sudo apt install gimp
$ gimp
```

### Tera Termを使用する場合(未確認)
1. Tera Termの`設定`->`SSH転送`->`リモートの(X)アプリケーションをローカルのXサーバに表示する`
2. VcXsrvやXmingなどのX serverを起動
3. Tera Termでssh接続

### 通常のTerminalからSSH接続する場合(未確認)
1. VcXsrvやXmingなどのX serverを起動
2. 以下のコマンドでSSH接続
```
$ ssh -YC fpga@192.168.*.*
```

## Note
- ssh接続先はubuntu-desktopがインストールされていないCUI環境でもOK
- ssh: 他のサーバにsshで接続する場合
- sshd: 他からsshで接続される場合

## Reference
- [Ubuntu 20.04 LTS に後から GUI (X Window System) を追加する](https://blog.amedama.jp/entry/ubuntu-2004-install-gui)
