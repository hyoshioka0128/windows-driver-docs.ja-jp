---
title: NdisTimedDataHang ルール (ndis)
description: NdisTimedDataHang ルールでは、NET の NDIS ミニポート ドライバーがすべての保留中の送信要求を処理することを確認\_バッファー\_22 秒内のリストの構造体。
ms.assetid: CDFC9C23-B065-4916-BF1C-5429B6B57A23
ms.date: 05/21/2018
keywords:
- NdisTimedDataHang ルール (ndis)
topic_type:
- apiref
api_name:
- NdisTimedDataHang
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 960fa64c4f64193f69eddf09c9f69e3eae97dd9e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531192"
---
# <a name="ndistimeddatahang-rule-ndis"></a>NdisTimedDataHang ルール (ndis)


**NdisTimedDataHang** NDIS ミニポート ドライバーでのすべての保留中の送信要求を処理するルールを確認します[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)22 秒内の構造。

ミニポート ドライバーを呼び出す必要があります、 [ **NdisMSendNetBufferListsComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563668)関数がすべての保留中の送信要求を完了する[ **NET\_バッファー\_リスト**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。 保留中の送信要求があるを場合は、NDIS ミニポート ドライバーがそれらを完了する続行する必要があります。 少なくとも 1 つの保留中の送信要求がある場合にこの規則に違反を**NET\_バッファー\_一覧**構造とないこのような過去 22 秒で完了した要求を送信します。

カーネル デバッガーを使用するには、問題の原因を識別できるようにします。 ルールのチェック\_PendingNbl、最も古いものを指すの状態を保留中[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)します。 使用して、 [ **! ndiskd.nbl** ](https://msdn.microsoft.com/library/windows/hardware/ff564156)デバッガー拡張機能。 デバッガーの使用方法の詳細については、[Windows デバッグ](https://msdn.microsoft.com/library/windows/hardware/ff551063)を参照してください。

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

|                                   |                                                                                                                                         |
|-----------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x0x0009200F) |

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
 

 





