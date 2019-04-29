---
title: 揮発性の設定の使用
description: 揮発性の設定の使用
ms.assetid: 16fb8c2a-60d8-4c0a-879d-447a1cda5415
keywords:
- Driver Verifier の WDK、揮発性の設定
- WDK の Driver Verifier の揮発性の設定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb1aa9c074a96f4da35f7e0b366c7dbfa43117c6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326182"
---
# <a name="using-volatile-settings"></a>揮発性の設定の使用


## <span id="ddk_using_volatile_settings_tools"></span><span id="DDK_USING_VOLATILE_SETTINGS_TOOLS"></span>


Driver Verifier の状態 (アクティブ化、非アクティブ化、オプションの変更または検証されているドライバーの一覧を変更する) をほとんど変更をコンピューター (「再起動」) を再起動する場合にのみ有効です。

ただし、アクティブ化し、再起動しなくてもいくつかのオプションを非アクティブ化できます。 呼ばれる、*揮発性の設定。* これらの設定の変更がすぐに有効、最後と次のブートまで、またはもう一度変更されるまでです。

このセクションでは、揮発性の設定と、さまざまなバージョンの Windows に含まれるドライバーの検証ツールのバージョンで使用する方法について説明します。

### <a name="span-idchangingoptionswithoutrebootingspanspan-idchangingoptionswithoutrebootingspanchanging-options-without-rebooting"></a><span id="changing_options_without_rebooting"></span><span id="CHANGING_OPTIONS_WITHOUT_REBOOTING"></span>再起動しなくてもオプションを変更します。

アクティブ化して以外のすべての Driver Verifier のオプションを非アクティブ化[DDI 準拠の検査](ddi-compliance-checking.md)、 [Power Framework 遅延ファジー テスト](concurrency-stress-test.md)、 [Storport 検証](dv-storport-verification.md)、[SCSI 検証](scsi-verification.md)と[ディスクの整合性チェック](disk-integrity-checking.md)コンピューターを再起動しなくてもします。

**注**  Windows Vista より前の Windows のバージョンでは、アクティブ化して、コンピューターを再起動しなくても、次の Driver Verifier のオプションのみを非アクティブ化します。 ただし、ドライバーの検証ツールが既に実行されている必要がありますのでは、Driver Verifier を少なくとも 1 つのオプションを使用して開始して、コンピューターを再起動します。 これを実行した後は、アクティブ化しても再起動せず、これらの設定を非アクティブ化します。
-   [特別なプール](special-pool.md)

-   [強制 IRQL 検査](force-irql-checking.md)

-   [低リソース シミュレーション](low-resources-simulation.md)

 

### <a name="span-idchangingdriverswithoutrebootingspanspan-idchangingdriverswithoutrebootingspanchanging-drivers-without-rebooting"></a><span id="changing_drivers_without_rebooting"></span><span id="CHANGING_DRIVERS_WITHOUT_REBOOTING"></span>再起動しなくてもドライバーを変更します。

以降では、Windows Vista は、追加し、ドライバーの検証が実行されていない場合でも、コンピューターを再起動しなくてもドライバー (つまり、開始、停止、ドライバーの検証) を削除することができます。

再起動しなくても既に読み込まれているドライバーの検証を開始することもできますが、再起動しなくても、ドライバーの検証を停止することはできません。 ドライバーが読み込まれると検証されているドライバーの検証ツールを監視、次回の再起動までがオフにできます Driver Verifier のオプションを確認します、ドライバーを再起動しなくても Driver Verifier のオーバーヘッドを最小限に抑えます。

Windows XP および Windows Server 2003 では、追加し、のみ場合、ドライバーは現在読み込まれていないが、再起動しなくてもドライバーを削除することができます。

揮発性の設定を変更するにを使用して、 [ **Verifier のコマンド ライン**](verifier-command-line.md)、またはドライバー検証マネージャー。 2 つのバージョンのドライバー検証マネージャー--に 1 つずつ[Windows 2000](driver-verifier-manager--windows-2000-.md)とに 1 つずつ[Windows XP 以降](driver-verifier-manager--windows-xp-and-later-.md)。

### <a name="span-idvolatileandregistrysettingsspanspan-idvolatileandregistrysettingsspanvolatile-and-registry-settings"></a><span id="volatile_and_registry_settings"></span><span id="VOLATILE_AND_REGISTRY_SETTINGS"></span>揮発性とレジストリ設定

大きな利便性は、追加、ドライバーの変更とを再起動しなくてもオプションを設定できるとは利用できない一部のテスト シナリオで Driver Verifier を実行することができます。

ただし、従来、ドライバーの検証の設定をレジストリに追加のモデルにいくつかの利点があるため、各設定の揮発性のメソッドを使用するか、レジストリ、またはその両方で設定するかどうかを決定する必要があります。

-   揮発性または"runtime"の設定が、すぐに有効になりますが、シャット ダウン、または Windows を再起動すると、これらの設定が失われます。

-   レジストリ設定には、再起動が必要ですが、それらを変更し、もう一度再起動するまで、レジストリのままにします。

設定を一貫して使用するか、ドライバーの読み込み中に測定する必要がありますはレジストリに追加する必要があります。 必要なときに、その他の設定を有効にすることができます。

レジストリ設定と揮発性の設定の両方を使用する場合、レジストリの設定ではなく、揮発性の設定が使用されることに注意してください。追加機能ではありません。

### <a name="span-idconfiguringvolatilesettingsbyusingtheverifiercommandlinespanspan-idconfiguringvolatilesettingsbyusingtheverifiercommandlinespanconfiguring-volatile-settings-by-using-the-verifier-command-line"></a><span id="configuring_volatile_settings_by_using_the_verifier_command_line"></span><span id="CONFIGURING_VOLATILE_SETTINGS_BY_USING_THE_VERIFIER_COMMAND_LINE"></span>検証ツールのコマンドラインを使用して、揮発性の設定を構成します。

追加または削除揮発性のオプションを使用して、 **/volatile/flags**パラメーター。

(Windows XP 以降)を追加または揮発性の一覧からドライバーを削除するには使用、 **/volatile/adddriver**または **/volatile/removedriver**パラメーター。 参照してください[ **Driver Verifier のコマンド構文**](verifier-command-line.md)詳細についてはします。

-   開始または再起動することがなく、ドライバーの検証を停止します。

    ```
    verifier /volatile /adddriver DriverName.sys
    verifier /volatile /removedriver DriverName.sys
    ```

    このコマンドの構文を使用して追加することができます (検証を開始) の任意のドライバーも現在読み込まれているドライバーです。 コマンドに現在読み込まれているドライバーの削除 (検証を停止する) は失敗します。 として常に、ドライバーが読み込まれるとすぐに読み込まれていないドライバーの検証が開始されます。

-   アクティブ化または再起動することがなくオプションを非アクティブ化します。

    ```
    verifier /volatile /flags Options
    ```

    ドライバーの検証オプションのいずれかでこのコマンドの構文を使用するには除く[SCSI 検証](scsi-verification.md)と[ディスクの整合性チェック](disk-integrity-checking.md)します。 以下に例を示します。

    ```
    verifier /volatile /flags 0x20
    ```

    このコマンドをアクティブ化、[デッドロックの検出](deadlock-detection.md)を再起動しなくてもオプションです。

-   すべてのドライバーの検証オプションをオフにするには。

    再起動しなくても現在読み込まれているドライバーの検証を停止することはできません。 ただし、次回の再起動までのオーバーヘッドを最小限に抑えるため、再起動することがなくすべてのドライバーの検証オプションを非アクティブ化するのに次のコマンド構文を使用できます。

    ```
    verifier /volatile /flags 0
    ```

    Driver Verifier の継続のオプションを使用してドライバーを監視する、[自動チェック](automatic-checks.md)機能、これをオフにすることはできませんが、一般的な検証のオーバーヘッドの約 10% にオーバーヘッドが削減されます。

### <a name="span-idconfiguringvolatilesettingsbyusingdriververifiermanagerwindows2kspanspan-idconfiguringvolatilesettingsbyusingdriververifiermanagerwindows2kspanspan-idconfiguringvolatilesettingsbyusingdriververifiermanagerwindows2kspanconfiguring-volatile-settings-by-using-driver-verifier-manager-windows-2000"></a><span id="configuring_volatile_settings_by_using_driver_verifier_manager__windows2K"></span><span id="configuring_volatile_settings_by_using_driver_verifier_manager__windows2k"></span><span id="CONFIGURING_VOLATILE_SETTINGS_BY_USING_DRIVER_VERIFIER_MANAGER__WINDOWS2K"></span>ドライバー検証マネージャー (Windows 2000) を使用して、揮発性の設定を構成します。

**揮発性の設定を変更するには**

1.  をクリックして、**揮発性の設定**タブ。

2.  機能を有効にするには、機能の (「確認」)、チェック ボックスを選択します。

3.  (「オフ」) をオフにする機能を無効にするには、チェック ボックスを使用します。

4.  クリックして**適用**変更を適用します。

ドライバー検証マネージャー オプションを示します Driver Verifier 現在実際には、揮発性の設定を含む、変更を永続的な設定を有効にする次の再起動後にスケジュールされています。 各ドライバーは、その状態が表示されている必要があります。

### <a name="span-idconfiguringvolatilesettingsbyusingdriververifiermanagerwindowspanspan-idconfiguringvolatilesettingsbyusingdriververifiermanagerwindowspanconfiguring-volatile-settings-by-using-driver-verifier-manager-windows-xp-and-later"></a><span id="configuring_volatile_settings_by_using_driver_verifier_manager__window"></span><span id="CONFIGURING_VOLATILE_SETTINGS_BY_USING_DRIVER_VERIFIER_MANAGER__WINDOW"></span>揮発性の設定を使用してドライバー検証マネージャーの構成 (Windows XP 以降)

**現在アクティブなドライバーの検証機能を表示したり、揮発性の設定を変更するには**

1.  ドライバー検証マネージャーを起動し、選択、**現在検証済みのドライバーに関する情報を表示**タスク。

2.  **[次へ]** をクリックします。

    この画面では、永続的な設定を有効にする次の再起動後にスケジュールされている、Driver Verifier のオプション現在の変更を含まないが、実際には、揮発性の設定などが表示されます。 各ドライバーは、その状態が表示されている必要があります。

3.  アクティブなオプションを変更する をクリックして**変更**します。 選択または目的のオプションをオフにし、クリックして**OK**します。

4.  新しいドライバーを確認するには、クリックして**追加**します。 これにより、ドライバー ファイルを確認するには、コンピューターを参照するダイアログ ボックスが開きます。 適切なドライバーを特定すた後には、次のようにクリックします。**オープン**検証済みのドライバーの一覧に追加します。

5.  を一覧からドライバーを削除するドライバーの名前を選択し をクリックして**削除**します。

6.  変更が完了したらは有効または Driver Verifier のオプションの表示が完了したらをクリックします**次**、2 回クリックして**完了**します。

### <a name="span-iddriverstatusvaluesspanspan-iddriverstatusvaluesspandriver-status-values"></a><span id="driver_status_values"></span><span id="DRIVER_STATUS_VALUES"></span>ドライバーの状態の値

ドライバー検証マネージャーに表示されているドライバーの 3 つの状態の値を示しています、**現在の設定と検証済みのドライバー (実行時の情報)** 画面。 状態の値は次のとおりです。

<span id="Loaded"></span><span id="loaded"></span><span id="LOADED"></span>**読み込まれました。**  
ドライバーは、現在読み込まれている検証中です。

<span id="Unloaded"></span><span id="unloaded"></span><span id="UNLOADED"></span>**アンロード**  
ドライバーは読み込まれ、最後の起動後に少なくとも 1 回確認しますが、現在アンロードされてです。

<span id="Never_Loaded"></span><span id="never_loaded"></span><span id="NEVER_LOADED"></span>**読み込まれていません。**  
Driver Verifier は、このドライバーを確認する指示されましたが、この要求の後、ドライバーが読み込まれていません。 これは、ドライバーが要求時に読み込まれ、このセッションでの必要はまだありませんに示していることができます。 検証のため、要求されたドライバーが存在しない場合に、またはドライバーのイメージ ファイルが破損していることを示している可能性もします。

### <a name="span-iddisplayingvolatilesettingsbyusingdriververifiermanagerwindowsspanspan-iddisplayingvolatilesettingsbyusingdriververifiermanagerwindowsspandisplaying-volatile-settings-by-using-driver-verifier-manager-windows-2000"></a><span id="displaying_volatile_settings_by_using_driver_verifier_manager__windows"></span><span id="DISPLAYING_VOLATILE_SETTINGS_BY_USING_DRIVER_VERIFIER_MANAGER__WINDOWS"></span>ドライバー検証マネージャー (Windows 2000) を使用して、揮発性の設定を表示します。

現在アクティブなドライバーの検証機能を表示するには、いずれかを選択、 **ドライバ ステータスの**または**揮発性の設定**タブ。

これらの画面の各オプションを示します Driver Verifier 現在実際には、揮発性の設定を含む、変更を永続的な設定を有効にする次の再起動後にスケジュールされています。 各ドライバーは、その状態が表示されている必要があります。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[**Driver Verifier のコマンド構文**](verifier-command-line.md)

[Driver Verifier を制御します。](controlling-driver-verifier.md)

 

 






