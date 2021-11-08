# auto_start
## Overview
起動時にスクリプトを自動起動する方法に関する勉強．

## Note
自動起動スクリプトにコマンドを記入する場合はフルパスで記入する必要があるので注意．
```
// コマンドの定義場所の検索
$ which echo
> /usr/bin/echo
```
[【systemd】プログラム自動起動の設定時にハマったこと（ユーザ指定・Pythonパス指定・ウィンドウ表示）](https://dev.classmethod.jp/articles/systemd-setting-to-execute-program-automatically-on-start/)

## 自動起動方法
### systemdを使った自動化
これが最も自然なやり方．
- systemd: Linuxの起動処理やシステム管理を行う仕組み
- systemctl: systemdを制御するコマンド
#### 作成手順
1. 好きな場所に実行ファイル(スクリプト)を作成
   ```
   $ vim ~/sample.sh
   ```
2. ユニット定義ファイルの作成．
   ```
   $ ch /lib/systemd/system
   $ sudo vim name.service
   ```
   ```
   [Unit]
   Description="do ~/sample.sh"
   
   [Service]
   Type=simple
   after=[先に実行するサービス]
   ExecStart=/home/[username]/sample.sh %n
   ExecStop=/usr/bin/echo "stop ~/sample.sh"
   Restart=no
   
   [Install]
   
   ```
   [systemd のユニットファイルの作り方](https://tex2e.github.io/blog/linux/create-my-systemd-service)
3. ユニット定義ファイルの変更通知
   ```
   $ systemctl daemon-reload
   ```
4. サービスの起動・終了
   ```
   // サービスの起動
   $ systemctl start name.service
   $ systemctl is-active name.service
   > active
   
   // 別ターミナルを開きサービスのログ確認
   $ tail -f /var/log/messages
   
   // サービスの終了
   $ systemctl stop name.service
   $ systemctl is-active name.service
   > unknown
   ```

```
// サービス一覧表示
$ systemctl list-unit-files --type=service
$ systemctl list-unit-files --type=service | grep [service name]
// サービスの状態表示
$ systemctl status [service]
// サービスの自動起動の有効化
$ systemctl enable [service]
// サービスの自動起動の無効化
$ systemctl disable [service]
// サービスの停止
$ systemctl stop [service]
```
