---
title: NdisTimedDataHang rule (ndis)
description: NdisTimedDataHang 規則は、NDIS ミニポートドライバーが、 \_ 22 秒以内に NET バッファーリスト構造に対する保留中の送信要求を処理することを確認し \_ ます。
ms.assetid: CDFC9C23-B065-4916-BF1C-5429B6B57A23
ms.date: 05/21/2018
keywords:
- NdisTimedDataHang rule (ndis)
topic_type:
- apiref
api_name:
- NdisTimedDataHang
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1033d8894ff1e7e36195b3cbaac4a55bb3ba68e2
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916322"
---
# <a name="ndistimeddatahang-rule-ndis"></a>NdisTimedDataHang rule (ndis)


**NdisTimedDataHang**規則は、NDIS ミニポートドライバーが、22秒以内に[**NET \_ バッファー \_ リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造に対する保留中の送信要求を処理することを確認します。

ミニポートドライバーは、すべての[**NET \_ BUFFER \_ リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造に対する保留中の送信要求を完了するために、 [**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)関数を呼び出す必要があります。 保留中の送信要求がある場合は、NDIS ミニポートドライバーが引き続き完了する必要があります。 このルールは、 **NET \_ BUFFER \_ LIST**構造に対して保留中の送信要求が少なくとも1つ存在し、そのような送信要求が過去22秒間に完了していない場合に違反します。

カーネルデバッガーを使用して、問題の原因を特定することができます。 \_PendingNbl のルールの状態を確認します。これは、最も古い保留中の[**NET \_ BUFFER \_ リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)を指します。 [**! Ndiskd nbl**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ndiskd-nbl)デバッガー拡張機能を使用します。 デバッガーの使用方法の詳細については、「 [Windows デバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)」を参照してください。

**ドライバーモデル: NDIS**

|                                   |                                                                                                                                         |
|-----------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー \_検証の \_ 検出 \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x0x0009200F) |

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">実行時</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">ドライバーの検証ツール</a>を実行し、 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wifi-verification" data-raw-source="[NDIS/WIFI verification](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wifi-verification)">NDIS/WIFI 検証</a>オプションを選択します。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>適用対象
----------

[**Miniportsendnetbufferlists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists) 
[ **NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)
 

 





