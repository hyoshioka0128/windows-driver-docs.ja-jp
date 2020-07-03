---
title: NdisFilterTimedDataSend rule (ndis)
description: NdisFilterTimedDataSend 規則は、NDIS フィルタードライバーが、タイムアウトする前に FilterSendNetBufferLists 関数によって送信要求を完了することを確認します。
ms.assetid: 0D04DF73-4391-4668-8F6C-023BEE5A7F08
ms.date: 05/21/2018
keywords:
- NdisFilterTimedDataSend rule (ndis)
topic_type:
- apiref
api_name:
- NdisFilterTimedDataSend
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 75692efb304ec466722806865c30cc74d9a40559
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916300"
---
# <a name="ndisfiltertimeddatasend-rule-ndis"></a>NdisFilterTimedDataSend rule (ndis)


**NdisFilterTimedDataSend**規則は、NDIS フィルタードライバーが、タイムアウトする前に[*filtersendnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists)関数によって送信要求を完了することを確認します。

カーネルデバッガーを使用して、問題の原因を特定することができます。 \_PendingNbl のルールの状態を確認します。これは、最も古い保留中の[**NET \_ BUFFER \_ リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)を指します。 [**! Ndiskd nbl**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ndiskd-nbl)デバッガー拡張機能を使用します。 デバッガーの使用方法の詳細については、「 [Windows デバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)」を参照してください。

**ドライバーモデル: NDIS**

|                                   |                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー \_検証の \_ 検出 \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00092011) |

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">ドライバーの検証ツール</a>を実行し、 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wifi-verification" data-raw-source="[NDIS/WIFI verification](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wifi-verification)">NDIS/WIFI 検証</a>オプションを選択します。 このルールは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking" data-raw-source="[DDI compliance checking](https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking)">DDI 準拠チェック</a>オプションを使用してもテストされます。</p></td>
</tr>
</tbody>
</table>

 

 

 





