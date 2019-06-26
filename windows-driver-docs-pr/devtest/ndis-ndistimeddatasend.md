---
title: NdisTimedDataSend ルール (ndis)
description: NDIS ドライバー MiniportSendNetBufferLists を呼び出すと、ミニポート ドライバーが完了する、送信要求 30 秒以内 NdisTimedDataSend ルールを確認します。
ms.assetid: 2240254E-4381-4009-ACF2-DA481CB065FE
ms.date: 05/21/2018
keywords:
- NdisTimedDataSend ルール (ndis)
topic_type:
- apiref
api_name:
- NdisTimedDataSend
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 434dfce8b0dbc79f114e2bac2a9acb3c346ffaf7
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392184"
---
# <a name="ndistimeddatasend-rule-ndis"></a>NdisTimedDataSend ルール (ndis)


**NdisTimedDataSend**規則検証する NDIS ドライバーを呼び出すと[ *MiniportSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_send_net_buffer_lists)、ミニポート ドライバーが 30 の送信要求を完了します。秒数。

カーネル デバッガーを使用するには、問題の原因を識別できるようにします。 ルールのチェック\_PendingNbl、タイムアウトの原因となる保留中のバッファーの一覧を示す状態。 使用して、 [ **! ndiskd.nbl** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ndiskd-nbl)デバッガー拡張機能を調べる、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)します。 デバッガーの使用方法の詳細については、次を参照してください。 [Windows デバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)します。

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) (0x0009200D) |

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">実行時に</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>を選択し、 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wifi-verification" data-raw-source="[NDIS/WIFI verification](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wifi-verification)">NDIS/WIFI 検証</a>オプション。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>適用対象
----------

[**MiniportSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_send_net_buffer_lists)
[**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsendnetbufferlistscomplete)
 

 





