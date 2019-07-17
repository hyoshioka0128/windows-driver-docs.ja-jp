---
title: INF ファイルを使用したファイル システム フィルター ドライバーのアンインストール
description: INF ファイルを使用したファイル システム フィルター ドライバーのアンインストール
ms.assetid: e41deb65-7977-479c-ac42-c550aa6a3f1b
keywords:
- INF ファイル WDK ファイル システム フィルター ドライバーをアンインストールします。
- フィルター ドライバー WDK ファイル システムのアンインストール
ms.date: 07/15/2019
ms.localizationpriority: medium
ms.openlocfilehash: 53511f98d83a7859e5f05769f287e0e90c46232f
ms.sourcegitcommit: 6790f79bafb69c53e655b40810e24a11081e5038
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68270227"
---
# <a name="using-an-inf-file-to-uninstall-a-file-system-filter-driver"></a>INF ファイルを使用したファイル システム フィルター ドライバーのアンインストール

コマンドライン、PowerShell、バッチ ファイルと共に、INF ファイルを使用して、ドライバーをアンインストールするまたはユーザー モードでアプリケーションをアンインストールします。

「アンインストールを右クリックして」のオプションはありません。

## <a name="command-line-or-batch-file-uninstall"></a>コマンドラインまたはバッチ ファイルのアンインストール

実行する、 **DefaultUninstall**と**DefaultUninstall.Services**コマンドラインで、INF ファイルのセクションでは、コマンド プロンプトで次のコマンドを入力または作成し、バッチ ファイルを実行このコマンドが含まれます。

'' コマンド ライン RUNDLL32 します。EXE SETUPAPI します。DLL、InstallHinfSection DefaultUninstall 132 パスにする-アンインストール-dir\infname.inf
```

**Rundll32** and **InstallHinfSection** are described in the Tools and Setup and System Administration sections, respectively, of the Microsoft Windows SDK documentation.

## Powershell Uninstall

Type the following command at the Powershell command prompt:

```PowerShell
Get-CimInstance Win32_SystemDriver -Filter "name='your_driver_name'" | Invoke-CimMethod -MethodName Delete
```

## <a name="uninstall-application"></a>アプリケーションをアンインストールします。

実行することも、 **DefaultUninstall**と**DefaultUninstall.Services** INF のセクションでは次のコード例に示すように、アプリケーションのアンインストールからファイルします。

```cpp
InstallHinfSection(NULL,NULL,TEXT("DefaultUninstall 132 path-to-uninstall-dir\infname.inf"),0);
```

アプリケーションを使用して、ドライバーをアンインストールする場合は、次のガイドラインに従います。

* 最終的なアンインストールの準備として、セットアップ アプリケーションは、ディレクトリのアンインストールにドライバーの INF ファイルをコピーする必要があります。
* **DefaultUninstall.Services** 、INF ファイルのセクション、 **DelService**ディレクティブは、0x200 を常に指定する必要があります (SPSVCINST\_STOPSERVICE) が前に、サービスを停止するフラグ削除されます。
* ドライバーを使用した、ユーザー モード アプリケーションがインストールされた場合、ユーザーでアンインストールに必要な場合はようにこのアプリケーションは追加またはコントロール パネルの [プログラムの削除] に表示する必要があります。 アプリケーションとドライバーの両方を表す 1 つの項目を表示する必要があります。 追加と削除 で、アプリケーションの一覧を表示する方法の詳細については、Microsoft Windows sdk のセットアップとシステム管理のセクションでは"を削除する an Application"を参照してください。
* アプリケーションのアンインストールまたは削除しないでください、INF ファイル (関連付けられた PNF ファイル)、Windows の INF ファイルのディレクトリから ( *%windir%\\INF*)。
* いくつかのフィルター ドライバー ファイルは、アプリケーションのアンインストール時に安全に削除できません。 これらのファイルに表示されませんが、 **DefaultUninstall.Services** INF ファイルのセクション。

詳細については、アプリケーションのアンインストールを参照してください[デバイス インストール アプリケーションを記述して](https://docs.microsoft.com/windows-hardware/drivers/install/writing-a-device-installation-application)します。
