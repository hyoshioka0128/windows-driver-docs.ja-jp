---
title: NdisFilterTimedDataReceive rule (ndis)
description: NdisFilterTimedDataReceive 規則は、NDIS フィルタードライバーが、タイムアウトする前に FilterReceiveNetBufferLists 関数によって受信要求を完了することを確認します。
ms.assetid: B7B557F5-2D41-4F1F-9DE6-6BE23860A39E
ms.date: 05/21/2018
keywords:
- NdisFilterTimedDataReceive rule (ndis)
topic_type:
- apiref
api_name:
- NdisFilterTimedDataReceive
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 31e1469f5a2af85ca1e50d5d967f84747438dd85
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839341"
---
# <a name="ndisfiltertimeddatareceive-rule-ndis"></a>NdisFilterTimedDataReceive rule (ndis)


**NdisFilterTimedDataReceive**規則は、NDIS フィルタードライバーが、タイムアウトする前に[*FilterReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists)関数によって受信要求を完了することを確認します。

カーネルデバッガーを使用して、問題の原因を特定することができます。 PendingNbl のルール\_の状態を確認します。これは、保留中の最も古い[**NET\_BUFFER\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)を指します。 [ **! Ndiskd nbl**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ndiskd-nbl)デバッガー拡張機能を使用します。 デバッガーの使用方法の詳細については、「 [Windows デバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)」を参照してください。

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

|                                   |                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー\_VERIFIER\_検出された\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00092012) |

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

 

 

 





