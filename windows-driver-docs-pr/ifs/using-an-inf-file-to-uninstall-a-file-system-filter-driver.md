---
title: INF ファイルを使用したファイル システム フィルター ドライバーのアンインストール
description: INF ファイルを使用したファイル システム フィルター ドライバーのアンインストール
ms.assetid: e41deb65-7977-479c-ac42-c550aa6a3f1b
keywords:
- INF ファイル WDK ファイルシステム, フィルタードライバーのアンインストール
- フィルタードライバーのアンインストール WDK ファイルシステム
ms.date: 07/15/2019
ms.localizationpriority: medium
ms.openlocfilehash: 53511f98d83a7859e5f05769f287e0e90c46232f
ms.sourcegitcommit: f89a978ee23b9d2f925b13ea56b2c6cd48b4603a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2019
ms.locfileid: "68270227"
---
# <a name="using-an-inf-file-to-uninstall-a-file-system-filter-driver"></a>INF ファイルを使用したファイル システム フィルター ドライバーのアンインストール

ドライバーをアンインストールするには、コマンドライン、PowerShell、INF ファイルをバッチファイルと共に使用するか、ユーザーモードのアンインストールアプリケーションを使用します。

"右クリックアンインストール" オプションはありません。

## <a name="command-line-or-batch-file-uninstall"></a>コマンドラインまたはバッチファイルのアンインストール

INF ファイルの**defaultuninstall**および**defaultuninstall. Services**セクションをコマンドラインで実行するには、コマンドプロンプトで次のコマンドを入力するか、このコマンドを含むバッチファイルを作成して実行します。

```Command Line
RUNDLL32.EXE SETUPAPI.DLL,InstallHinfSection DefaultUninstall 132 path-to-uninstall-dir\infname.inf
```

**Rundll32**と**Installhinfsection**の詳細については、Microsoft Windows SDK のドキュメントの「ツールとセットアップ」と「システム管理」セクションを参照してください。

## <a name="powershell-uninstall"></a>Powershell のアンインストール

Powershell コマンドプロンプトで、次のコマンドを入力します。

```PowerShell
Get-CimInstance Win32_SystemDriver -Filter "name='your_driver_name'" | Invoke-CimMethod -MethodName Delete
```

## <a name="uninstall-application"></a>アプリケーションのアンインストール

次のコード例に示すように、アンインストールアプリケーションから INF ファイルの**defaultuninstall**および**defaultuninstall. Services**セクションを実行することもできます。

```cpp
InstallHinfSection(NULL,NULL,TEXT("DefaultUninstall 132 path-to-uninstall-dir\infname.inf"),0);
```

アプリケーションを使用してドライバーをアンインストールする場合は、次のガイドラインに従ってください。

* 最終的なアンインストールを準備するには、セットアップアプリケーションで、ドライバーの INF ファイルをアンインストールディレクトリにコピーする必要があります。
* INF ファイルの**defaultuninstall. Services**セクションでは、 **delservice**ディレクティブで、削除前にサービスを停止する\_ように、常に 0x200 (SPSVCINST stopservice) フラグを指定する必要があります。
* ユーザーモードアプリケーションがドライバーと共にインストールされている場合は、ユーザーが必要に応じてアンインストールできるように、コントロールパネルの [プログラムの追加と削除] にこのアプリケーションが表示されます。 アプリケーションとドライバーの両方を表す項目が1つだけ表示されます。 [プログラムの追加と削除] でアプリケーションを一覧表示する方法の詳細については、Microsoft Windows SDK ドキュメントの「セットアップとシステム管理」セクションの「アプリケーションの削除」を参照してください。
* アンインストールアプリケーションでは、Windows inf ファイルディレクトリ ( *% windir%\\INF*) から inf ファイル (またはそれに関連付けられている PNF ファイル) を削除しないでください。
* 一部のフィルタードライバーファイルは、アプリケーションのアンインストール時に安全に削除できません。 これらのファイルは、INF ファイルの**Defaultuninstall. Services**セクションには記載されていません。

アプリケーションのアンインストールの詳細については、「[デバイスインストールアプリケーションの作成](https://docs.microsoft.com/windows-hardware/drivers/install/writing-a-device-installation-application)」を参照してください。
