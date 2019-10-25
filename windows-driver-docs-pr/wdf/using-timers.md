---
title: タイマーの使用
description: フレームワークの組み込みタイマーサポートの使用方法について説明します。 KMDF ドライバーと、バージョン2以降の UMDF ドライバーの両方に適用されます。
ms.assetid: f3bca5bf-fa5f-4b8f-ad28-26d29fc33963
keywords:
- タイマー WDK KMDF
- フレームワークオブジェクト WDK KMDF、タイマーオブジェクト
- タイマーオブジェクト WDK KMDF
- 定期的なタイマー WDK KMDF
- タイマーの停止 WDK KMDF
- タイマー WDK KMDF の開始
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61c1c5d86da34e4d1055eeb40facb7e408bc9327
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845421"
---
# <a name="using-timers"></a>タイマーの使用


このトピックでは、フレームワークの組み込みタイマーサポートの使用方法について説明します。 これは、カーネルモードドライバーフレームワーク (KMDF) ドライバーだけでなく、バージョン2以降のユーザーモードドライバーフレームワーク (UMDF) ドライバーにも適用されます。

フレームワークには、ドライバーがタイマーを作成できるようにする*タイマーオブジェクト*が用意されています。 ドライバーがタイマーオブジェクトを作成し、タイマーのクロックを開始した後、指定した時間が経過すると、フレームワークはドライバーが提供するコールバック関数を呼び出します。 必要に応じて、指定した時間が経過するたびに、フレームワークがコールバック関数を繰り返し呼び出すように、ドライバーがタイマーを設定できます。

フレームワークタイマーオブジェクトを作成するには、ドライバーが[**Wdftimercreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdftimer/nf-wdftimer-wdftimercreate)メソッドを呼び出す必要があります。 このメソッドは、 [*Evttimerfunc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdftimer/nc-wdftimer-evt_wdf_timer)コールバック関数と定期的な時間間隔を登録します。 フレームワークがコールバック関数を1回だけ呼び出すようにする場合、ドライバーは定期的な時間間隔に0を指定します。

通常は、デバイスごとにドライバーが必要とするタイマーの数がわかります。 そのため、ドライバーは、 [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数で[**wdftimercreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdftimer/nf-wdftimer-wdftimercreate)を呼び出してタイマーオブジェクトを作成できます。また、タイマーオブジェクトハンドルをデバイスまたはキューオブジェクトの[コンテキスト空間](framework-object-context-space.md)に格納できます。

タイマーを開始するために、ドライバーは[**Wdftimerstart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdftimer/nf-wdftimer-wdftimerstart)を呼び出し、"期限" を渡します。 フレームワークはタイマーのクロックを開始し、指定された時間が経過すると[*Evttimerfunc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdftimer/nc-wdftimer-evt_wdf_timer) callback 関数を呼び出します。

ドライバーが[**Wdftimercreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdftimer/nf-wdftimer-wdftimercreate)という周期的な時間間隔を指定した場合、タイマーは周期的な*タイマー*と呼ばれます。 周期的なタイマーのクロックは、最初の "期限切れ" が経過した後も引き続き実行されます。また、定期的な時間間隔が経過するたびに、フレームワークがドライバーのコールバック関数を繰り返し呼び出します。 定期的なタイマーは自動的に開始されません。 周期的でないタイマーと同様に、ドライバーは最初にタイマーを作成した後も[**Wdftimerstart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdftimer/nf-wdftimer-wdftimerstart)を呼び出す必要があります。

ドライバーは、期限切れになったときに非定期的タイマーを再開するために、 [*Evttimerfunc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdftimer/nc-wdftimer-evt_wdf_timer) callback 関数から[**Wdftimerstart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdftimer/nf-wdftimer-wdftimerstart)を呼び出すことができます。

タイマーを停止するために、ドライバーは[**Wdftimerstop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdftimer/nf-wdftimer-wdftimerstop)を呼び出すことができます。 ドライバーは、開始と停止によって、タイマーを繰り返し再利用できます。

ドライバーがタイマーオブジェクトを作成するときは、親オブジェクトを指定する必要があります。 フレームワークはタイマーを停止し、親が削除されるとタイマーオブジェクトを削除します。 タイマーオブジェクトの親オブジェクトを取得するために、ドライバーは[**WdfTimerGetParentObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdftimer/nf-wdftimer-wdftimergetparentobject)を呼び出すことができます。

バージョン1.9 より前の KMDF バージョンでは、すべてのドライバーのコールバック関数を IRQL = パッシブ\_レベルで実行する場合、タイマーオブジェクトを簡単に使用することはできません。 このフレームワークは、IRQL = ディスパッチ\_レベルで呼び出される遅延プロシージャ呼び出し (DPC) として、タイマーオブジェクトの[*Evttimerfunc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdftimer/nc-wdftimer-evt_wdf_timer)コールバック関数を実装します。 したがって、タイマーの有効期限コードをパッシブ\_レベルで実行する場合、 *Evttimerfunc*コールバック関数は、パッシブ\_レベルで実行される[作業項目](using-framework-work-items.md)をキューに挿入する必要があります。

KMDF バージョン1.9 以降では、パッシブ\_レベルで実行されるタイマーである*パッシブレベルのタイマー*を作成できます。 パッシブレベルのタイマーを作成するには、ドライバーが[**Wdftimercreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdftimer/nf-wdftimer-wdftimercreate)を呼び出すときに、 [**Wdfexecutionlevelpassive**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ne-wdfobject-_wdf_execution_level)実行レベルを指定します。 その結果、フレームワークは、受動的\_レベルで実行される作業項目として、 [*Evttimerfunc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdftimer/nc-wdftimer-evt_wdf_timer)コールバック関数を実装します。 パッシブレベルのタイマーを定期的なタイマーにすることはできません。

UMDF バージョン2.0 以降では、フレームワークは、ユーザーモードスレッドプールからのワーカースレッドとしてタイマーオブジェクトの[*Evttimerfunc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdftimer/nc-wdftimer-evt_wdf_timer)コールバック関数を実装します。 その結果、UMDF ドライバーのタイマーコールバック関数は、常にパッシブ\_レベルで実行されます。

## <a name="no-wake-timers"></a>ウェイクタイマーがありません


システムの電力効率は、システムが低電力状態から再開するタイマーによって軽減されます。 バッテリ寿命を向上させる方法の1つは、システムをスリープ解除するのではなく、重要でない定期的な操作を遅延させることです。 Windows 8.1 以降では、 *wake タイマーを使用せず*に、kmdf ドライバーまたは UMDF ドライバーでこのような非クリティカル操作を実行できます。 No wake timer は、システムが低電力状態のときに有効期限が切れた場合にシステムをスリープ解除しません。 代わりに、このフレームワークは、次回システムが S0 に完全に達したときに、ドライバーの[*Evttimerfunc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdftimer/nc-wdftimer-evt_wdf_timer)コールバック関数を呼び出します。

KMDF バージョン1.13 と UMDF バージョン2.0 以降では、ウェイクタイマーを使用できません。

Wake タイマーを作成しない場合は、 [**WDF\_timer\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdftimer/ns-wdftimer-_wdf_timer_config)の**TolerableDelay**メンバーを**TolerableDelayUnlimited**に設定します。

ウェイクタイマーの詳細については、「[ウェイクアップタイマー](https://docs.microsoft.com/windows-hardware/drivers/kernel/no-wake-timers)を使用しない」を参照してください。

## <a name="high-resolution-timers"></a>高解像度タイマー


標準フレームワークタイマーの精度は、システムクロックのティック間隔と一致します。これは、既定では15.6 ミリ秒です。 Windows 8.1 から、*高解像度タイマー*を作成できます。 高解像度タイマーの精度は1ミリ秒です。 正確で予測可能な有効期限が必要な重要な操作に対しては、高解像度タイマーを使用できます。 頻繁に必要となるサービスの結果として、高解像度タイマーによってバッテリの寿命が低下する可能性があります。

高解像度タイマーは kmdf ドライバーでのみ使用できます KMDF バージョン1.13 以降。

高解像度タイマーを作成するには、 [**WDF\_timer\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdftimer/ns-wdftimer-_wdf_timer_config)の**usehighresolution タイマー**メンバーを**wdftrue**に設定し、 **[期間]** の値を目的の解像度に調整します。

次の表に、ドライバーが**ピリオド**に提供するさまざまな値に基づいたタイマーの動作の例を示します。 これらの例では、システムクロックティックの間隔が15ミリ秒であることを前提としています。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">期間 (ミリ秒)</th>
<th align="left">標準タイマー</th>
<th align="left">高解像度タイマー</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>10</p></td>
<td align="left"><p>タイマーの有効期限は0ミリ秒から25ミリ秒です。</p></td>
<td align="left"><p>タイマーは、可能な限り10ミリ秒後に期限切れになります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>16</p></td>
<td align="left"><p>タイマーの有効期限は15ミリ秒から30ミリ秒です。</p></td>
<td align="left"><p>タイマーは、可能な限り16ミリ秒後に期限切れになります。</p></td>
</tr>
</tbody>
</table>

 

高解像度タイマーの詳細については、「[高解像度タイマー](https://docs.microsoft.com/windows-hardware/drivers/kernel/high-resolution-timers)」を参照してください。

タイマー精度をシステムクロックの粒度に関連付ける方法の詳細については、「[タイマー精度](https://docs.microsoft.com/windows-hardware/drivers/kernel/timer-accuracy)」を参照してください。

 

 





