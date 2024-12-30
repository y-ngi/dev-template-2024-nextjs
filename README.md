# 初めに

フロントエンド開発環境の土台を作成します。  

## 構築する環境

- volta
- node
- npm
- Next.js 15
  - TypeScript
  - ESLint
  - Tailwind CSS

また、開発用のスタブサーバ（APIサーバ）としてwiremockも準備する

## 1. 前提環境

- wsl2(ubuntu-22.04)
- vscode
- docker（wiremock用）

## 2. Node.js環境構築

初めにVoltaのインストールを行います.  
既に指定のNode.jsの環境を構築済みの方は飛ばしても良いですが、プロジェクト毎のNode&npmのバージョン管理をvoltaにて行うことを前提とするため、可能な限りインストールしてください.  

### 2.1. Voltaインストール

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

### 2.2. node インストール

※本手順はプロジェクト新規立ち上げする時だけの手順です. **プロジェクトに途中参加する場合、実行不要**

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

## 3. プロジェクト作成

※ GitHubから作成済みプロジェクトをチェックアウトした場合は、本手順を飛ばして [『4. プロジェクト初期化』](#4-プロジェクト初期化) へ

``` shell
npx create-next-app@15

✔ What is your project named? … next-app
✔ Would you like to use TypeScript? … Yes
✔ Would you like to use ESLint? … Yes
✔ Would you like to use Tailwind CSS? … Yes
✔ Would you like your code inside a `src/` directory? … Yes
✔ Would you like to use App Router? (recommended) … Yes
✔ Would you like to use Turbopack for `next dev`? … No
✔ Would you like to customize the import alias (`@/*` by default)? … Yes
✔ What import alias would you like configured? … @/*
Creating a new Next.js app in /home/y-ngi/work/dev-template-2024-nextjs/next-app.
```

Next.js 15 のプロジェクトが作成できたので起動確認

``` shell
cd next-app
npm run dev
```

## 4. プロジェクト初期化

### 4.1. プロジェクトに必要なパッケージをインストールしテスト起動

``` shell
cd next-app                     # プロジェクトディレクトリに移動
npm install --save-dev          # 開発用モジュールのインストール
npm run dev                     # 開発環境にてアプリ起動
# 以下必要に応じて以下の手順でスタブサーバも起動してください
cd ../tools/wiremock            # スタブサーバのディレクトリに移動
docker-compose up -d            # スタブサーバ起動
docker-compose down             # スタブサーバ終了(使い終わったら)
```
