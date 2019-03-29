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
ms.openlocfilehash: 4c58c8a988f63419ea05f63a5710782f381c2a59
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578235"
---
# <a name="ndisfiltertimeddatasend-rule-ndis"></a>NdisFilterTimedDataSend ルール (ndis)


**NdisFilterTimedDataSend**ルールでは、NDIS フィルター ドライバーが、送信要求が完了したことを検証、 [ *FilterSendNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff549966)タイムアウトになるまでの関数。

カーネル デバッガーを使用するには、問題の原因を識別できるようにします。 ルールのチェック\_PendingNbl、最も古いものを指すの状態を保留中[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)します。 使用して、 [ **! ndiskd.nbl** ](https://msdn.microsoft.com/library/windows/hardware/ff564156)デバッガー拡張機能。 デバッガーの使用方法の詳細については、次を参照してください。 [Windows デバッグ](https://msdn.microsoft.com/library/windows/hardware/ff551063)します。

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

|                                   |                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00092011) |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a>を選択し、 <a href="https://msdn.microsoft.com/library/windows/hardware/dn312128" data-raw-source="[NDIS/WIFI verification](https://msdn.microsoft.com/library/windows/hardware/dn312128)">NDIS/WIFI 検証</a>オプション。 このルールはでテストされても、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh454208" data-raw-source="[DDI compliance checking](https://msdn.microsoft.com/library/windows/hardware/hh454208)">DDI 準拠の検査</a>オプション。</p></td>
</tr>
</tbody>
</table>

 

 

 





