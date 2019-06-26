---
title: NDKPI 完了処理要件
description: NDK コンシューマーと NDK プロバイダーは、NDKPI 完了処理するための要件に従う必要があります。
ms.assetid: 87150E2F-64F2-4EAB-A8B3-8E77622BE36C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fda94936acd396fa2f60ba70ddc4a1eeb2f18b9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376771"
---
# <a name="ndkpi-completion-handling-requirements"></a>NDKPI 完了処理要件


NDK コンシューマーと NDK プロバイダーは、NDKPI 完了処理するための要件に従う必要があります。

## <a name="the-rules-for-ndkgetcqresults-ndkgetcqresultsex-and-ndkarmcq-functions"></a>NdkGetCqResults、NdkGetCqResultsEx、NdkArmCq 関数のルール


コンシューマーで同じ完了キュー (CQ) オブジェクトでこれらのプロバイダー関数への呼び出しは常にシリアル化 ([**NDK\_CQ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_cq))。

-   *NdkGetCqResults* ([*NDK\_FN\_GET\_CQ\_RESULTS*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_get_cq_results))
-   *NdkGetCqResultsEx* ([*NDK\_FN\_GET\_CQ\_RESULTS\_EX*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_get_cq_results_ex))
-   *NdkArmCq* ([*NDK\_FN\_ARM\_CQ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_arm_cq))

コンシューマーは決して同じプロバイダー関数を複数回呼び出す同時ことは決してを呼び出すこともこれらの関数の任意の組み合わせに同時に同じ CQ 複数のスレッドからだけでなく意味します。

**NdkOperationTypeReceiveAndInvalidate**リモート結果として発生する完了*NdkSendAndInvalidate* ([*NDK\_FN\_送信\_AND\_INVALIDATE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_send_and_invalidate)) 呼び出しの取得を使用する必要がある*NdkGetCqResults* (いない*NdkGetCqResultsEx*n)。 これも、受信側で指定したトークンを無効にする必要がありますが、この無効化の受信側のコンシューマーに通知しない (コンシューマーが使用する必要があります*NdkGetCqResultsEx*この情報を取得する)。 以降、 *NdkInvalidate* ([*NDK\_FN\_INVALIDATE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_invalidate)) を通常どおり、同じトークンが失敗します。

## <a name="the-rules-for-notification-callbacks"></a>通知のコールバックの規則


プロバイダーを呼び出す必要があります、 *NdkCqNotificationCallback* ([*NDK\_FN\_CQ\_通知\_コールバック*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_cq_notification_callback)) コールバックを 1 回だけ、コンシューマーが武装した後でのみ、 *NdkCqNotificationCallback*呼び出すことによってコールバック*NdkArmCq*します。 プロバイダーは、arm をクリアする必要がありますを呼び出すと、 *NdkCqNotificationCallback*コールバック時に呼び出し元の条件、 *NdkCqNotificationCallback*コールバックが発生する (つまり、要求したとき入力候補に入れられ、CQ)。

あるかどうか、CQ に既に存在する入力候補、コンシューマーを呼び出すと*NdkArmCq*プロバイダーは次のように動作します。

-   少なくとも 1 つの入力候補が新しく追加された場合、CQ に前回*NdkCqNotificationCallback*コールバックが呼び出されると、プロバイダーは、arm 要求をすぐに (シリアル化の要件は以下を参照してください) を満たす必要があります。
-   ただし、存在する場合、CQ ですべての入力候補もときに最後*NdkCqNotificationCallback*コールバックが呼び出された (つまり、コンシューマーと呼ばれる*NdkArmCq*すべてを削除せず、入力候補および新しい入力候補に設定、CQ)、プロバイダーでは、arm 要求をすぐに満たすことがあります。

プロバイダーを呼び出す必要がある場合、 *NdkCqNotificationCallback*が既にある場合、コールバック、 *NdkCqNotificationCallback*進行中でコールバックし、プロバイダーの呼び出しを延期する必要があります、*NdkCqNotificationCallback*コールバックへの既存の呼び出し後まで、 *NdkCqNotificationCallback*コールバックは、プロバイダーにコントロールを返します。 つまり、プロバイダーは、シリアル化するため、 *NdkCqNotificationCallback*コールバック。

結果として得られる arm 入力の場合は、次の表に示します*NdkArmCq*する前に、前の 2 つ目に呼び出されます*NdkArmCq*要求を満たします。

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
<th align="left">2 番目の arm ANY</th>
<th align="left">2 番目の arm エラー</th>
<th align="left">2 番目の arm 要請</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1 日の arm ANY</p></td>
<td align="left"><p>任意</p></td>
<td align="left"><p>任意</p></td>
<td align="left"><p>任意</p></td>
</tr>
<tr class="even">
<td align="left"><p>1 日の arm エラー</p></td>
<td align="left"><p>任意</p></td>
<td align="left"><p>エラー</p></td>
<td align="left"><p>要請</p></td>
</tr>
<tr class="odd">
<td align="left"><p>1 日の arm 要請</p></td>
<td align="left"><p>任意</p></td>
<td align="left"><p>要請</p></td>
<td align="left"><p>要請</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック


[ネットワーク ダイレクト カーネル プロバイダー インターフェイス (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






