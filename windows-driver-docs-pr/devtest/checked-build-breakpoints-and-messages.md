---
title: チェック ビルドのブレークポイントとメッセージ
description: チェック ビルドのブレークポイントとメッセージ
ms.assetid: 99b27487-eb95-4303-bad6-0b7ed8b450f0
keywords:
- ブレークポイント WDK
- チェック済みビルド WDK、ブレークポイント
- チェックされたビルドの WDK、メッセージ
- メッセージ WDK チェック済みビルド
ms.date: 05/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 2f8118d259fffafa86817341656020af2167df4a
ms.sourcegitcommit: 076f9cd83313f6d8ab5688340f05bde7e8fbb8ee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2020
ms.locfileid: "82999073"
---
# <a name="checked-build-breakpoints-and-messages"></a>チェック ビルドのブレークポイントとメッセージ

## <span id="ddk_checked_build_breakpoints_and_messages_tools"></span><span id="DDK_CHECKED_BUILD_BREAKPOINTS_AND_MESSAGES_TOOLS"></span>

このトピックでは、チェックされたビルドでドライバーが発生する可能性のある一般的なブレークポイントと[**Dbgprint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgprint)メッセージの一覧と説明を示します。

> [!NOTE]
> チェックを行ったビルドは、Windows 10 バージョン1803より前の古いバージョンの Windows で使用できました。
> Driver Verifier や GFlags などのツールを使用して、新しいバージョンの Windows でドライバーコードを確認します。

<span id="____DPC_routine___1_sec_---_This_is_not_a_break_in_KeUpdateSystemTime"></span><span id="____dpc_routine___1_sec_---_this_is_not_a_break_in_keupdatesystemtime"></span><span id="____DPC_ROUTINE___1_SEC_---_THIS_IS_NOT_A_BREAK_IN_KEUPDATESYSTEMTIME"></span>**\*\*\*DPC ルーチン&gt; 1 秒---これは KeUpdateSystemTime では中断されません。**  
このメッセージは、ブレークポイントが発行される直前に表示されます。 これは、アクティブなドライバーが DPC ルーチンで1秒以上費やされたことを示します。

<span id="____isr_at_0x_________________nnnnnnnn_________________took_over_.5_second"></span><span id="____ISR_AT_0X_________________NNNNNNNN_________________TOOK_OVER_.5_SECOND"></span>0x nnnnnnnn *nnnnnnnn* **の ISR は、約5秒を超え\* \* \* **ました**took over .5 second**  
このメッセージは、ブレークポイントが発行される直前に表示されます。 これは、エントリポイント 0x*nnnnnnnn*を持つ割り込みサービスルーチンが500ミリ秒を超えて実行されたことを示します。

<span id="IOINIT__Built-in_driver__________________xxxxxx_________________failed_to_initialize___0xnnnnnnnn"></span><span id="ioinit__built-in_driver__________________xxxxxx_________________failed_to_initialize___0xnnnnnnnn"></span><span id="IOINIT__BUILT-IN_DRIVER__________________XXXXXX_________________FAILED_TO_INITIALIZE___0XNNNNNNNN"></span>**Ioinit: 組み込みドライバー** *xxxxxx*が**初期化に失敗しました。-0x * * * nnnnnnnn*のブート開始ドライバーが、 *xxxxxx* * **driverentry**エントリポイントからエラー状態 0x nnnnnnnn * を返しました。

<span id="IOINIT__Built-in_driver__________________xxxxxx_________________took__________________y.z________________s_to_initialize"></span><span id="ioinit__built-in_driver__________________xxxxxx_________________took__________________y.z________________s_to_initialize"></span><span id="IOINIT__BUILT-IN_DRIVER__________________XXXXXX_________________TOOK__________________Y.Z________________S_TO_INITIALIZE"></span>**Ioinit: 組み込みドライバー** *xxxxxx*は、**初期化に** *y. z* s を**要し**ました  
**Driverentry**エントリポイントで、 *xxxxxx*という名前のブート開始ドライバー (予想される最大5秒の時間を超える *) を実行*しました。

<span id="IOINIT__Built-in_driver__________________xxxxxx_________________took__________________y.z________________s_to_fail_initialization"></span><span id="ioinit__built-in_driver__________________xxxxxx_________________took__________________y.z________________s_to_fail_initialization"></span><span id="IOINIT__BUILT-IN_DRIVER__________________XXXXXX_________________TOOK__________________Y.Z________________S_TO_FAIL_INITIALIZATION"></span>**Ioinit: 組み込みドライバー** *xxxxxx* **took**で**初期化に失敗し**ました *。*  
**Driverentry**エントリポイントで、 *xxxxxx*という名前のブート開始ドライバー (予想される最大5秒の時間を超える *) を実行*しました。

<span id="ioload__driver__________________xxxxxx_________________took__________________y.z________________s_to_initialize"></span><span id="IOLOAD__DRIVER__________________XXXXXX_________________TOOK__________________Y.Z________________S_TO_INITIALIZE"></span>**Ioload: ドライバー** *xxxxxx* **が初期化に** *y. z* s を**要し**ました  
**Driverentry**エントリポイントで、 *xxxxxx*という名前のドライバー (予想最大5秒の時間を超える) が実行されました *。*

<span id="ioload__driver__________________xxxxxx_________________took__________________y.z________________s_to_fail_initialization"></span><span id="IOLOAD__DRIVER__________________XXXXXX_________________TOOK__________________Y.Z________________S_TO_FAIL_INITIALIZATION"></span>**Ioload: ドライバー**の*xxxxxx* **took**で**初期化に失敗し**ました *。*  
**Driverentry**エントリポイントで、 *xxxxxx*という名前のドライバー (予想最大5秒の時間を超える) が実行されました *。*

<span id="IopLoadDriver__A_PnP_driver__________________xxxxxx_________________does_not_support_DriverUnload_routine"></span><span id="ioploaddriver__a_pnp_driver__________________xxxxxx_________________does_not_support_driverunload_routine"></span><span id="IOPLOADDRIVER__A_PNP_DRIVER__________________XXXXXX_________________DOES_NOT_SUPPORT_DRIVERUNLOAD_ROUTINE"></span>**Ioiostream Add川: PnP ドライバー** *Xxxxxx* **は Driverunload ルーチンをサポートしていません**  
*Xxxxxx*という名前のドライバー\_は\_、IRP MJ PNP をサポートしていますが、 **driverentry**に unload ルーチンが指定されていません。

<span id="DO_DEVICE_INITIALIZING_flag_not_cleared_on_DO_0x_________________nnnnnnnn"></span><span id="do_device_initializing_flag_not_cleared_on_do_0x_________________nnnnnnnn"></span><span id="DO_DEVICE_INITIALIZING_FLAG_NOT_CLEARED_ON_DO_0X_________________NNNNNNNN"></span>**Do\_0x\_nnnnnnnn でデバイス初期化フラグがクリアされていません** *nnnnnnnn*  
アドレス 0x*nnnnnnnn*のデバイスオブジェクトが**driverentry**の外部で作成されました\_が\_、システムに戻る前にデバイスの初期化ビットがクリアされませんでした。

 

 





