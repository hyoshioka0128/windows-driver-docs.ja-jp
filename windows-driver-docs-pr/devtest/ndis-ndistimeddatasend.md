---
title: NdisTimedDataSend rule (ndis)
description: NdisTimedDataSend ルールは、NDIS ドライバーが MiniportSendNetBufferLists を呼び出すと、ミニポートドライバーが30秒以内に送信要求を完了することを確認します。
ms.assetid: 2240254E-4381-4009-ACF2-DA481CB065FE
ms.date: 05/21/2018
keywords:
- NdisTimedDataSend rule (ndis)
topic_type:
- apiref
api_name:
- NdisTimedDataSend
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 045e68b583588c8db723eddbe91d6e5fa043cc70
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916320"
---
# <a name="ndistimeddatasend-rule-ndis"></a>NdisTimedDataSend rule (ndis)


**NdisTimedDataSend**ルールは、NDIS ドライバーが[*Miniportsendnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)を呼び出すと、ミニポートドライバーが30秒以内に送信要求を完了することを確認します。

カーネルデバッガーを使用して、問題の原因を特定することができます。 \_PendingNbl のルールの状態を確認します。これにより、タイムアウトの原因となっている保留中のバッファーの一覧が参照されます。 [**Nbl**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ndiskd-nbl)デバッガー拡張機能を使用して、 [**NET \_ BUFFER \_ リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)を確認します。 デバッガーの使用方法の詳細については、「 [Windows デバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)」を参照してください。

**ドライバーモデル: NDIS**

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー \_検証の \_ 検出 \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x0009200d) |

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
 

 





