---
title: INF ファイルを使用したファイル システム フィルター ドライバーのインストール
description: INF ファイルを使用したファイル システム フィルター ドライバーのインストール
ms.assetid: 0bc70cdb-d115-4329-9fcc-a085a57c5f78
keywords:
- INF ファイル WDK ファイル システムのインストール手順
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc33292c5b1e054d9c559ee2c556a51dc430fe20
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380290"
---
# <a name="using-an-inf-file-to-install-a-file-system-filter-driver"></a>INF ファイルを使用したファイル システム フィルター ドライバーのインストール


## <span id="ddk_using_an_inf_file_to_install_a_file_system_filter_driver_if"></span><span id="DDK_USING_AN_INF_FILE_TO_INSTALL_A_FILE_SYSTEM_FILTER_DRIVER_IF"></span>


INF ファイルを作成した後は、インストール、アップグレード、およびファイル システム フィルター ドライバーをアンインストールに使用できます。 単独でまたはバッチ ファイルまたはと共にユーザー モードのセットアップ アプリケーション INF ファイルを使用することができます。

### <a name="span-idright-clickinstallspanspan-idright-clickinstallspanspan-idright-clickinstallspanright-click-install"></a><span id="Right-Click_Install"></span><span id="right-click_install"></span><span id="RIGHT-CLICK_INSTALL"></span>インストールを右クリックします。

実行する、 [ **DefaultInstall** ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-defaultinstall-section)と[ **DefaultInstall.Services** ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-defaultinstall-services-section)のセクションでは、INF ファイルの次を行う必要があります。

1.  Windows エクスプ ローラーでは、INF ファイル名を右クリックします。 ショートカット メニューが表示されます。

2.  **[インストール]** をクリックします。

**注**   INF ファイルが含まれている場合にのみ、ショートカット メニューが表示されます、 **DefaultInstall**セクション。

 

### <a name="span-idcommand-lineorbatchfileinstallspanspan-idcommand-lineorbatchfileinstallspanspan-idcommand-lineorbatchfileinstallspancommand-line-or-batch-file-install"></a><span id="Command-Line_or_Batch_File_Install"></span><span id="command-line_or_batch_file_install"></span><span id="COMMAND-LINE_OR_BATCH_FILE_INSTALL"></span>コマンドラインまたはバッチ ファイルのインストール

実行する、 **DefaultInstall**と**DefaultInstall.Services**コマンドラインまたはバッチ ファイルのインストールを使用して、INF ファイルのセクションは、コマンド プロンプトで次のコマンドを入力または作成し、このコマンドが含まれたバッチ ファイルを実行します。

```cpp
RUNDLL32.EXE SETUPAPI.DLL,InstallHinfSection DefaultInstall 132 path-to-inf\infname.inf
```

"Rundll32"と"InstallHinfSection"が、ツール、セットアップとシステム管理で説明されているセクションをそれぞれの Microsoft Windows SDK のドキュメント。

### <a name="span-idsetupapplicationspanspan-idsetupapplicationspanspan-idsetupapplicationspansetup-application"></a><span id="Setup_Application"></span><span id="setup_application"></span><span id="SETUP_APPLICATION"></span>アプリケーションをセットアップします。

[**InstallHinfSection** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-installhinfsectiona)次のコード例に示すように、セットアップ アプリケーションから呼び出すもできます。

```cpp
InstallHinfSection(NULL,NULL,TEXT("DefaultInstall 132 path-to-inf\infname.inf"),0); 
```

ドライバーをインストールするセットアップ アプリケーションを使用する場合は、次のガイドラインに従います。

-   最終的なアンインストールの準備として、セットアップ アプリケーションは、ディレクトリのアンインストールにドライバーの INF ファイルをコピーする必要があります。

-   セットアップ アプリケーションでは、ドライバーを使用した、ユーザー モード アプリケーションをインストールする場合、ユーザーでアンインストールに必要な場合はようにこのアプリケーションは追加またはコントロール パネルの [プログラムの削除] に表示する必要があります。 アプリケーションとドライバーの両方を表す 1 つの項目を表示する必要があります。

    追加と削除 で、アプリケーションの一覧を表示する方法の詳細については、Windows sdk のセットアップとシステム管理のセクションでは"を削除する an Application"を参照してください。

-   アプリケーションをセットアップする必要があります Windows INF ファイルのディレクトリにドライバーの INF ファイルをコピーしない ( *%windir%\\INF*)。 SetupAPI がファイルを自動的にコピーの一部として、 [ **InstallHinfSection** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-installhinfsectiona)呼び出します。

セットアップ アプリケーションの詳細については、次を参照してください。[デバイス インストール アプリケーションを記述して](https://docs.microsoft.com/windows-hardware/drivers/install/writing-a-device-installation-application)します。

 

 




