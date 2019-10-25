---
title: KSPROPERTY\_接続\_ALLOCATORFRAMING\_EX
description: AVStream クライアントは、KSK プロパティ\_接続\_ALLOCATORFRAMING\_EX プロパティを使用して、pin のフレーム要件を決定します。
ms.assetid: 7ff1462f-959b-413e-a888-bcf7d251edee
keywords:
- KSPROPERTY_CONNECTION_ALLOCATORFRAMING_EX ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CONNECTION_ALLOCATORFRAMING_EX
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad41468c03ec8b8e1a0ff5b528ea41b191c8e707
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826832"
---
# <a name="ksproperty_connection_allocatorframing_ex"></a>KSPROPERTY\_接続\_ALLOCATORFRAMING\_EX


AVStream クライアントは、KSK プロパティ\_接続\_ALLOCATORFRAMING\_EX プロパティを使用して、pin のフレーム要件を決定します。

## <span id="ddk_ksproperty_connection_allocatorframing_ex_ks"></span><span id="DDK_KSPROPERTY_CONNECTION_ALLOCATORFRAMING_EX_KS"></span>


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
<th>[購入]</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>[はい]</p></td>
<td><p>必須ではない</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing_ex" data-raw-source="[&lt;strong&gt;KSALLOCATOR_FRAMING_EX&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing_ex)"><strong>KSALLOCATOR_FRAMING_EX</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このプロパティは、AVStream pin のフレーム要件を記述する[**Ksallocator\_フレーミング\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing_ex)を返します。

Stream クラスで実行されているミニドライバーは、 [ **\_ALLOCATORFRAMING の\_接続に Ksk プロパティ**](ksproperty-connection-allocatorframing.md)を使用する必要があります。

「 [KS アロケーター](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-allocators)」を参照してください。 および[Avstream アロケーター](https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-allocators)。

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
<td>Ks (Ks を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSALLOCATOR\_フレーミング\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing_ex)

 

 






