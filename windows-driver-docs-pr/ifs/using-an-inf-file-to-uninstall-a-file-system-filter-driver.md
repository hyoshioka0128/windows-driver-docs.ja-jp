---
title: ファイル システム フィルター ドライバーをアンインストールする INF ファイルを使用します。
description: ファイル システム フィルター ドライバーをアンインストールする INF ファイルを使用します。
ms.assetid: e41deb65-7977-479c-ac42-c550aa6a3f1b
keywords:
- INF ファイル WDK ファイル システム フィルター ドライバーをアンインストールします。
- フィルター ドライバー WDK ファイル システムのアンインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 062b126b9bc0becca59cff7a1ef470c4fbd83dd4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530088"
---
# <a name="using-an-inf-file-to-uninstall-a-file-system-filter-driver"></a>ファイル システム フィルター ドライバーをアンインストールする INF ファイルを使用します。


## <span id="ddk_using_an_inf_file_to_uninstall_a_file_system_filter_driver_if"></span><span id="DDK_USING_AN_INF_FILE_TO_UNINSTALL_A_FILE_SYSTEM_FILTER_DRIVER_IF"></span>


ドライバーをアンインストールするには、バッチ ファイルと共に、INF ファイルを使用して、またはユーザー モードでアプリケーションをアンインストールします。

「アンインストールを右クリックして」のオプションはありません。

### <a name="span-idcommand-lineorbatchfileuninstallspanspan-idcommand-lineorbatchfileuninstallspanspan-idcommand-lineorbatchfileuninstallspancommand-line-or-batch-file-uninstall"></a><span id="Command-Line_or_Batch_File_Uninstall"></span><span id="command-line_or_batch_file_uninstall"></span><span id="COMMAND-LINE_OR_BATCH_FILE_UNINSTALL"></span>コマンドラインまたはバッチ ファイルのアンインストール

実行する、 **DefaultUninstall**と**DefaultUninstall.Services**コマンドラインで、INF ファイルのセクションでは、コマンド プロンプトで次のコマンドを入力または作成し、バッチ ファイルを実行このコマンドが含まれます。

```cpp
RUNDLL32.EXE SETUPAPI.DLL,InstallHinfSection DefaultUninstall 132 path-to-uninstall-dir\infname.inf
```

**Rundll32**と**InstallHinfSection**されて、ツール、セットアップとシステム管理のセクションはそれぞれ、Microsoft Windows SDK ドキュメントの。

### <a name="span-iduninstallapplicationspanspan-iduninstallapplicationspanspan-iduninstallapplicationspanuninstall-application"></a><span id="Uninstall_Application"></span><span id="uninstall_application"></span><span id="UNINSTALL_APPLICATION"></span>アプリケーションをアンインストールします。

実行することも、 **DefaultUninstall**と**DefaultUninstall.Services** INF のセクションでは次のコード例に示すように、アプリケーションのアンインストールからファイルします。

```cpp
InstallHinfSection(NULL,NULL,TEXT("DefaultUninstall 132 path-to-uninstall-dir\infname.inf"),0); 
```

アプリケーションを使用して、ドライバーをアンインストールする場合は、次のガイドラインに従います。

-   最終的なアンインストールの準備として、セットアップ アプリケーションは、ディレクトリのアンインストールにドライバーの INF ファイルをコピーする必要があります。

-   **DefaultUninstall.Services** 、INF ファイルのセクション、 **DelService**ディレクティブは、0x200 を常に指定する必要があります (SPSVCINST\_STOPSERVICE) が前に、サービスを停止するフラグ削除されます。

-   ドライバーを使用した、ユーザー モード アプリケーションがインストールされた場合、ユーザーでアンインストールに必要な場合はようにこのアプリケーションは追加またはコントロール パネルの [プログラムの削除] に表示する必要があります。 アプリケーションとドライバーの両方を表す 1 つの項目を表示する必要があります。

    追加と削除 で、アプリケーションの一覧を表示する方法の詳細については、Microsoft Windows sdk のセットアップとシステム管理のセクションでは"を削除する an Application"を参照してください。

-   アプリケーションのアンインストールまたは削除しないでください、INF ファイル (関連付けられた PNF ファイル)、Windows の INF ファイルのディレクトリから (*%windir%\\INF*)。

-   いくつかのフィルター ドライバー ファイルは、アプリケーションのアンインストール時に安全に削除できません。 これらのファイルに表示されませんが、 **DefaultUninstall.Services** INF ファイルのセクション。

詳細については、アプリケーションのアンインストールを参照してください[デバイス インストール アプリケーションを記述して](https://msdn.microsoft.com/library/windows/hardware/ff554015)します。

 

 




