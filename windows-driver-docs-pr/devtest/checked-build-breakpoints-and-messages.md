---
title: チェック ビルドのブレークポイントとメッセージ
description: チェック ビルドのブレークポイントとメッセージ
ms.assetid: 99b27487-eb95-4303-bad6-0b7ed8b450f0
keywords:
- WDK のブレークポイント
- チェック ビルド WDK、ブレークポイント
- チェック ビルド WDK、メッセージ
- WDK のメッセージがビルドを確認
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e9cf50cc13e9ae0e5f936a9a98b5d1385e8fae3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360388"
---
# <a name="checked-build-breakpoints-and-messages"></a>チェック ビルドのブレークポイントとメッセージ


## <span id="ddk_checked_build_breakpoints_and_messages_tools"></span><span id="DDK_CHECKED_BUILD_BREAKPOINTS_AND_MESSAGES_TOOLS"></span>


このトピックでは説明の一覧と一般的なブレークポイントのいくつか説明し、 [**による DbgPrint** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-dbgprint)ドライバーは、チェックのビルドで発生可能性のあるメッセージ。

<span id="____DPC_routine___1_sec_---_This_is_not_a_break_in_KeUpdateSystemTime"></span><span id="____dpc_routine___1_sec_---_this_is_not_a_break_in_keupdatesystemtime"></span><span id="____DPC_ROUTINE___1_SEC_---_THIS_IS_NOT_A_BREAK_IN_KEUPDATESYSTEMTIME"></span> **\*\*\* DPC ルーチン&gt;1 秒---これは KeUpdateSystemTime の中断ではありません**  
ブレークポイントを発行する前に、このメッセージが表示されます。 これは、アクティブなドライバーが DPC ルーチンで 1 秒以上に費やされたことを示します。

<span id="____isr_at_0x_________________nnnnnnnn_________________took_over_.5_second"></span><span id="____ISR_AT_0X_________________NNNNNNNN_________________TOOK_OVER_.5_SECOND"></span> **\*\*\* 0 x で ISR** *nnnnnnnn* **.5 秒以上かかりました**  
ブレークポイントを発行する前に、このメッセージが表示されます。 示して割り込みサービス ルーチンとエントリ ポイント 0 x*nnnnnnnn* 500 ミリ秒以上を実行します。

<span id="IOINIT__Built-in_driver__________________xxxxxx_________________failed_to_initialize___0xnnnnnnnn"></span><span id="ioinit__built-in_driver__________________xxxxxx_________________failed_to_initialize___0xnnnnnnnn"></span><span id="IOINIT__BUILT-IN_DRIVER__________________XXXXXX_________________FAILED_TO_INITIALIZE___0XNNNNNNNN"></span>**IOINIT:組み込みのドライバー** *xxxxxx*  **− 0 の初期化に失敗しました x * * * この nnnnnnnn*ブート開始ドライバーの名前付き*xxxxxx*エラー状態が返されました0 x*nnnnnnnn * からその**DriverEntry**エントリ ポイント。

<span id="IOINIT__Built-in_driver__________________xxxxxx_________________took__________________y.z________________s_to_initialize"></span><span id="ioinit__built-in_driver__________________xxxxxx_________________took__________________y.z________________s_to_initialize"></span><span id="IOINIT__BUILT-IN_DRIVER__________________XXXXXX_________________TOOK__________________Y.Z________________S_TO_INITIALIZE"></span>**IOINIT:組み込みのドライバー** *xxxxxx* **かかりました** *y.z* **を初期化します。**  
ブート開始ドライバーの名前付き*xxxxxx*に対して実行される*y.z*秒 (これは 5 秒間の予想最大時間より長い) でその**DriverEntry**エントリ ポイント。

<span id="IOINIT__Built-in_driver__________________xxxxxx_________________took__________________y.z________________s_to_fail_initialization"></span><span id="ioinit__built-in_driver__________________xxxxxx_________________took__________________y.z________________s_to_fail_initialization"></span><span id="IOINIT__BUILT-IN_DRIVER__________________XXXXXX_________________TOOK__________________Y.Z________________S_TO_FAIL_INITIALIZATION"></span>**IOINIT:組み込みのドライバー** *xxxxxx* **かかりました** *y.z* **の初期化に失敗します。**  
ブート開始ドライバーの名前付き*xxxxxx*に対して実行される*y.z*秒 (これは 5 秒間の予想最大時間より長い) でその**DriverEntry**エントリ ポイント。

<span id="ioload__driver__________________xxxxxx_________________took__________________y.z________________s_to_initialize"></span><span id="IOLOAD__DRIVER__________________XXXXXX_________________TOOK__________________Y.Z________________S_TO_INITIALIZE"></span>**IOLOAD:ドライバー** *xxxxxx* **かかりました** *y.z* **を初期化します。**  
という名前のドライバー *xxxxxx*に対して実行される*y.z*秒 (これは 5 秒間の予想最大時間より長い) でその**DriverEntry**エントリ ポイント。

<span id="ioload__driver__________________xxxxxx_________________took__________________y.z________________s_to_fail_initialization"></span><span id="IOLOAD__DRIVER__________________XXXXXX_________________TOOK__________________Y.Z________________S_TO_FAIL_INITIALIZATION"></span>**IOLOAD:ドライバー** *xxxxxx* **かかりました** *y.z* **の初期化に失敗します。**  
という名前のドライバー *xxxxxx*に対して実行される*y.z*秒 (これは 5 秒間の予想最大時間より長い) でその**DriverEntry**エントリ ポイント。

<span id="IopLoadDriver__A_PnP_driver__________________xxxxxx_________________does_not_support_DriverUnload_routine"></span><span id="ioploaddriver__a_pnp_driver__________________xxxxxx_________________does_not_support_driverunload_routine"></span><span id="IOPLOADDRIVER__A_PNP_DRIVER__________________XXXXXX_________________DOES_NOT_SUPPORT_DRIVERUNLOAD_ROUTINE"></span>**IopLoadDriver:PnP ドライバー** *xxxxxx* **DriverUnload ルーチンをサポートしていません**  
という名前のドライバー *xxxxxx* IRP をサポートしている\_MJ\_PNP、アンロード ルーチンが指定されませんでしたが、 **DriverEntry**します。

<span id="DO_DEVICE_INITIALIZING_flag_not_cleared_on_DO_0x_________________nnnnnnnn"></span><span id="do_device_initializing_flag_not_cleared_on_do_0x_________________nnnnnnnn"></span><span id="DO_DEVICE_INITIALIZING_FLAG_NOT_CLEARED_ON_DO_0X_________________NNNNNNNN"></span> **\_デバイス\_初期化フラグをオフには 0 x** *nnnnnnnn*  
デバイス オブジェクトのアドレス 0 x*nnnnnnnn*の外部で作成された**DriverEntry**、しかし、\_デバイス\_ビットを初期化していますが、システムに返す前にクリアされていません。

 

 





