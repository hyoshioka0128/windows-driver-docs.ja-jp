---
title: バグ チェック 0x189 BAD_OBJECT_HEADER
description: BAD_OBJECT_HEADER のバグ チェックでは、0x00000189 の値を持ちます。 これは、「OBJECT_HEADER が破損していることを示します。
ms.assetid: 1B4F586A-2DFB-421A-863B-CC706FB4795B
keywords:
- バグ チェック 0x189 BAD_OBJECT_HEADER
- BAD_OBJECT_HEADER
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- BAD_OBJECT_HEADER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 492a795590eaa1baa92283ab641c2b4e75fbb04a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362086"
---
# <a name="bug-check-0x189-badobjectheader"></a>バグ チェック 0x189:不適切な\_オブジェクト\_ヘッダー


不適切な\_オブジェクト\_ヘッダーのバグ チェックが 0x00000189 の値を持ちます。 これが示す「オブジェクト\_ヘッダーが破損しています。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="badobjectheader-parameters"></a>不適切な\_オブジェクト\_ヘッダー パラメーター


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">1</td>
<td align="left">不適切な OBJECT_HEADER へのポインター</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">OBJECT_HEADER TypeIndex をに基づいて、結果として得られる OBJECT_TYPE へのポインター</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left"><p>破損の種類です。</p>
0x0 :型のインデックスは、破損している 0x1 を示します。オブジェクトのセキュリティ記述子が無効です。</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">予約済み</td>
</tr>
</tbody>
</table>

 

 

 




