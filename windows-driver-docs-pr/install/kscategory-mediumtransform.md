---
title: KSCATEGORY_MEDIUMTRANSFORM
description: KSCATEGORY_MEDIUMTRANSFORM
ms.assetid: a57c0dd5-48b1-4f58-ac3a-e1f175a228f0
keywords:
- KSCATEGORY_MEDIUMTRANSFORM デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_MEDIUMTRANSFORM
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c6a451ecb060ef3be5388f51d3ccc0a6948f2ec7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387023"
---
# <a name="kscategorymediumtransform"></a>KSCATEGORY_MEDIUMTRANSFORM


KSCATEGORY_MEDIUMTRANSFORM[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)が定義されている、[カーネル ストリーミング](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)(KS) 機能のカテゴリが使用されているメディアの種類を変換します。

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
<td align="left"><p>KSCATEGORY_MEDIUMTRANSFORM</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{CF1DDA2E-9743-11D0-A3EE-00A0C9223196}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KS デバイス用のドライバーでは、オペレーティング システムに、デバイスが KSCATEGORY_MEDIUMTRANSFORM 機能カテゴリをサポートすることを示す KSCATEGORY_MEDIUMTRANSFORM のインスタンスを登録します。

KSCATEGORY_MEDIUMTRANSFORM 機能のカテゴリは、のいずれか、 [ **KSPROPERTY_TOPOLOGY_CATEGORIES** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-topology-categories)機能別に分類します。

<a name="requirements"></a>必要条件
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

 

 






