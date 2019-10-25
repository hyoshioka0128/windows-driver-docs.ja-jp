---
title: NDKPI 完了処理要件
description: NDK コンシューマーおよび NDK プロバイダーは、NDKPI 完了処理のために、次の要件に従う必要があります。
ms.assetid: 87150E2F-64F2-4EAB-A8B3-8E77622BE36C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d2e55f0f08707caf6bb26e334c61b00f62503a3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831905"
---
# <a name="ndkpi-completion-handling-requirements"></a>NDKPI 完了処理要件


NDK コンシューマーおよび NDK プロバイダーは、NDKPI 完了処理のために、次の要件に従う必要があります。

## <a name="the-rules-for-ndkgetcqresults-ndkgetcqresultsex-and-ndkarmcq-functions"></a>NdkGetCqResults、NdkGetCqResultsEx、および NdkArmCq の各関数の規則


コンシューマーは、これらのプロバイダー関数の呼び出しを、同じ完了キュー (CQ) オブジェクト ([**NDK\_CQ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_cq)) で常にシリアル化します。

-   *NdkGetCqResults* ([*NDK\_FN\_GET\_CQ\_の結果*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_get_cq_results))
-   *NdkGetCqResultsEx* ([*NDK\_FN\_GET\_CQ\_RESULTS\_EX*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_get_cq_results_ex))
-   *NdkArmCq* ([*NDK\_FN\_ARM\_CQ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_arm_cq))

これは、コンシューマーが同じプロバイダー関数を同時に複数回呼び出すことがないことを意味しますが、複数のスレッドから同じ CQ でこれらの関数の組み合わせを同時に呼び出すことはありません。

リモート*Ndksendandinvalidate* ([*NDK\_FN\_SEND\_および\_無効化*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_send_and_invalidate)) 呼び出しの結果として発生する**NdkOperationTypeReceiveAndInvalidate** completion は、引き続きを使用して*取得する必要があります。NdkGetCqResults* ( *NdkGetCqResultsEx*n 以外)。 その場合でも、受信側で指定されたトークンを無効にする必要がありますが、この無効化の受信側のコンシューマーには通知されません (コンシューマーは*NdkGetCqResultsEx*を使用してこの情報を取得する必要があります)。 同じトークンに対して後で*NdkInvalidate* ([*NDK\_FN\_無効化*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_invalidate)) は、通常どおり失敗します。

## <a name="the-rules-for-notification-callbacks"></a>通知コールバックのルール


プロバイダーは、 *NdkCqNotificationCallback* ([*NDK\_FN\_CQ\_NOTIFICATION\_callback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_cq_notification_callback)) コールバックを1回だけ呼び出す必要があります。また、コンシューマーが*NdkCqNotificationCallback*コールバックを実行した後にのみ、*NdkArmCq*を呼び出しています。 つまり、プロバイダーは arm をクリアし、 *NdkCqNotificationCallback*コールバックの呼び出し条件が発生したときに*NdkCqNotificationCallback*コールバックを呼び出す必要があります (つまり、要求の完了が CQ でキューに登録されている場合)。

コンシューマーが*NdkArmCq*を呼び出すときに、CQ に既に入力候補が存在する場合、プロバイダーは次のように動作します。

-   最後の*NdkCqNotificationCallback*コールバックが呼び出された後、少なくとも1つの入力候補が CQ に新しく配置された場合、プロバイダーは arm 要求を直ちに満たす必要があります (シリアル化の要件については、以下を参照してください)。
-   ただし、最後の*NdkCqNotificationCallback*コールバックが呼び出されたときに、CQ 内のすべての入力候補も存在した場合 (つまり、コンシューマーは、すべての入力候補を削除せずに*NdkArmCq*を呼び出しましたが、新しい入力候補は CQ に配置されませんでした。) では、プロバイダーは arm 要求をすぐに満たすことができます。

プロバイダーが*NdkCqNotificationCallback*コールバックを呼び出す必要がある場合、既に実行中の*NdkCqNotificationCallback*コールバックがある場合、プロバイダーは*NdkCqNotificationCallback*の呼び出しを遅延させる必要があります。*NdkCqNotificationCallback* callback への既存の呼び出しがプロバイダーに制御を返すまでのコールバック。 つまり、プロバイダーは*NdkCqNotificationCallback*コールバックのシリアル化を行います。

次の表は、前の*NdkArmCq*要求が満たされる前に*NdkArmCq*が2回呼び出された場合に生成される arm の種類を示しています。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"></th>
<th align="left">2番目の arm 任意</th>
<th align="left">arm の2番目のエラー</th>
<th align="left">2番目の arm の要請</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1番目の arm 任意</p></td>
<td align="left"><p>いつ</p></td>
<td align="left"><p>いつ</p></td>
<td align="left"><p>いつ</p></td>
</tr>
<tr class="even">
<td align="left"><p>arm の1回目のエラー</p></td>
<td align="left"><p>いつ</p></td>
<td align="left"><p>誤り</p></td>
<td align="left"><p>要請</p></td>
</tr>
<tr class="odd">
<td align="left"><p>1番目の arm の要請</p></td>
<td align="left"><p>いつ</p></td>
<td align="left"><p>要請</p></td>
<td align="left"><p>要請</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック


[ネットワークダイレクトカーネルプロバイダーインターフェイス (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






