---
title: WIA\_IP\_経由で\_スキャン\_右
description: WIA\_IP\_経由で\_スキャン\_WIA と共に RIGHT プロパティ\_IP\_経由で\_スキャン\_左、WIA\_IP\_経由で\_スキャン\_上部と WIA\_IP\_経由で\_スキャン\_下部がインチの後続のスキャン、経由での量を構成に使用されます (0.001 \ 0034;)物理的なドキュメントを基準との単位です。
ms.assetid: 17259314-2102-46B9-A493-7F879A7D0604
keywords:
- WIA_IPS_OVER_SCAN_RIGHT イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_OVER_SCAN_RIGHT
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: c3fe67bd9c62239e23157482a2476b64ff572f08
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354647"
---
# <a name="wiaipsoverscanright"></a>WIA\_IP\_経由で\_スキャン\_右


**WIA\_IP\_経由で\_スキャン\_右**プロパティと共に[ **WIA\_IP\_経由で\_スキャン\_左**](wia-ips-over-scan-left.md)、 [ **WIA\_IP\_経由で\_スキャン\_上部**](wia-ips-over-scan-top.md)、および[ **WIA\_IP\_経由で\_スキャン\_下部**](wia-ips-over-scan-bottom.md)インチ (0.001 インチ) 単位では、後続のスキャン、経由での量を構成するために使用物理的なドキュメントを基準にします。 WIA ミニドライバーは、作成し、このプロパティを保持します。




プロパティの種類:VT\_UI4

有効な値 :WIA\_PROP\_範囲

アクセス権:[読み取り/書き込み]

<a name="remarks"></a>注釈
-------

このプロパティは、フラット ベッドを含むすべてプログラミング可能なイメージのデータ ソース アイテムの有効な (WIA\_カテゴリ\_ベッド) とフィーダー (WIA\_カテゴリ\_フィーダー) が、場合にのみ、 [ **WIA\_IP\_経由で\_スキャン**](wia-ips-over-scan.md)プロパティがサポートされています。 サポートされている場合は、このプロパティが必要です。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

 

 





