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
ms.openlocfilehash: e68b7c56fcea1342460d9772f41d7bc74a030fbe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365210"
---
# <a name="ndistimeddatasend-rule-ndis"></a>NdisTimedDataSend ルール (ndis)


**NdisTimedDataSend**規則検証する NDIS ドライバーを呼び出すと[ *MiniportSendNetBufferLists*](https://msdn.microsoft.com/library/windows/hardware/ff559440)、ミニポート ドライバーが 30 の送信要求を完了します。秒数。

カーネル デバッガーを使用するには、問題の原因を識別できるようにします。 ルールのチェック\_PendingNbl、タイムアウトの原因となる保留中のバッファーの一覧を示す状態。 使用して、 [ **! ndiskd.nbl** ](https://msdn.microsoft.com/library/windows/hardware/ff564156)デバッガー拡張機能を調べる、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)します。 デバッガーの使用方法の詳細については、次を参照してください。 [Windows デバッグ](https://msdn.microsoft.com/library/windows/hardware/ff551063)します。

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x0009200D) |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a>を選択し、 <a href="https://msdn.microsoft.com/library/windows/hardware/dn312128" data-raw-source="[NDIS/WIFI verification](https://msdn.microsoft.com/library/windows/hardware/dn312128)">NDIS/WIFI 検証</a>オプション。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>適用対象
----------

[**MiniportSendNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff559440)
[**NdisMSendNetBufferListsComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563668)
 

 





