---
title: KSCATEGORY_SPLITTER
description: KSCATEGORY_SPLITTER
ms.assetid: 056b6bc0-5566-4498-959d-dbc9725aa03e
keywords:
- KSCATEGORY_SPLITTER デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_SPLITTER
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c1c0ec5833c3af47f354307de44466fbff619e87
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366700"
---
# <a name="kscategorysplitter"></a>KSCATEGORY_SPLITTER


KSCATEGORY_SPLITTER[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)が定義されている、[カーネル ストリーミング](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)データ ストリームを分割する (KS) 機能のカテゴリ。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">属性</th>
<th align="left">設定</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>識別子</p></td>
<td align="left"><p>KSCATEGORY_SPLITTER</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{0A4252A0-7E70-11D0-A5D6-28DB04C10000}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KS オーディオ アダプター デバイス用のドライバーでは、オペレーティング システムに、デバイスが KSCATEGORY_SPLITTER 機能カテゴリをサポートすることを示す KSCATEGORY_SPLITTER のインスタンスを登録します。

KSCATEGORY_SPLITTER 機能のカテゴリは、のいずれか、 [ **KSPROPERTY_TOPOLOGY_CATEGORIES** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-topology-categories)機能別に分類します。

分割ウィンドウについては、次を参照してください。 [AVStream スプリッター](https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-splitters)します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ks.h (Ks.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY_TOPOLOGY_CATEGORIES**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-topology-categories)

 

 






