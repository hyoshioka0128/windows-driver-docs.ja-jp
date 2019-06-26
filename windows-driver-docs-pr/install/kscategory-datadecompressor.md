---
title: KSCATEGORY_DATADECOMPRESSOR
description: KSCATEGORY_DATADECOMPRESSOR
ms.assetid: 260906fc-fdd5-487f-9f45-db6ca4591233
keywords:
- KSCATEGORY_DATADECOMPRESSOR デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_DATADECOMPRESSOR
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8f48389862715402ab944f96cd5efff469440c20
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385899"
---
# <a name="kscategorydatadecompressor"></a>KSCATEGORY_DATADECOMPRESSOR


KSCATEGORY_DATADECOMPRESSOR[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)が定義されている、[カーネル ストリーミング](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)データ ストリームの圧縮を解除 (KS) 機能のカテゴリ。

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
<td align="left"><p>KSCATEGORY_DATADECOMPRESSOR</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{2721AE20-7E70-11D0-A5D6-28DB04C10000}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KS デバイス用のドライバーでは、オペレーティング システムに、デバイスが KSCATEGORY_DATADECOMPRESSOR 機能カテゴリをサポートすることを示す KSCATEGORY_DATADECOMPRESSOR のインスタンスを登録します。

KSCATEGORY_DATADECOMPRESSOR 機能のカテゴリは、のいずれか、 [ **KSPROPERTY_TOPOLOGY_CATEGORIES**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-topology-categories)します。

データ ストリームを圧縮する KS 機能カテゴリに対して定義されているデバイスのインターフェイス クラスについては、次を参照してください。 [ **KSCATEGORY_DATACOMPRESSOR**](kscategory-datacompressor.md)します。

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


[**KSCATEGORY_DATACOMPRESSOR**](kscategory-datacompressor.md)

[**KSPROPERTY_TOPOLOGY_CATEGORIES**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-topology-categories)

 

 






