---
title: NdisFilterTimedPauseComplete rule (ndis)
description: NdisFilterTimedPauseComplete は、FilterPause 関数が10秒以内に完了することを確認します。FilterPause 関数は失敗しません。FilterPause 関数を2回完了することはできません。
ms.assetid: 60B926CC-E2C4-42B8-8555-5E620DCDDAFC
ms.date: 05/21/2018
keywords:
- NdisFilterTimedPauseComplete rule (ndis)
topic_type:
- apiref
api_name:
- NdisFilterTimedPauseComplete
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fcf139118b4347c517b1d6d0cf040e698e7faa6e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839339"
---
# <a name="ndisfiltertimedpausecomplete-rule-ndis"></a>NdisFilterTimedPauseComplete rule (ndis)


**NdisFilterTimedPauseComplete**は次の3つのことを確認します。

-   [*Filterpause*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_pause)関数は10秒以内に完了します。

-   [*Filterpause*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_pause)関数は失敗しません。

-   [*Filterpause*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_pause)関数を2回完了することはできません。

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

|                                   |                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー\_VERIFIER\_検出された\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00092010) |

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

 

 

 





