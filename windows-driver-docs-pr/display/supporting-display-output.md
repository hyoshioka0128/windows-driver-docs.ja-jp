---
title: ディスプレイ出力および ACPI イベントのサポート
description: システム構成とデバイス電源管理の包括的なアプローチは、ACPI 仕様に基づき、Windows に組み込まれています。
ms.assetid: CD5BC59A-4C15-4111-BF4F-13DC04F6874F
keywords:
- ACPI 表示 WDK ディスプレイ
- ACPI ベースのディスプレイホットキー WDK ディスプレイ
- ホットキー WDK 表示の表示
- BIOS 表示コントロール WDK 表示
- 自動表示スイッチ WDK 表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac923e73d8aa7f13a69a59a9c0f2ee6982743fb5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825628"
---
# <a name="supporting-display-output-and-acpi-events"></a>ディスプレイ出力および ACPI イベントのサポート


システム構成とデバイス電源管理の包括的なアプローチは、Advanced Configuration and Power Interface (ACPI) 仕様に基づいて、Windows に組み込まれています。 Windows では、ドライバーが出力デバイスを表示する構成と機能を管理するために使用できる機能をサポートしています。 詳細については、 [acpi web サイト](https://go.microsoft.com/fwlink/p/?linkid=57185)の acpi 仕様を参照してください。

## <a name="span-idbios_requirements_to_support_display_output_devicesspanspan-idbios_requirements_to_support_display_output_devicesspanspan-idbios_requirements_to_support_display_output_devicesspanbios-requirements-to-support-display-output-devices"></a><span id="BIOS_Requirements_to_Support_Display_Output_Devices"></span><span id="bios_requirements_to_support_display_output_devices"></span><span id="BIOS_REQUIREMENTS_TO_SUPPORT_DISPLAY_OUTPUT_DEVICES"></span>出力デバイスの表示をサポートする BIOS 要件


システム BIOS によって公開されている表示ミニポートドライバーまたは ACPI メソッドは、出力デバイス構成を表示します。 [**DxgkDdiNotifyAcpiEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_notify_acpi_event)関数は、ACPI イベントに関するミニポートドライバーをディスプレイに通知するために呼び出されます。 たとえば、ユーザーが出力デバイススイッチのキーボードショートカットを押すと、 **DxgkDdiNotifyAcpiEvent**関数は、ACPI\_通知\_サイクル\_\_のホットキー通知と要求の種類の DXGK に表示されます。\_ACPI\_変更\_\_モードを表示します。 その結果、オペレーティングシステムは、 [**DxgkDdiRecommendFunctionalVidPn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendfunctionalvidpn)関数を呼び出して、選択した表示出力デバイスを照会します。

ACPI 表示出力の次のエイリアスは、「Dispmprt. h」で定義されています。

-   ACPI\_方法\_\_DOD-ディスプレイアダプターに接続されているすべてのデバイスを列挙します。 統合コントローラーで出力デバイスの切り替えがサポートされている場合は、この方法が必要です。 これは、ACPI 仕様で定義されている DOD\_ メソッドのエイリアス名です。
-   ACPI\_メソッド\_表示\_DOS-システムファームウェアがアクティブな表示出力を自動的に切り替えることができることを示します。 これは、ACPI 仕様で定義されている SOD\_ メソッドのエイリアス名です。 次に、許可されるパラメーターを示します。
    -   ACPI\_ARG\_\_スイッチ\_イベントを有効にします。 システムファームウェアがアクティブな表示出力デバイスを自動的に切り替えることができないことを示します。 代わりに、それぞれの表示出力デバイスに関連付けられている状態変数に必要な変更を保存し、表示スイッチイベントを生成する必要があります。 オペレーティングシステムは、配布の\_DG メソッド\_出力する ACPI\_メソッドを呼び出すことによって、デバイスのアクティブな状態を照会できます。
    -   ACPI\_ARG\_\_自動\_スイッチを有効にします。 システムファームウェアがオペレーティングシステムと対話することなく、アクティブな表示出力デバイスを自動的に切り替える必要があることを示します。 表示スイッチイベントは生成されません。
    -   ACPI\_ARG\_\_スイッチ\_イベントを無効にします。 システムファームウェアが何の操作も実行してはいけないことを示します。つまり、出力デバイスを切り替えたり、オペレーティングシステムに通知したりすることはありません。 ACPI\_メソッド\_出力\_DG メソッドによって返された値はロックされています。
-   ACPI\_方法\_出力\_DC-表示出力デバイスの状態を返します。 これは、ACPI 仕様で定義されている CSD\_ メソッドのエイリアス名です。
-   ACPI\_方法\_出力\_DG-表示出力デバイスの状態がアクティブかどうかを確認します。 これは、ACPI 仕様で定義されている SGD\_ メソッドのエイリアス名です。
-   ACPI\_方法\_出力\_DSS-ディスプレイ出力デバイスの状態をアクティブまたは非アクティブに設定します。 これは、ACPI 仕様で定義されている SSD\_ メソッドのエイリアス名です。 この操作は、オペレーティングシステムによって管理され、ちらつきを回避します。
-   ACPI\_方法\_表示\_GPD-ブート時にどのビデオデバイスがポストされるかを判断するために、CMOS エントリを照会します。 これは、ACPI 仕様で定義されている DPG\_ メソッドのエイリアス名です。
-   ACPI\_方法\_表示\_SPD-起動時にどのビデオデバイスがポストされるかを決定する CMOS エントリを更新します。 これは、ACPI 仕様で定義されている DPS\_ メソッドのエイリアス名です。
-   ACPI\_METHOD\_DISPLAY\_VPO-実装されているビデオオプションを決定します。 これは、ACPI 仕様で定義されている OPV\_ メソッドのエイリアス名です。

## <a name="span-idexternal_asynchronous_eventsspanspan-idexternal_asynchronous_eventsspanspan-idexternal_asynchronous_eventsspanexternal-asynchronous-events"></a><span id="External_Asynchronous_Events"></span><span id="external_asynchronous_events"></span><span id="EXTERNAL_ASYNCHRONOUS_EVENTS"></span>外部非同期イベント


オペレーティングシステムは、出力デバイスの表示に影響する外部の非同期イベントについて通知を受ける必要があります。 次の通知および関連する要求の種類は、 [**DxgkDdiNotifyAcpiEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_notify_acpi_event)関数で定義されています。

-   ACPI\_通知\_サイクル\_表示\_ホットキー-ユーザーが サイクル表示のショートカットキーを押したことをオペレーティングシステムに通知します。
-   ACPI\_通知\_次の\_表示\_ホットキー-ユーザーが次の表示のショートカットキーを押したことをオペレーティングシステムに通知します。
-   ACPI\_通知\_前\_表示\_ホットキー-ユーザーが前の表示のキーボードショートカットを押したことをオペレーティングシステムに通知します。

**メモ** 以前の通知は、ユーザーがキーボードショートカットを押したときに発生したイベントの処理に依存しています。

 

ディスプレイミニポートドライバーがオペレーティングシステムに対して行うことができる要求の種類を次に示します。

-   DXGK\_ACPI\_変更\_表示\_モード-新しい推奨されるアクティブなビデオの現在のネットワーク (VidPN) にモード変更を開始する要求。
-   DXGK\_ACPI\_ポーリング\_表示アダプターの子の接続をポーリングする\_の子要求を表示します。

**メモ** 前の要求は、 [**DxgkDdiNotifyAcpiEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_notify_acpi_event)関数によって返される*AcpiFlags*パラメーターの値です。

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[統合された表示パネルでの明るさコントロールのサポート](supporting-brightness-controls-on-integrated-display-panels.md)

 

 






