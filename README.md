# Windows Setup

1. Chocolatey
2. ConEmu
3. Msys2
4. Atom Beta
4. Hain
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

## ２．ConEmu

### Msys2 の登録

#### Startup

- **Settings** -> **Startup** -> **Tasks**
  - `Msys2::bash`
  - `set CHERE_INVOKING=1 & MSYSTEM=MSYS & C:\tools\msys64\usr\bin\bash.exe --login -i -new_console:C:\tools\msys64\msys2.ico`

#### ConEmu Here

- **Settings** -> **Integration** -> **Command**
  - `set CHERE_INVOKING=1 & MSYSTEM=MSYS & C:\tools\msys64\usr\bin\bash.exe -c "export CONEMU_CURRENT=$PWD && /c/tools/msys64/usr/bin/bash.exe --login  -i -new_console:C:\tools\msys64\msys2.ico"`

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

##### Mouse button actions

- Right: <None>

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
'''

### pacman 設定ファイル

- /etc/pacman.conf

#### 色表示

- Color のコメントを外す

```
Color
```

## 4. ATOM Beta

- [Atom Beta](https://atom.io/beta)
  - 1.15.0-beta2

### Install Directory

- C:\Apps\Atom_Beta_x64

## Hain

- [GitHub:Release](https://github.com/appetizermonster/hain/releases)
  - v0.6.0

### hain-plugin-filesearch

- **Preferences** -> **hain-plugin-filesearch**
  - C:\Apps
