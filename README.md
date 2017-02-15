# Windows Setup
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

- ConEmu
- msys2
