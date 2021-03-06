## ユースケース

このドキュメントでは、LinuxまたはMac OSのローカルPCでSSHを利用してLinuxインスタンスにログインする方法について説明します。

##  対応OS

Linux または Mac OS

## 認証方式

**パスワード**または**キー**です。

## 前提条件
- インスタンスにログインするための管理者アカウント及びパスワード(またはキー)は取得しました。
 - システムのデフォルトパスワードを利用してインスタンスにログインする場合は、[サイト内メール](https://console.cloud.tencent.com/message)にアクセスして取得してください。
 - インスタンスを[キーでログインする](#LoginWithKey) 場合、キーの作成を完了して、CVMにキーをバインドする必要があります。 詳細の操作については、[SSHキー](http://intl.cloud.tencent.com/document/product/213/16691)をご参照ください。
 - パスワードを忘れた場合、[インスタンスパスワードをリセット](http://intl.cloud.tencent.com/document/product/213/16566)してください。
- CVMインスタンスはすでにパブリックIPを購入されており、このインスタンスは22ポート（クイック設定で購入したCVMインスタンスの場合、デフォルトで開放している）を開放しました。

## 操作手順

### パスワードでログインする

1. 次のコマンドを実行して、Linux CVMに接続します。
> ローカルPCがMac OSシステムの場合、最初にシステム付属のターミナル（Terminal）を開き、次のコマンドを実行する必要があります。
> ローカルPCがLinuxシステムの場合、次のコマンドを直接実行できます。
>
```
ssh <username>@<hostname or IP address>
```
 - `username` は、前提条件で取得されたデフォルトのアカウントです。
 - `hostname or IP address` は Linux インスタンスのパブリックIPアドレス或いはカスタムドメイン名です。
2. 取得したパスワードを入力し、**Enter**キーを押してログインを完了します。

<span id="LoginWithKey"></span>
### キーでログインする

1. 次のコマンドを実行して、プライベートキーファイルに本人だけ読み取り権限を付与します。
> ローカルPCがMac OSシステムの場合、最初にシステム付属のターミナル（Terminal）を開き、次のコマンドを実行する必要があります。
> ローカルPCがLinuxシステムの場合、次のコマンドを直接実行できます。
>
```
chmod 400 <ダウンロードしたCVMに関連するプライベートキーの絶対パス>
```
2. 次のコマンドを実行して、リモートログインします。
```
ssh -i <ダウンロードしたCVMに関連するプライベートキーの絶対パス> <username>@<hostname or IP address>
```
 - `username` は、前提条件で取得したデフォルトのアカウントです。
 - `hostname or IP address` は Linux インスタンスのパブリックIPアドレス或いはカスタムドメイン名です。

 例えば、 `ssh -i "Mac/Downloads/shawn_qcloud_stable" ubuntu@192.168.11.123` コマンドを実行して、Linux CVMにリモートログインします。
