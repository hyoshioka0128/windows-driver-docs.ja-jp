---
title: 統合された表示パネルでの明るさコントロールのサポート
description: 統合された表示パネルでの明るさコントロールのサポート
ms.assetid: d32ee274-569e-4adc-a723-28dc756fb177
keywords:
- 明るさ WDK ディスプレイ
- ACPI ベースの明るさホットキー WDK ディスプレイ
- 輝度ホットキーの通知 (WDK 表示)
- BIOS 輝度制御 WDK ディスプレイ
- 自動輝度 WDK 表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3af37e60ee0a25ab56943561bcb763187cdb90e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829402"
---
# <a name="supporting-brightness-controls-on-integrated-display-panels"></a>統合された表示パネルでの明るさコントロールのサポート


明るさの制御は、オペレーティングシステムによって提供されるモニタードライバーである Monitor に実装されます。 モニタードライバーは、Windows Management Instrumentation (WMI) インターフェイスを実装して、アプリケーション (オペレーティングシステムの明るさスライダーなど) が輝度レベルと対話できるようにします。 モニタードライバーはデバイスの電源ポリシーエンジン (供給された PE) に登録して、明るさのレベルが電源ポリシーの変化に反応するようにします。 モニタードライバーは、ACPI ベースの明るさのショートカットキーを処理するために、Advanced Configuration and Power Interface (ACPI) に登録します。 [Windows 2000 Display Driver モデル](windows-2000-display-driver-model-design-guide.md)との互換性を確保するために、モニタードライバーは IOCTL ベースの明るさコントロールを実装します。

システムの基本入出力システム (BIOS) によって公開されている表示ミニポートドライバーまたは ACPI メソッドは、統合された表示パネルの明るさの変更をサポートできます。 [ **\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_video_output_technology)コンピューター内で内部的に接続される出力テクノロジを持つとマークされている最初のビデオターゲットでは、モニタードライバーはディスプレイミニポートドライバーの[**DxgkDdiQueryInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_interface)関数を呼び出して、GUID\_devinterface\_輝度\_2 および DXGK\_輝度\_インターフェイス\_バージョン\_1、および明るさの制御によって識別される[輝度制御インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を照会します。 [Interface v. 2 (アダプティブおよび Smooth 輝度コントロール)](https://docs.microsoft.com/windows-hardware/drivers/ddi/index) 。 GUID\_DEVINTERFACE\_輝度と DXGK\_輝度\_インターフェイス\_バージョン\_2 によって識別されます。 ディスプレイミニポートドライバーで少なくとも輝度制御インターフェイスがサポートされていない場合、モニタードライバーは ACPI を使用して、子デバイスの \_BCL、\_BCM、および \_BQC の各メソッドを照会します。 これらの方法の詳細については、 [acpi web サイト](https://go.microsoft.com/fwlink/p/?linkid=57185)の acpi 仕様を参照してください。

**注**   Windows Display Driver MODEL (WDDM) では、統合された表示パネルを識別するために ACPI 識別子は使用されません。 これは、id が0x0110 の表示パネルのみをサポートする[Windows 2000 Display Driver モデル](windows-2000-display-driver-model-design-guide.md)とは異なります。

 

[ミニポートドライバーの表示] または [BIOS で公開されている ACPI] メソッドで明るさの制御がサポートされている場合、モニタードライバーは、明るさのショートカットキーの ACPI 通知を登録します。 ショートカットキーの通知についてモニタードライバーに通知するための代替手段はありません。 モニタドライバーが輝度制御メカニズムを使用できない場合、またはディスプレイミニポートドライバーで[輝度制御インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)が提供されているが、 [**DxgkDdiGetPossibleBrightness**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgk_brightness_get_possible)関数の呼び出しに失敗した場合、モニタードライバーは明るさの制御をサポートしていません。

### <a name="span-idbrightness_levelsspanspan-idbrightness_levelsspanspan-idbrightness_levelsspanbrightness-levels"></a><span id="Brightness_Levels"></span><span id="brightness_levels"></span><span id="BRIGHTNESS_LEVELS"></span>明るさのレベル

明るさのレベルは、0 ~ 100 の範囲の1バイトの値として表されます。0はオフ、100は、ラップトップコンピューターがサポートする最大の明るさです。 すべてのラップトップコンピューターは、最大輝度レベル100を報告する必要があります。ただし、1つのラップトップコンピューターでは、レベル0をサポートする必要はありません。 値が 0 ~ 100 の場合は、大きな値が高い明るさのレベルを表す必要があります。 レベル間の増分は一様である必要はありません。また、ラップトップコンピューターでは、最大101レベルまでの個別の値をいくつでもサポートできます。 ハードウェアレベルを明るさのレベルの値の範囲にマップする方法を決める必要があります。 ただし、ディスプレイミニポートドライバーの[**DxgkDdiGetPossibleBrightness**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgk_brightness_get_possible)関数を呼び出すと、ハードウェアがサポートしているよりも多くの明るさレベルの値を報告することはできません。

### <a name="span-iddisabling_automatic_brightness_changes_by_the_biosspanspan-iddisabling_automatic_brightness_changes_by_the_biosspanspan-iddisabling_automatic_brightness_changes_by_the_biosspandisabling-automatic-brightness-changes-by-the-bios"></a><span id="Disabling_Automatic_Brightness_Changes_by_the_BIOS"></span><span id="disabling_automatic_brightness_changes_by_the_bios"></span><span id="DISABLING_AUTOMATIC_BRIGHTNESS_CHANGES_BY_THE_BIOS"></span>BIOS による明るさの自動変更を無効にする

システム BIOS とモニタードライバーの両方がディスプレイパネルの明るさを制御している場合に発生する可能性のある問題を回避するために、ディスプレイミニポートドライバーでは、引数のビット2を \_DOS メソッドに設定する必要があります。 \_の DOS メソッドとその引数の詳細については、「ACPI 仕様」を参照してください。 ビット2を設定すると、システム BIOS は、明るさの自動変更を実行しないように通知されます。

### <a name="span-idbios_requirements_to_support_brightness_controlsspanspan-idbios_requirements_to_support_brightness_controlsspanspan-idbios_requirements_to_support_brightness_controlsspanbios-requirements-to-support-brightness-controls"></a><span id="BIOS_Requirements_to_Support_Brightness_Controls"></span><span id="bios_requirements_to_support_brightness_controls"></span><span id="BIOS_REQUIREMENTS_TO_SUPPORT_BRIGHTNESS_CONTROLS"></span>明るさの制御をサポートする BIOS の要件

最適な方法で統合パネルの明るさの制御をサポートするミニポートドライバーを表示するには、システム BIOS が ACPI を通じて次の項目を提供する必要があります。

-   明るさの制御方法

    統合パネルデバイスでは、ACPI 輝度制御の方法 (\_BCL、\_BCM、\_BQC) がサポートされている必要があります。 \_BCL と \_BCM は、ACPI 仕様のバージョン 1.0 b 以降は変更されていません。これらの定義は、「b. 6.2 and B 6.3」の ACPI 3.0 仕様に記載されています。 \_BQC は省略可能であり、セクション B-1 の ACPI 3.0 仕様で定義されています。 明るさのレベルの定義については、「明るさのレベル」を参照してください。

    次に示すのは、Dispmprt に定義されている ACPI 輝度制御メソッドのエイリアスです。

    -   [ACPI\_メソッド\_出力\_]-Windows がディスプレイ出力デバイスでサポートされている明るさレベルの一覧を照会できるようにします。 この方法は、統合 LCD が存在し、明るさのレベルをサポートしている場合に必要です。
    -   ACPI\_方法\_出力\_BCMÂ Windows で表示出力デバイスの明るさのレベルを設定できるようにします。 Windows によって設定されるのは、ACPI\_メソッド\_出力\_BCL メソッドによって報告されたレベルのみです。 Acpi\_メソッド\_OUTPUT\_BCL メソッドが実装されている場合は\_、\_出力\_BCM メソッドを出力する必要があります。
-   システム BIOS の自動輝度制御を無効にする

    システム BIOS は、システム BIOS の自動輝度変更を無効にするために、グラフィックスアダプターの \_DOS メソッドに対して引数のビット2を設定することをサポートする必要があります。 このビットは、このメソッドのビットに対して以前に定義した値に加算されます。 このビットの詳細については、ACPI 3.0 仕様の「4.1」セクションを参照してください。 このビットがサポートされていない場合は、モニタードライバーとシステム BIOS の両方で輝度レベルを変更することができます。これにより、明るさがちらつくため、明るさがユーザーが要求した値ではない値に設定される可能性があります。

    ACPI 自動輝度制御メソッドのエイリアスは、次のように定義されています。

    -   ACPI\_メソッド\_表示\_を表示する-システム BIOS がアクティブな表示出力を自動的に切り替えることができるか、または LCD の明るさを制御できることを示します。 次に、許可されるパラメーターを示します。
        -   ACPI\_ARG\_\_自動\_LCD\_の明るさを有効にします。 AC から DC に電力が変化したときに、システム BIOS で LCD の明るさのレベルを自動的に制御する必要があることを示します。
        -   ACPI\_ARG\_\_自動\_LCD\_明るさを無効にします。 AC から DC に電力が変化したときに、システム BIOS で LCD の明るさのレベルを自動的に制御しないように指定します。
-   明るさのショートカットキーの通知

    明るさのショートカットキーの通知は、グラフィックスアダプターではなく、統合された表示パネルデバイスを対象としている必要があります。

    次の通知は、「Dispmprt. h」で定義されているとおりにサポートされています。

    -   ACPI\_通知\_サイクル\_明るさ\_ホットキー-ユーザーが画面の明るさを切り替えるためにホットキーを押しました。
    -   ACPI\_\_INC\_輝度\_ホットキーに通知します。ユーザーは、画面の明るさを上げるためにホットキーを押しました。
    -   ACPI\_\_DEC\_の明るさ\_ホットキーに通知します。ユーザーは、画面の明るさを下げるためにホットキーを押しました。
    -   ACPI\_\_ゼロ\_明るさ\_ホットキー-ユーザーが画面の明るさを0に下げるためにホットキーを押しました。

    これらのショートカットキーの通知は、ACPI 3.0 仕様の新しいものであり、セクション B-1 で説明されています。 通常、ラップトップコンピューターは、これらのショートカットキーの通知をすべてサポートしているわけではありません。

    ACPI\_に対するモニタードライバーの既定の動作\_INC\_の明るさ\_ホットキーおよび ACPI\_通知\_10 月\_の明るさ\_を通知の明るさを下げる (または、前の明るさのレベルより少なくとも5% 以上)。次に使用可能な5% のステップレベルに到達するまで (5、10、15、...、95、100)。 ショートカットキーを使用してインクリメントまたはデクリメントを行うと、次の例に示すように、非対称パターンが輝度レベルで作成される場合があります。

    -   使用可能な \_BCL 輝度制御レベル0、1、5、10、...、95、100

        <span id="Results_using_the_ACPI_NOTIFY_INC_BRIGHTNESS_HOTKEY_notification_"></span><span id="results_using_the_acpi_notify_inc_brightness_hotkey_notification_"></span><span id="RESULTS_USING_THE_ACPI_NOTIFY_INC_BRIGHTNESS_HOTKEY_NOTIFICATION_"></span>ACPI\_通知\_INC\_輝度\_ホットキー通知を使用した結果:  
        0、5、10、15、20、25、30、35、40、45、50、55、60、65、70、75、80、85、90、95、100

        <span id="Results_using_the_ACPI_NOTIFY_DEC_BRIGHTNESS_HOTKEY_notification_"></span><span id="results_using_the_acpi_notify_dec_brightness_hotkey_notification_"></span><span id="RESULTS_USING_THE_ACPI_NOTIFY_DEC_BRIGHTNESS_HOTKEY_NOTIFICATION_"></span>ACPI\_通知\_DEC\_の明るさ\_ホットキー通知を使用した場合の結果:  
        100、95、90、85、80、75、70、65、60、55、50、45、40、35、30、25、20、15、10、5、0

    -   1、5、10、...、95、100として指定されている \_BCL 輝度制御レベルを利用できます

        <span id="Results_using_the_ACPI_NOTIFY_INC_BRIGHTNESS_HOTKEY_notification_"></span><span id="results_using_the_acpi_notify_inc_brightness_hotkey_notification_"></span><span id="RESULTS_USING_THE_ACPI_NOTIFY_INC_BRIGHTNESS_HOTKEY_NOTIFICATION_"></span>ACPI\_通知\_INC\_輝度\_ホットキー通知を使用した結果:  
        1、10、15、20、25、30、35、40、45、50、55、60、65、70、75、80、85、90、95、100

        <span id="Results_using_the_ACPI_NOTIFY_DEC_BRIGHTNESS_HOTKEY_notification_"></span><span id="results_using_the_acpi_notify_dec_brightness_hotkey_notification_"></span><span id="RESULTS_USING_THE_ACPI_NOTIFY_DEC_BRIGHTNESS_HOTKEY_NOTIFICATION_"></span>ACPI\_通知\_DEC\_の明るさ\_ホットキー通知を使用した場合の結果:  
        100、95、90、85、80、75、70、65、60、55、50、45、40、35、30、25、20、15、10、5、1

    後者の例では、1が使用可能な最後の値であるため、ドライバーは、前の値5と異なる5パーセントの単位ではなく、明るさのレベルを1に設定します。

    このモニタドライバーの既定の動作は、DWORD の値を変更することで上書きできます。 次のレジストリキーの**Minimumsteppercentage** :

    `HKEY_LOCAL_MACHINE\ SYSTEM\ CurrentControlSet\ Services\` *Monitor*`\ Parameters\`

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[表示出力と ACPI イベントのサポート](supporting-display-output.md)

 

 






