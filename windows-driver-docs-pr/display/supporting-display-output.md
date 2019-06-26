---
title: ディスプレイ出力および ACPI イベントのサポート
description: システム構成とデバイスの電源管理に包括的なアプローチは、ACPI の仕様に基づき、Windows に組み込まれます。
ms.assetid: CD5BC59A-4C15-4111-BF4F-13DC04F6874F
keywords:
- ACPI は、WDK の表示を表示します。
- ACPI ベースの表示のホット キー WDK の表示
- ホット キーの WDK を表示します。
- BIOS は、WDK を表示するコントロールを表示します。
- スイッチの自動表示 WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 582c40ac08c11be025d8acce0fefec233656a215
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355539"
---
# <a name="supporting-display-output-and-acpi-events"></a>ディスプレイ出力および ACPI イベントのサポート


システム構成とデバイスの電源管理に包括的なアプローチは、Advanced Configuration and Power Interface (ACPI) の仕様に基づき、Windows に組み込まれます。 Windows では、ドライバーでの構成と表示の出力デバイスの電源管理に使用できる機能をサポートします。 詳細については、上、ACPI 仕様を参照してください。、 [ACPI の web サイト](https://go.microsoft.com/fwlink/p/?linkid=57185)します。

## <a name="span-idbiosrequirementstosupportdisplayoutputdevicesspanspan-idbiosrequirementstosupportdisplayoutputdevicesspanspan-idbiosrequirementstosupportdisplayoutputdevicesspanbios-requirements-to-support-display-output-devices"></a><span id="BIOS_Requirements_to_Support_Display_Output_Devices"></span><span id="bios_requirements_to_support_display_output_devices"></span><span id="BIOS_REQUIREMENTS_TO_SUPPORT_DISPLAY_OUTPUT_DEVICES"></span>ディスプレイ デバイスの出力をサポートするための BIOS 要件


ディスプレイのミニポート ドライバーまたはシステム BIOS サポート表示出力デバイス構成によって公開されている ACPI メソッド。 [ **DxgkDdiNotifyAcpiEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_notify_acpi_event) ACPI イベントに関するディスプレイ ミニポート ドライバーに通知する関数が呼び出されます。 出力デバイス スイッチに、ユーザーがキーボード ショートカットを押したときになど、 **DxgkDdiNotifyAcpiEvent**関数を呼び出すと ACPI\_通知\_サイクル\_表示\_DXGK のホットキー通知と、要求が入力\_ACPI\_変更\_表示\_モード。 その結果、オペレーティング システムの呼び出し、 [ **DxgkDdiRecommendFunctionalVidPn** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendfunctionalvidpn)出力デバイスを選択した表示のクエリを実行する関数。

Dispmprt.h では、ACPI 表示出力には、次のエイリアスが定義されています。

-   ACPI\_メソッド\_表示\_DOD - ディスプレイ アダプターにアタッチされているすべてのデバイスを列挙します。 統合されたコント ローラーは、出力デバイスの切り替えをサポートしている場合、このメソッドが必要です。 これは、DOD のエイリアス名\_ACPI 仕様によって定義されるメソッド。
-   ACPI\_メソッド\_表示\_DOS - は、システム ファームウェアが自動的にアクティブな表示出力を切り替え可能なであることを示します。 これは、SOD のエイリアス名\_ACPI 仕様によって定義されるメソッド。 許可されているパラメーターを次に示します。
    -   ACPI\_ARG\_を有効にする\_スイッチ\_イベント。 システム ファームウェア切り替える必要がありますいない自動的にアクティブな状態では、出力デバイスを表示します。 代わりに、各ディスプレイ出力デバイスに関連付けられている状態変数に、必要な変更を保存し、表示の切り替えイベントの生成にする必要があります。 オペレーティング システムは、ACPI を呼び出すことによって、デバイスのアクティブな状態を照会できます\_メソッド\_出力\_DG メソッド。
    -   ACPI\_ARG\_を有効にする\_自動\_スイッチ。 システム ファームウェアが、アクティブなを自動的に切り替える必要がある状態は、オペレーティング システムと対話することがなく、出力デバイスを表示します。 表示の切り替えイベントは生成されません。
    -   ACPI\_ARG\_を無効にする\_スイッチ\_イベント。 状態システム ファームウェアには、任意のアクションは実行しないでください。つまり、出力デバイスを切り替えるもオペレーティング システムに通知します。 ACPI によって返される値\_メソッド\_出力\_DG メソッドはロックされています。
-   ACPI\_メソッド\_出力\_DC のディスプレイの状態を取得する出力デバイス。 これは、CSD のエイリアス名\_ACPI 仕様によって定義されるメソッド。
-   ACPI\_メソッド\_出力\_DG のディスプレイの状態を出力デバイスがアクティブかどうかを確認します。 これは、SGD のエイリアス名\_ACPI 仕様によって定義されるメソッド。
-   ACPI\_メソッド\_出力\_DSS - 設定の表示状態の出力デバイス アクティブまたは非アクティブにします。 これは、SSD のエイリアス名\_ACPI 仕様によって定義されるメソッド。 オペレーティング システムでは、ちらつきを回避するには、この操作を管理します。
-   ACPI\_メソッド\_表示\_GPD - ビデオ デバイスがブート時に投稿を判断するのには、CMOS エントリを照会します。 これは、DPG のエイリアス名\_ACPI 仕様によって定義されるメソッド。
-   ACPI\_メソッド\_表示\_SPD - は、ビデオ デバイスがブート時に投稿を決定する CMOS エントリを更新します。 これは、DPS のエイリアス名\_ACPI 仕様によって定義されるメソッド。
-   ACPI\_メソッド\_表示\_VPO - どのようなビデオのオプションの実装を決定します。 これは、OPV のエイリアス名\_ACPI 仕様によって定義されるメソッド。

## <a name="span-idexternalasynchronouseventsspanspan-idexternalasynchronouseventsspanspan-idexternalasynchronouseventsspanexternal-asynchronous-events"></a><span id="External_Asynchronous_Events"></span><span id="external_asynchronous_events"></span><span id="EXTERNAL_ASYNCHRONOUS_EVENTS"></span>外部の非同期イベント


オペレーティング システムは、表示の出力デバイスに影響する外部の非同期のイベントについて通知する必要があります。 次の通知と関連する要求の種類が Dispmprt.h で定義されているし、で使用される、 [ **DxgkDdiNotifyAcpiEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_notify_acpi_event)関数。

-   ACPI\_通知\_サイクル\_表示\_ホットキー - は、ユーザーのサイクルの表示のキーボード ショートカットが押されたことをオペレーティング システムに通知します。
-   ACPI\_通知\_次\_表示\_ホットキー - は、ユーザーが次の表示のキーボード ショートカットを押されたことをオペレーティング システムに通知します。
-   ACPI\_通知\_PREV\_表示\_ホットキー - は、ユーザーが以前表示のキーボード ショートカットを押されたことをオペレーティング システムに通知します。

**注**前の通知は、キーボード ショートカット キーを押すと、ユーザーによるイベントの処理に依存します。

 

ディスプレイのミニポート ドライバーがオペレーティング システムに加えることが要求の種類を次に示します。

-   DXGK\_ACPI\_変更\_表示\_モード - 要求モードを開始する変更を新しいアクティブなビデオ存在するネットワーク (VidPN) をお勧めします。
-   DXGK\_ACPI\_ポーリング\_表示\_ディスプレイ アダプターの子の接続をポーリングする要求の子。

**注**、以前の要求の値、 *AcpiFlags*パラメーターによって返される、 [ **DxgkDdiNotifyAcpiEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_notify_acpi_event)関数。

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[パネルの統合ディスプレイの明るさコントロールをサポート](supporting-brightness-controls-on-integrated-display-panels.md)

 

 






