---
title: KSPROPERTY\_BDA\_PIN\_ID
description: クライアントを使用して、KSPROPERTY\_BDA\_PIN\_pin の BDA 識別子 (ID) を取得する ID。
ms.assetid: 6f7a4454-1294-4646-8e21-bfec9a14b612
keywords:
- KSPROPERTY_BDA_PIN_ID ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_PIN_ID
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14ee22245d287a47508005fdfed2353e8e078b7e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390549"
---
# <a name="kspropertybdapinid"></a>KSPROPERTY\_BDA\_PIN\_ID


クライアントを使用して、KSPROPERTY\_BDA\_PIN\_pin の BDA 識別子 (ID) を取得する ID。

## <span id="ddk_ksproperty_bda_pin_id_ks"></span><span id="DDK_KSPROPERTY_BDA_PIN_ID_KS"></span>


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
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>〇</p></td>
<td><p>いいえ</p></td>
<td><p>Pin</p></td>
<td><p>KSPROPERTY</p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

戻り値は、暗証番号 (pin) の ID を指定します。

ネットワーク プロバイダーが KSMETHOD を使用してフィルターの暗証番号 (pin) を作成するときに\_BDA\_作成\_PIN\_ファクトリ、フィルターの BDA ミニドライバーは、その pin ID KSPROPERTY\_BDA\_PIN\_ID は、この ID を返します。

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
<td>Bdamedia.h (Bdamedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSMETHOD\_BDA\_作成\_PIN\_ファクトリ**](ksmethod-bda-create-pin-factory.md)

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

 

 






