---
title: 検証するドライバーを選択します。
description: 検証するドライバーを選択します。
ms.assetid: a752dea1-f49c-4e58-9e56-6b54701c760e
keywords:
- Driver Verifier WDK、ドライバーの選択
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2eb963341b9012da015bb1151c427d7de5423ef
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531933"
---
# <a name="selecting-drivers-to-be-verified"></a>検証するドライバーを選択します。


## <span id="ddk_selecting_drivers_to_be_verified_tools"></span><span id="DDK_SELECTING_DRIVERS_TO_BE_VERIFIED_TOOLS"></span>


使用して検証のためのドライバーを選択できる、 [ **Verifier のコマンド ライン**](verifier-command-line.md)、またはドライバー検証マネージャーを使用しています。 2 つのバージョンのドライバー検証マネージャー--に 1 つずつ[Windows 2000](driver-verifier-manager--windows-2000-.md)とに 1 つずつ[Windows XP 以降](driver-verifier-manager--windows-xp-and-later-.md)。

### <a name="span-idverifiercommandlinespanspan-idverifiercommandlinespanverifier-command-line"></a><span id="verifier_command_line"></span><span id="VERIFIER_COMMAND_LINE"></span>検証ツールのコマンドライン

すべてのドライバーを確認するため、 **/all**パラメーター。

ドライバーの一覧を確認するため、 **/driver**パラメーター。

参照してください[ **Verifier のコマンド ライン**](verifier-command-line.md)詳細についてはします。

### <a name="span-iddriververifiermanagerwindows2000spanspan-iddriververifiermanagerwindows2000spandriver-verifier-manager-windows-2000"></a><span id="driver_verifier_manager__windows_2000_"></span><span id="DRIVER_VERIFIER_MANAGER__WINDOWS_2000_"></span>ドライバー検証マネージャー (Windows 2000)

すべてのドライバーを確認するには、選択、**設定**タブ。選択**ドライバーをすべて検証**です。 キーを押します**適用**します。

ドライバーの一覧を確認するには、選択、**設定**タブ。選択**選択したドライバーを確認します。** します。 最新のブート中にシステムに読み込まれたすべてのドライバーの一覧が表示されます。

**検証ステータス**列は、各ドライバーの現在の状態を示します。 考えられる**検証ステータス**値は。

<span id="Enabled"></span><span id="enabled"></span><span id="ENABLED"></span>**有効になっています。**  
ドライバーは、現在検証されているされ、再起動後に検証するように続行されます。

<span id="Disabled"></span><span id="disabled"></span><span id="DISABLED"></span>**無効になっています。**  
ドライバーはされていない現在検証されている、再起動後に検証されません。

<span id="Enabled__Reboot_Needed_"></span><span id="enabled__reboot_needed_"></span><span id="ENABLED__REBOOT_NEEDED_"></span>**有効になっている (再起動が必要)**  
ドライバーは現在検証されているされませんが、ユーザーがこのドライバーの検証を要求します。 このドライバーは、再起動後に検証されます。

<span id="Disabled__Reboot_Needed_"></span><span id="disabled__reboot_needed_"></span><span id="DISABLED__REBOOT_NEEDED_"></span>**無効になっている (再起動が必要)**  
ドライバーは現在検証されているが、ユーザーがこの検証の終了を要求します。 再起動後、このドライバーを検証できなくされます。

この一覧から 1 つまたは複数のドライバーを選択してをクリックして、**を確認してください**または**確認しない**ボタンをクリックします。 ドライバーの名前とコントロールの検証 メニューから右クリックすることもできます。

**確認これら追加ドライバー後 [次へ] を再起動**テキスト ボックスを使用すると、現在システムに読み込まれるドライバーの名前を入力します。 複数の名前は、スペースで区切る必要があります。

検証するドライバーを選択すると、以下のキーを押して**適用**します。

すべてのオプションを非アクティブ化し、検証済みのドライバーの一覧をクリア、選択、**設定**タブ。キーを押して、**すべて元に戻す**ボタンをクリックします。 キーを押します**適用**します。

### <a name="span-iddriververifiermanagerwindowsxpandlaterspanspan-iddriververifiermanagerwindowsxpandlaterspandriver-verifier-manager-windows-xp-and-later"></a><span id="driver_verifier_manager__windows_xp_and_later_"></span><span id="DRIVER_VERIFIER_MANAGER__WINDOWS_XP_AND_LATER_"></span>ドライバー検証マネージャー (Windows XP 以降)

Windows XP とそれ以降のドライバー検証マネージャーでは、ドライバーの選択は、オプションの選択後に行う必要があります。 参照してください[ドライバー検証ツールのオプションの選択](selecting-driver-verifier-options.md)のこの最初の手順の説明。

最初の手順が完了したらと表示されます、**ことを確認するには、どのようなドライバーを選択**パネル。 さまざまな方法でドライバーを選択できます。

-   すべてのドライバーを確認するには、選択**このコンピューターにインストールされているすべてのドライバーを自動的に選択**します。

-   ドライバーの一覧を確認するには、選択**ドライバー名を一覧から選択**しキーを押します**次**します。 現在読み込まれているすべてのドライバーの一覧が表示されます。 (Windows XP 以降では、各ドライバーの現在の確認状態が示されません。)検証する各のドライバーの横にあるボックスを確認します。 一覧に示されていないドライバーを選択するキーを押して**追加現在読み込まれていないドライバーの一覧に**します。 これにより、必要なドライバーのファイル システムから参照できます。 キーを押して**オープン**一覧の先頭には、ドライバーを追加します。 検証用に選択するには、このドライバーの横にあるボックスを確認してください。

    Windows 8 以降、することがボタンを使用してドライバー検証マネージャーですべてのドライバーを選択する (**すべて選択**)、選択をオフ (**すべて選択解除**)、反転、および (**を反転します。選択**)。

-   署名されていないドライバーを確認するには、選択**未署名のドライバーを自動的に選択**します。 これらのドライバーの一覧が表示されます。 (このようなドライバーが存在しない場合、エラー メッセージが表示されます。)

-   以前のバージョンの Windows 向けに構築されたドライバーを確認するには、選択**の以前のバージョンの Windows の組み込みドライバーが自動的に選択**します。 これらのドライバーの一覧が表示されます。 (このようなドライバーが存在しない場合、エラー メッセージが表示されます。)

検証するドライバーを選択すると、いずれかを押して**次**または**完了**します。

ディスクの整合性チェックを有効にした場合は、コンピューターに接続されたすべての物理ディスクの一覧が表示されます。 チェックすることを確認して、キーを押します各ディスクの横にあるボックスをオン**完了**します。

すべてのオプションを非アクティブ化して、検証済みのドライバーの一覧を消去、ドライバー検証マネージャーを起動し、選択**既存の設定を削除**最初の画面から。 キーを押します**完了**します。

### <a name="span-idrebootrequiredspanspan-idrebootrequiredspanreboot-required"></a><span id="reboot_required"></span><span id="REBOOT_REQUIRED"></span>再起動が必要です。

Windows XP と Windows Server 2003 で開始し、(「再起動」) を再起動しなくてもドライバーの検証を停止、ドライバーが読み込まれていない場合にのみ、コンピューター。 詳細については、[揮発性の設定を使用する](using-volatile-settings.md)を参照してください。

以降では、Windows Vista は、開始および、コンピューターを再起動しなくても読み込まれていないドライバーの検証を停止できます。 再起動しなくても既に読み込まれているドライバーの検証を開始することもできます。 ただし、システムを再起動するまでは既に読み込まれているドライバーの検証を停止することはできません。 詳細については、[揮発性の設定を使用する](using-volatile-settings.md)を参照してください。

 

 





