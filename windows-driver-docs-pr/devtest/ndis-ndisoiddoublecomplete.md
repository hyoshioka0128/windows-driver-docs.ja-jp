---
title: NdisOidDoubleComplete rule (ndis)
description: NdisOidDoubleComplete 規則は、NDIS ミニポートドライバーが同じ OID に対して NdisMOidRequestComplete ルーチンを2回呼び出すことができないことを指定します。
ms.assetid: 876A3D3C-554F-4D71-AD1B-F568D0AD6C0D
ms.date: 05/21/2018
keywords:
- NdisOidDoubleComplete rule (ndis)
topic_type:
- apiref
api_name:
- NdisOidDoubleComplete
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7a27791d1e0749885187a6285d60cc3391bf8c1b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839366"
---
# <a name="ndisoiddoublecomplete-rule-ndis"></a>NdisOidDoubleComplete rule (ndis)


**NdisOidDoubleComplete**規則は、NDIS ミニポートドライバーが同じ OID に対して[**NdisMOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)ルーチンを2回呼び出すことができないことを指定します。

OID は追跡 (追跡\_オブジェクト) されます。 カーネルデバッガーでこのエラーをデバッグするには、 **! ndiskd oid**デバッガー拡張機能を使用します。

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

|                                   |                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー\_VERIFIER\_検出された\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00091002) |

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

 

の順に移動します。

<a name="applies-to"></a>適用対象
----------

[**Miniportoidrequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)
[ **NdisMOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)
 

 





