# Windows Setup

1. Chocolatey
2. ConEmu
3. Msys2
4. Atom Beta
5. Hain
6. Oracke JDK

---

## 1. Chocolatey

- [Install](https://chocolatey.org/install)
  - [Uninstall](https://chocolatey.org/docs/uninstallation)

### Execution_Policies 対応

```
このシステムではスクリプトの実行が無効になっているため、ファイル C:\Users\<username>\AppData\Local\Temp\chocolatey\chocI
nstall\tools\chocolateyInstall.ps1 を読み込むことができません。詳細については、「about_Execution_Policies」(http://go.m
icrosoft.com/fwlink/?LinkID=135170) を参照してください。
発生場所 行:164 文字:3
+ & $chocInstallPS1
+   ~~~~~~~~~~~~~~~
    + CategoryInfo          : セキュリティ エラー: (: ) []、PSSecurityException
    + FullyQualifiedErrorId : UnauthorizedAccess
```

PowerShell の実行ポリシーによりはじかれるため設定を変更する

- PowerShell を管理者権限で起動
- 次のコマンドで権限を確認:

```
PS C:\WINDOWS\system32> Get-ExecutionPolicy
Restricted
```

- 次のコマンドで **Unrestricted** に変更:

```
PS C:\WINDOWS\system32> Set-ExecutionPolicy -ExecutionPolicy Unrestricted
```

### Chocolatey のインストール

```
PS C:\WINDOWS\system32> iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))
```

#### インストール・ディレクトリ

- C:\ProgramData\chocolatey

### Chocolatey 管理アプリケーション

- msys2
  - `choco install msys2`
    - 20160719.1.1
- ConEmu
  - `choco install conemu`
    - ConEmu 17.1.18.0

- Source Code Pro Programming Font
  - `choco install sourcecodepro`
    - 2.030.0

---

## ２．ConEmu

### Msys2 の登録

#### Startup

- **Settings** -> **Startup** -> **Tasks**
  - `Msys2::bash`
  - `set CHERE_INVOKING=1 & MSYSTEM=MSYS & C:\tools\msys64\usr\bin\bash.exe --login -i -new_console:C:\tools\msys64\msys2.ico`

#### ConEmu Here

- **Settings** -> **Integration** -> **Command**
  - `set CHERE_INVOKING=1 & set MSYSTEM=MSYS & C:\tools\msys64\usr\bin\bash.exe -c "export CONEMU_CURRENT=$PWD && /c/tools/msys64/usr/bin/bash.exe --login  -i -new_console:C:\tools\msys64\msys2.ico"`

- **/etc/profile**
```
if [ -n ${CONEMU_CURRENT} ]; then
    cd ${CONEMU_CURRENT}
else
    cd ~
fi
```

### 基本設定

#### Main

- **Settings** -> **Main**

##### Font

- Font: Source Code Pro
- Anti aliasing: Clear Type
##### Monospace

- Monospace: OFF

#### Main::Size & Pos

##### Aligmment

- Center console in workspace: ON
- Pad size (pixels): 10

#### Main::Appearance

##### Title bar

- Hide caption always: ON

#### Features::Colors

##### Schemes

- Schemes: <Solarized>

#### Keys & Macro::Mark/Copy

##### Select text with keybord

- Start selection with Shift + Arrow: ON

#### Keys & Macro::Paste

##### Paste mode

- Shift+Instert: Do nothing
- Ctrl+v: Multi lines

##### Mouse button actions

- Right: <None>

---

## 3. Msys2

### pacmanパッケージ管理

#### パッケージのアップグレード(yum update)

```
$ pacman -Syu
```

- S: --sync(同期)
- y: --refresh(リポジトリデータベースと同期)
- u: --upgrades(更新)

#### リポジトリデータベースの最新情報取得

```
$ pacman -Syy
```

#### パッケージのインストール(yum install)

```
$ pacman -S git
$ pacman -S --noconfirm vim
```

#### パッケージのアンインストール(yum remove)

```
$ pacman -Rs php
```

- s: --search(依存関係を検索)

#### リポジトリデータベースのパッケージの検索(yum search)

```
$ pacman -Ss ruby
```

#### リポジトリデータベースのパッケージの詳細情報表示(yum info)

```
$ pacman -Si ruby
```

#### インストール済みパッケージのリストアップ

```
$ pacman -Qqe
```

### pacman 設定ファイル

- /etc/pacman.conf

#### 色表示

- Color のコメントを外す

```
Color
```

### 3.1. git

- `pacmand -S git`

```
$ git config --global user.name "shinyay"
$ git config --global user.email "shinya.com@gmail.com"
$ git config --global core.editor 'vim -c "set fenc=utf-8"'
$ git config --global color.diff auto
$ git config --global color.status auto
$ git config --global color.branch auto
```

### 3.2. SDKMAN!

```
$ curl -s "https://get.sdkman.io" | bash
$ source "$HOME/.sdkman/bin/sdkman-init.sh"
```

#### Beta Channel

```
$ sed -i.bak '/sdkman_beta/s/false/true/g' ${HOME}/.sdkman/etc/config
$ sdk selfupdate force
```

#### Maven

```
$ sdk install maven
```

#### sbt

```
$ sdk install sbt
```


## 4. ATOM Beta

- [Atom Beta](https://atom.io/beta)
  - 1.15.0-beta2

### Install Directory

- C:\Apps\Atom_Beta_x64

### Atom Packages Synchronization with apm stars

```
$ apm login
$ apm stars --installed
$ apm start --install
```

## 5. Hain

- [GitHub:Release](https://github.com/appetizermonster/hain/releases)
  - v0.6.0

### hain-plugin-filesearch

- **Preferences** -> **hain-plugin-filesearch**
  - C:\Apps

## 6. Oracke JDK

```
ORACLE_JDK_URL=http://download.oracle.com/otn-pub/java/jdk/8u121-b13/e9e7ea248e2c4826b92b3f075a80e441/jdk-8u121-windows-x64.exe

wget --no-cookies --no-check-certificate --header "Cookie: oraclelicense=accept-securebackup-cookie" "${ORACLE_JDK_URL}"
```

### Install Path

- **C:\Java\jdk1.8.0_121**

### システム環境変数

- JAVA_HOME
- C:\Java\jdk1.8.0_121

## 7. Oracle Enterprise Pack for Eclipse

```
$ wget --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn_software/oepe/12.2.1.5/neon/oepe-12.2.1.5-neon-distro-win32-x86_64.zip
```
