---
title: タイマーの使用
description: 組み込みのタイマーのフレームワークのサポートを使用する方法について説明します。 KMDF ドライバーとバージョン 2 で UMDF ドライバーの両方に適用されます。
ms.assetid: f3bca5bf-fa5f-4b8f-ad28-26d29fc33963
keywords:
- WDK KMDF のタイマー
- フレームワークは、WDK KMDF、タイマー オブジェクトをオブジェクトします。
- WDK KMDF のタイマー オブジェクト
- 定期的なタイマー WDK KMDF
- WDK KMDF のタイマーを停止しています
- WDK KMDF のタイマーを開始
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5cf0c9c4928c2a179bfb3e4d16d09acd4071a0b2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372177"
---
# <a name="using-timers"></a>タイマーの使用


このトピックでは、組み込みのタイマーのフレームワークのサポートを使用する方法について説明します。 カーネル モード ドライバー フレームワーク (KMDF) ドライバーとバージョン 2 でユーザー モード ドライバー フレームワーク (UMDF) ドライバーの両方に適用されます。

フレームワークを提供、*タイマー オブジェクト*タイマーを作成するドライバーを有効にします。 ドライバーは、タイマー オブジェクトを作成すると、タイマーのクロックを開始、フレームワークは、一定の時間が経過した後、ドライバーによって提供されるコールバック関数を呼び出します。 必要に応じて、ドライバーは、フレームワーク、コールバック関数を呼び出す、繰り返し一定の時間が経過するたびにできるように、タイマーを設定できます。

フレームワークのタイマー オブジェクトを作成するには、ドライバーを呼び出す必要があります、 [ **WdfTimerCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdftimer/nf-wdftimer-wdftimercreate)メソッド。 このメソッドは、登録、 [ *EvtTimerFunc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdftimer/nc-wdftimer-evt_wdf_timer)コールバック関数と、定期的な時間間隔。 コールバック関数を 1 回だけ呼び出すために、フレームワークを設定する場合、ドライバーに定期的な期間として 0 を指定します。

通常、各デバイスに必要なドライバーのタイマーの数がわかります。 そのため、ドライバーは、呼び出すことによってのタイマー オブジェクトを作成できます[ **WdfTimerCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdftimer/nf-wdftimer-wdftimercreate)でその[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数デバイスまたはキュー オブジェクトのタイマー オブジェクトのハンドルを格納、および[コンテキスト領域](framework-object-context-space.md)します。

タイマーをドライバーの呼び出しを開始する[ **WdfTimerStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdftimer/nf-wdftimer-wdftimerstart)、"due time"を渡します。 フレームワークは、タイマーのクロックと呼び出しを開始、 [ *EvtTimerFunc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdftimer/nc-wdftimer-evt_wdf_timer)一定の時間が経過すると、コールバック関数。

ドライバーでは、呼び出されたときに、定期的な期間が提供されるかどうか[ **WdfTimerCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdftimer/nf-wdftimer-wdftimercreate)、タイマーと呼ばれます、*定期的なタイマー*します。 定期的なタイマーのクロックが最初の実行が続行され「時間」の期限が経過すると、およびフレームワーク ドライバーのコールバック関数を呼び出す繰り返し、定期的な間隔が経過するたびにします。 定期的なタイマーは自動的に開始されません。 非定期的なタイマーは、のように、ドライバーは呼び出す必要がありますも[ **WdfTimerStart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdftimer/nf-wdftimer-wdftimerstart)初めて開始するタイマーを作成した後。

ドライバーが呼び出す可能性があります[ **WdfTimerStart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdftimer/nf-wdftimer-wdftimerstart)からその[ *EvtTimerFunc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdftimer/nc-wdftimer-evt_wdf_timer)後に非定期的なタイマーを再起動するためにコールバック関数有効期限が切れます。

ドライバーを呼び出すことができます、タイマーを停止する[ **WdfTimerStop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdftimer/nf-wdftimer-wdftimerstop)します。 ドライバーを起動して停止する繰り返しタイマーを再利用できます。

ドライバーは、タイマー オブジェクトを作成するときは、親オブジェクトを指定する必要があります。 フレームワークでは、タイマーを停止し、親が削除されたときに、タイマー オブジェクトを削除します。 タイマー オブジェクトの親オブジェクトを取得するには、ドライバーを呼び出すことができます[ **WdfTimerGetParentObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdftimer/nf-wdftimer-wdftimergetparentobject)します。

前のバージョン 1.9 KMDF バージョンでは、簡単に使用できませんタイマー オブジェクトすべてのドライバーのコールバック関数を IRQL で実行する場合 = パッシブ\_レベル。 タイマー オブジェクトの処理が実装されて[ *EvtTimerFunc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdftimer/nc-wdftimer-evt_wdf_timer)として遅延プロシージャ呼び出し (DPC) IRQL で呼び出されるコールバック関数のディスパッチを =\_レベル。 そのため、する場合はパッシブで実行するタイマーの有効期限コード\_レベル、 *EvtTimerFunc*コールバック関数がキューする必要があります、[作業項目](using-framework-work-items.md)パッシブに実行する\_レベル。

KMDF バージョン 1.9 以降では、作成することができます*パッシブ レベル タイマー*、これはパッシブで実行されるタイマー\_レベル。 パッシブ レベルのタイマーを作成するには、指定、 [ **WdfExecutionLevelPassive** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/ne-wdfobject-_wdf_execution_level)実行レベルには、ドライバーを呼び出すと[ **WdfTimerCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdftimer/nf-wdftimer-wdftimercreate). フレームワークを実装してその結果、 [ *EvtTimerFunc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdftimer/nc-wdftimer-evt_wdf_timer)コールバック関数のように作業項目をパッシブで実行される\_レベル。 定期的なタイマーをパッシブ レベルのタイマーができないことに注意してください。

UMDF バージョン 2.0 以降、フレームワークの実装、タイマー オブジェクトの[ *EvtTimerFunc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdftimer/nc-wdftimer-evt_wdf_timer)スレッド プールのユーザー モードからワーカー スレッドとしてコールバック関数。 UMDF ドライバーのタイマーのコールバック関数パッシブで常に実行結果として、\_レベル。

## <a name="no-wake-timers"></a>ウェイク アップ タイマー


システム電源効率が繰り返し発生する低電力状態から再開するシステム タイマーが減少します。 バッテリの寿命を向上させるために 1 つの方法では、システムをスリープ解除するのではなく、重要ではないの定期的な操作を遅延します。 使用できます Windows 8.1 以降、*ウェイク アップ タイマー* KMDF または UMDF ドライバーでこのような致命的でない操作を実行します。 なしのウェイク アップ タイマーは、システム スリープ解除しないシステムの低電力状態のときに有効期限が切れる場合。 代わりに、フレームワークが、ドライバーの[ *EvtTimerFunc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdftimer/nc-wdftimer-evt_wdf_timer)コールバック関数のシステムが完全に S0 状態で、[次へ] の時間。

ウェイク アップ タイマーは、KMDF バージョン 1.13 および UMDF バージョン 2.0 以降より使用可能ではありません。

なしのウェイク アップ タイマーを作成するには、設定、 **TolerableDelay**のメンバー [ **WDF\_タイマー\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdftimer/ns-wdftimer-_wdf_timer_config)に**TolerableDelayUnlimited**します。

ウェイク アップ タイマーの詳細については、次を参照してください。[いいえウェイク アップ タイマー](https://docs.microsoft.com/windows-hardware/drivers/kernel/no-wake-timers)します。

## <a name="high-resolution-timers"></a>高分解能タイマー


タイマーの標準フレームワークでは、システム クロックのティック間隔は 15.6 ミリ秒の既定値に一致する精度があります。 Windows 8.1 以降、作成*高分解能タイマー*します。 高解像度タイマーは、1 ミリ秒の精度を持ちます。 正確な予測可能な期限を必要とする重要な操作の高解像度タイマーを使用する可能性があります。 結果として、頻繁にサービスに必要なバッテリ寿命の短縮、高解像度タイマー可能性があります。

高分解能タイマーは、KMDF バージョン 1.13 以降、KMDF ドライバーでのみ可能です。

高解像度タイマーを作成するには、設定、 **UseHighResolutionTimer**のメンバー [ **WDF\_タイマー\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdftimer/ns-wdftimer-_wdf_timer_config)に**WdfTrue**、し、調整、**期間**を目的の解像度の値。

次の表は、ドライバーでは、別の値に基づいて、タイマーの動作の例を示します**期間**します。 これらの例では、システム クロックのティック間隔が 15 ミリ秒であると仮定します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">期間 (ミリ秒単位)</th>
<th align="left">標準的なタイマー</th>
<th align="left">高いタイマー精度</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>10</p></td>
<td align="left"><p>タイマーは、0 ミリ秒、25 ミリ秒の間で有効期限が切れます。</p></td>
<td align="left"><p>タイマーは、できるだけ 10 ミリ秒後すぐに有効期限です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>16</p></td>
<td align="left"><p>15 ミリ秒と 30 ミリ秒のタイマーが有効期限です。</p></td>
<td align="left"><p>タイマーは、できるだけ 16 ミリ秒後すぐに有効期限です。</p></td>
</tr>
</tbody>
</table>

 

高分解能タイマーの詳細については、次を参照してください。[高分解能タイマー](https://docs.microsoft.com/windows-hardware/drivers/kernel/high-resolution-timers)します。

タイマー精度が、システム クロックの粒度に関連する方法の詳細については、次を参照してください。[タイマー精度](https://docs.microsoft.com/windows-hardware/drivers/kernel/timer-accuracy)します。

 

 





