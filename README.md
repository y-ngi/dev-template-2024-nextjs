# 初めに

フロントエンド開発環境の土台を作成します。  

## 構築する環境

- volta
- node
- npm
- NextJS
- vite

また、開発用のスタブサーバ（APIサーバ）としてwiremockも準備する

## 前提環境

- wsl2(ubuntu-22.04)
- vscode
- docker（wiremock用）

## Node.js環境構築

初めにVoltaのインストールを行います.  
既に指定のNode.jsの環境を構築済みの方は飛ばしても良いですが、プロジェクト毎のNode&npmのバージョン管理をvoltaにて行うことを前提とするため、可能な限りインストールしてください.  

### (1) Voltaインストール

``` shell
curl https://get.volta.sh | bash
source ~/.bashrc
volta -v
 2.0.2  # インストールに成功していれば voltaのバージョンが表示される
```

上記コマンドを実行してVoltaのインストールを行います.  
voltaのバージョンが表示されていればインストール成功です.  
もしも表示されなかった場合は、コマンド実行時に出ているエラーメッセージなどをご確認ください.  

尚、インストールに成功していれば、`.~/.bashrc` の末尾に以下の設定が書き込まれているハズです.

``` shell
export VOLTA_HOME="$HOME/.volta"
export PATH="$VOLTA_HOME/bin:$PATH"
```

### (2) node インストール

#### 本手順はプロジェクト新規立ち上げする時だけの手順です. プロジェクトに途中参加する場合、実行不要.

新規にプロジェクトを立ち上げる場合、以下のコマンドでプロジェクトで使用するバージョンのnodeインストールと、voltaによるバージョン固定を行ってください

``` shell
volta install node@<指定するバージョン>
volta pin node@<指定するバージョン>
# node v20.18.1 の場合
# volta install node@20.18.1
# volta pin node@20.18.1
```

この設定を行うことで、voltaがnodeのバージョンを管理してくれるようになります. 

#### 以下は全員実行

``` shell
cd <プロジェクトフォルダ>
node -v
# プロジェクト指定バージョンのnodeがインストールされてる
```

voltaでバージョン指定されたプロジェクトフォルダ内に移動した後に、nodeを実行することでvoltaが自動的に指定バージョンのnodeをインストールします
