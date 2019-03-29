---
title: KSPROPERTY\_接続\_ALLOCATORFRAMING
description: クライアントが、KSPROPERTY を使用して、ストリーム クラスのモデルで\_接続\_ALLOCATORFRAMING プロパティ、pin のフレームの要件を決定します。
ms.assetid: 02cacade-938b-4fab-928f-75f790692324
keywords:
- KSPROPERTY_CONNECTION_ALLOCATORFRAMING ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CONNECTION_ALLOCATORFRAMING
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a6f14e3a8ae50daaacfb47f466fa340789730d8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574340"
---
# <a name="kspropertyconnectionallocatorframing"></a>KSPROPERTY\_接続\_ALLOCATORFRAMING


クライアントが、KSPROPERTY を使用して、ストリーム クラスのモデルで\_接続\_ALLOCATORFRAMING プロパティ、pin のフレームの要件を決定します。

## <span id="ddk_ksproperty_connection_allocatorframing_ks"></span><span id="DDK_KSPROPERTY_CONNECTION_ALLOCATORFRAMING_KS"></span>


### <a name="usage-summary-table"></a>使用状況の概要テーブル

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>取得</th>
<th>Set</th>
<th>移行先</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>はい</p></td>
<td><p>いいえ</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560979" data-raw-source="[&lt;strong&gt;KSALLOCATOR_FRAMING&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560979)"><strong>KSALLOCATOR_FRAMING</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

このプロパティを返します、 [ **KSALLOCATOR\_フレーム**](https://msdn.microsoft.com/library/windows/hardware/ff560979)pin のフレームの要件をについて説明します。 たとえば、**フレーム ・ サイズ**メンバーが、ピンでデータのフレーム サイズを指定します。

AVStream ミニドライバーを使用する必要があります[ **KSPROPERTY\_接続\_ALLOCATORFRAMING\_EX**](ksproperty-connection-allocatorframing-ex.md)します。

参照してください[KS アロケーター](https://msdn.microsoft.com/library/windows/hardware/ff567257)します。 [AVStream アロケーター](https://msdn.microsoft.com/library/windows/hardware/ff554202)します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ks.h (Ks.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSALLOCATOR\_フレーム**](https://msdn.microsoft.com/library/windows/hardware/ff560979)

 

 






