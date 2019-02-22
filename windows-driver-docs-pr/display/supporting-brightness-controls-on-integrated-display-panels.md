---
title: パネルの統合ディスプレイの明るさコントロールをサポート
description: パネルの統合ディスプレイの明るさコントロールをサポート
ms.assetid: d32ee274-569e-4adc-a723-28dc756fb177
keywords:
- WDK のディスプレイの明るさ
- Acpi の明るさのホット キー WDK の表示
- WDK の表示の明るさのホット キーを通知します。
- BIOS の明るさコントロール WDK の表示
- 自動明るさ WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0aaa29e791956762959ca0567e4eaabbfccf7f03
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536677"
---
# <a name="supporting-brightness-controls-on-integrated-display-panels"></a>パネルの統合ディスプレイの明るさコントロールをサポート


明るさコントロールは、オペレーティング システムによって付与されたモニター ドライバー Monitor.sys で実装されます。 モニター ドライバーでは、明るさのレベルと対話するアプリケーション (など、オペレーティング システムの明るさのスライダー) を許可する Windows Management Instrumentation (WMI) インターフェイスを実装します。 モニター ドライバーは、明るさのレベルは、電源ポリシーの変更に対応できるように、デバイスの電源ポリシー エンジン (DPPE) とを登録します。 モニター ドライバーは、acpi の明るさのショートカット キーを処理するには、Advanced Configuration and Power Interface (ACPI) を登録します。 互換性のため、 [Windows 2000 Display Driver Model](windows-2000-display-driver-model-design-guide.md)、モニター ドライバーは、IOCTL ベースの明るさコントロールを実装します。

ディスプレイ ミニポート ドライバーまたはシステムの基本入出力システム (BIOS) の統合ディスプレイの明るさを変更することができますサポートによって公開される ACPI メソッド。 内部的には、コンピューターに接続する出力のテクノロジを持つものとしてマークされている最初のビデオ ターゲット ([**D3DKMDT\_VOT\_内部**](https://msdn.microsoft.com/library/windows/hardware/ff546605))、モニター ドライバーの呼び出し、ディスプレイ ミニポート ドライバーの[ **DxgkDdiQueryInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff559764)関数のクエリを[明るさコントロール インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff538260)GUIDによって識別されています\_DEVINTERFACE\_明るさ\_2 および DXGK\_明るさ\_インターフェイス\_バージョン\_1、および[明るさコントロール インターフェイス V します。2 (適応性が滑らかな輝度)](https://msdn.microsoft.com/library/windows/hardware/jj647485) GUID によって識別される\_DEVINTERFACE\_明るさと DXGK\_明るさ\_インターフェイス\_バージョン\_2。 照会するモニター ドライバーが ACPI を使用して、ディスプレイのミニポート ドライバーがサポートしない場合、少なくとも、明るさコントロール インターフェイス、 \_BCL、 \_BCM、および\_子デバイス BQC メソッド。 これらのメソッドの詳細については、の ACPI 仕様を参照して、 [ACPI の web サイト](https://go.microsoft.com/fwlink/p/?linkid=57185)します。

**注**  で、Windows 表示 Driver Model (WDDM)、ACPI 識別子は、統合表示パネルを識別するために使用されません。 異なる、 [Windows 2000 Display Driver Model](windows-2000-display-driver-model-design-guide.md)、サポートするだけ 0x0110 の識別子を持つパネルが表示されます。

 

ACPI の BIOS に公開されているメソッドまたはディスプレイ ミニポート ドライバーで明るさコントロールをサポートしている場合、モニター ドライバーは、明るさのショートカット キーの ACPI 通知を登録します。 ショートカット キーの通知について、モニターのドライバーを通知するために代わるメカニズムが存在しません。 モニター ドライバーは、いずれかの明るさコントロール メカニズムを使用できない場合、または、ディスプレイのミニポート ドライバーを提供している場合、[明るさコントロール インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff538260)への呼び出しが失敗したが、 [ **DxgkDdiGetPossibleBrightness** ](https://msdn.microsoft.com/library/windows/hardware/ff559661)関数、モニターのドライバーが明るさコントロールをサポートしていません。

### <a name="span-idbrightnesslevelsspanspan-idbrightnesslevelsspanspan-idbrightnesslevelsspanbrightness-levels"></a><span id="Brightness_Levels"></span><span id="brightness_levels"></span><span id="BRIGHTNESS_LEVELS"></span>明るさのレベル

明るさのレベルは、0 から 100、0 がオフと 100 はラップトップ コンピューターをサポートする最大の明るさの範囲の 1 バイトの値として表されます。 100 です。 最大輝度レベルをすべてのラップトップ コンピューターが報告する必要があります。ただし、ラップトップ コンピューターでは、0 のレベルをサポートする必要はありません。 0 から 100 までの値の唯一の要件より大きな値が高い明るさを表す必要があります。 レベル間のインクリメントは、一様にする必要はありませんし、ラップトップ コンピューターは、任意の数の最大レベルの 101 の個別の値をサポートできます。 ハードウェアのレベルをレベルの明るさの値の範囲にマップする方法を決定する必要があります。 ただし、ディスプレイのミニポート ドライバーへの呼び出し[ **DxgkDdiGetPossibleBrightness** ](https://msdn.microsoft.com/library/windows/hardware/ff559661)関数は、ハードウェアがサポートよりも多くの輝度レベル値を報告する必要があります。

### <a name="span-iddisablingautomaticbrightnesschangesbythebiosspanspan-iddisablingautomaticbrightnesschangesbythebiosspanspan-iddisablingautomaticbrightnesschangesbythebiosspandisabling-automatic-brightness-changes-by-the-bios"></a><span id="Disabling_Automatic_Brightness_Changes_by_the_BIOS"></span><span id="disabling_automatic_brightness_changes_by_the_bios"></span><span id="DISABLING_AUTOMATIC_BRIGHTNESS_CHANGES_BY_THE_BIOS"></span>BIOS で自動の明るさの変更を無効にします。

システムの BIOS と、モニター ドライバーの両方を制御パネルの輝度を表示する場合に発生する可能性のある問題を避けるためには、ディスプレイのミニポート ドライバーがする引数のビット 2 を設定します。、 \_DOS メソッド。 詳細については、 \_DOS メソッドとその引数は、ACPI 仕様を参照してください。 設定するビット 2 の場合は、明るさを自動変更を実行しないでくださいシステム BIOS が通知されます。

### <a name="span-idbiosrequirementstosupportbrightnesscontrolsspanspan-idbiosrequirementstosupportbrightnesscontrolsspanspan-idbiosrequirementstosupportbrightnesscontrolsspanbios-requirements-to-support-brightness-controls"></a><span id="BIOS_Requirements_to_Support_Brightness_Controls"></span><span id="bios_requirements_to_support_brightness_controls"></span><span id="BIOS_REQUIREMENTS_TO_SUPPORT_BRIGHTNESS_CONTROLS"></span>明るさコントロールをサポートする BIOS 要件

最適な方法で統合されたパネルの明るさの制御をサポートするためにディスプレイ ミニポート ドライバーでは、システム BIOS は、ACPI を通じて、次のものを提供する必要があります。

-   コントロールの明るさのメソッド

    統合されたパネルのデバイスを ACPI の明るさコントロールのメソッドをサポートする必要があります (\_BCL、 \_BCM、および\_BQC)。 \_BCL と\_BCM には、ACPI 仕様のバージョン 1.0b 以降は変更されていません。 セクション B.6.2 および B.6.3 の ACPI 3.0 の仕様でその定義を見つけることができます。 \_BQC は省略可能で、B.6.4 のセクションでは ACPI 3.0 仕様で定義されています。 明るさのレベルの定義、明るさのレベルを参照してください。

    以下は、Dispmprt.h で定義されている ACPI の明るさコントロール メソッドの別名です。

    -   ACPI\_メソッド\_出力\_BCLÂ - 表示出力のデバイスでサポートされる明るさレベルの一覧を照会するは、Windows。 このメソッドは、統合の LCD が存在し、明るさのレベルをサポートしている場合に必要です。
    -   ACPI\_メソッド\_出力\_BCMÂ - 出力のディスプレイの明るさのレベルを設定するのには、Windows。 Windows は、ACPI によって報告されたレベルを設定してのみ\_メソッド\_出力\_BCL メソッド。 ACPI\_メソッド\_出力\_BCM 方法は、必要な場合、ACPI\_メソッド\_出力\_BCL メソッドを実装します。
-   自動システム BIOS の輝度を無効にします。

    システム BIOS に引数の設定ビット 2 をサポートする必要があります、 \_DOS メソッド グラフィックス アダプターを無効にする自動システム BIOS の明るさの変更を許可します。 このビットは、このメソッド内のビットの定義済みの値の追加です。 詳細については、このビットは、ACPI 3.0 の仕様の B.4.1」セクションを参照してください。 このビットがサポートされていない場合は、その結果、ちらつきの明るさの輝度レベル両方を変更することができますモニター ドライバーとシステム BIOS と、明るさはどのようなユーザー要求されていない値に設定のままにできる可能性があります。

    ACPI の明るさを自動制御メソッドの次のエイリアスは、Dispmprt.h で定義されます。

    -   ACPI\_メソッド\_表示\_DOSÂ - は、システムの BIOS が自動的にアクティブな表示出力の切り替えや、LCD の輝度を制御できることを示します。 許可されているパラメーターを次に示します。
        -   ACPI\_ARG\_を有効にする\_自動\_LCD\_明るさ。 システム BIOS が自動的に管理する LCD の明るさ、電源が AC から DC に変更されたときに記載されています。
        -   ACPI\_ARG\_を無効にする\_自動\_LCD\_明るさ。 システム BIOS がいない自動的に管理する、LCD の明るさのレベル、電源が AC から DC に変更されたときに記載されています。
-   ショートカット キーの明るさの通知

    明るさのショートカット キーの通知は、グラフィックス アダプターが、統合表示パネル デバイスを対象とする必要があります。

    Dispmprt.h で定義されている、次の通知がサポートされます。

    -   ACPI\_通知\_サイクル\_明るさ\_ホットキー - ユーザーが押したホットキーのディスプレイの明るさを循環します。
    -   ACPI\_通知\_INC\_明るさ\_ホットキー - ユーザーが押したホットキーのディスプレイの明るさを増やすことです。
    -   ACPI\_通知\_DEC\_明るさ\_ホットキー - ユーザーが押したホットキー ディスプレイの明るさを減らすためです。
    -   ACPI\_通知\_0\_明るさ\_ホットキー - ユーザーが押したホットキーをゼロにディスプレイの明るさを減らすためです。

    これらのショートカット キーの通知は、ACPI 3.0 仕様に新しい B.7 のセクションで説明します。 通常、ラップトップ コンピューターでは、すべてこれらのショートカット キーの通知のサポートはしません。

    ACPI のモニター ドライバーの既定の動作\_通知\_INC\_明るさ\_ホットキーと ACPI\_通知\_DEC\_明るさ\_ホット キー通知が明るさをインクリメント (またはデクリメント) を詳細には少なくとも 5% (以下) 前の輝度レベルよりも 5% の使用可能な手順の次のレベルに到達するまで (5、10、15、…、95, 100)。 インクリメントまたはデクリメントのショートカット キーでは、次の例に示すとして非対称のパターンを明るさのレベルに作成できます。

    -   使用可能な\_として 0、1、5、10、…、95 に指定された BCL の明るさコントロール レベル 100

        <span id="Results_using_the_ACPI_NOTIFY_INC_BRIGHTNESS_HOTKEY_notification_"></span><span id="results_using_the_acpi_notify_inc_brightness_hotkey_notification_"></span><span id="RESULTS_USING_THE_ACPI_NOTIFY_INC_BRIGHTNESS_HOTKEY_NOTIFICATION_"></span>ACPI を使用して結果を\_通知\_INC\_明るさ\_ホットキー通知。  
        0, 5, 10, 15, 20, 25, 30, 35, 40, 45, 50, 55, 60, 65, 70, 75, 80, 85, 90, 95, 100

        <span id="Results_using_the_ACPI_NOTIFY_DEC_BRIGHTNESS_HOTKEY_notification_"></span><span id="results_using_the_acpi_notify_dec_brightness_hotkey_notification_"></span><span id="RESULTS_USING_THE_ACPI_NOTIFY_DEC_BRIGHTNESS_HOTKEY_NOTIFICATION_"></span>ACPI を使用して結果を\_通知\_DEC\_明るさ\_ホットキー通知。  
        100, 95, 90, 85, 80, 75, 70, 65, 60, 55, 50, 45, 40, 35, 30, 25, 20, 15, 10, 5, 0

    -   使用可能な\_95 では、1、5、10、...、指定された BCL の明るさコントロール レベル 100

        <span id="Results_using_the_ACPI_NOTIFY_INC_BRIGHTNESS_HOTKEY_notification_"></span><span id="results_using_the_acpi_notify_inc_brightness_hotkey_notification_"></span><span id="RESULTS_USING_THE_ACPI_NOTIFY_INC_BRIGHTNESS_HOTKEY_NOTIFICATION_"></span>ACPI を使用して結果を\_通知\_INC\_明るさ\_ホットキー通知。  
        1, 10, 15, 20, 25, 30, 35, 40, 45, 50, 55, 60, 65, 70, 75, 80, 85, 90, 95, 100

        <span id="Results_using_the_ACPI_NOTIFY_DEC_BRIGHTNESS_HOTKEY_notification_"></span><span id="results_using_the_acpi_notify_dec_brightness_hotkey_notification_"></span><span id="RESULTS_USING_THE_ACPI_NOTIFY_DEC_BRIGHTNESS_HOTKEY_NOTIFICATION_"></span>ACPI を使用して結果を\_通知\_DEC\_明るさ\_ホットキー通知。  
        100, 95, 90, 85, 80, 75, 70, 65, 60, 55, 50, 45, 40, 35, 30, 25, 20, 15, 10, 5, 1

    場合でも、5 の以前の値と異なる割合ユニットを 5 未満の場合は、ドライバーが 1 に輝度レベルを設定するため、後者の例では、1、最後の使用可能な値です。

    DWORD の値を変更することで、この既定のモニター ドライバーの動作をオーバーライドできます。 **MinimumStepPercentage**で次のレジストリ キー。

    `HKEY_LOCAL_MACHINE\ SYSTEM\ CurrentControlSet\ Services\` *モニター*`\ Parameters\`

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[出力を表示し、ACPI イベントをサポートしています。](supporting-display-output.md)

 

 






