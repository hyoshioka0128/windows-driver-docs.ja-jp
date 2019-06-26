---
title: NdisFilterTimedDataSend ルール (ndis)
description: NdisFilterTimedDataSend ルールは、NDIS フィルター ドライバーがタイムアウトになるまで FilterSendNetBufferLists 関数によって送信要求を完了することを確認します。
ms.assetid: 0D04DF73-4391-4668-8F6C-023BEE5A7F08
ms.date: 05/21/2018
keywords:
- NdisFilterTimedDataSend ルール (ndis)
topic_type:
- apiref
api_name:
- NdisFilterTimedDataSend
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 370df8703f71ee105d7230362182ab33643db310
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392104"
---
# <a name="ndisfiltertimeddatasend-rule-ndis"></a>NdisFilterTimedDataSend ルール (ndis)


**NdisFilterTimedDataSend**ルールでは、NDIS フィルター ドライバーが、送信要求が完了したことを検証、 [ *FilterSendNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_send_net_buffer_lists)タイムアウトになるまでの関数。

カーネル デバッガーを使用するには、問題の原因を識別できるようにします。 ルールのチェック\_PendingNbl、最も古いものを指すの状態を保留中[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)します。 使用して、 [ **! ndiskd.nbl** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ndiskd-nbl)デバッガー拡張機能。 デバッガーの使用方法の詳細については、次を参照してください。 [Windows デバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)します。

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

|                                   |                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) (0x00092011) |

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>を選択し、 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wifi-verification" data-raw-source="[NDIS/WIFI verification](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wifi-verification)">NDIS/WIFI 検証</a>オプション。 このルールはでテストされても、 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking" data-raw-source="[DDI compliance checking](https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking)">DDI 準拠の検査</a>オプション。</p></td>
</tr>
</tbody>
</table>

 

 

 





