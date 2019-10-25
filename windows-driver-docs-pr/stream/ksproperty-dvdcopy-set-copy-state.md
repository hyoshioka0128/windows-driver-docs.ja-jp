---
title: KSK プロパティ\_DVDCOPY\_設定\_コピー\_状態
description: KSK プロパティ\_DVDCOPY\_SET\_\_STATE プロパティは、DVD デコーダーストリームのコピー状態を設定します。 このプロパティは、を実装する場合は省略可能です。
ms.assetid: f4e46d79-c70b-413a-9702-a73d3776ee2c
keywords:
- KSPROPERTY_DVDCOPY_SET_COPY_STATE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_DVDCOPY_SET_COPY_STATE
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b098d9753b25c4ce5d3de9bfecab6aeb91d6b83
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843324"
---
# <a name="ksproperty_dvdcopy_set_copy_state"></a>KSK プロパティ\_DVDCOPY\_設定\_コピー\_状態


KSK プロパティ\_DVDCOPY\_SET\_\_STATE プロパティは、DVD デコーダーストリームのコピー状態を設定します。 このプロパティは、を実装する場合は省略可能です。

## <span id="ddk_ksproperty_dvdcopy_set_copy_state_ks"></span><span id="DDK_KSPROPERTY_DVDCOPY_SET_COPY_STATE_KS"></span>


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
<td><p>[はい]</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_set_copy_state" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_SET_COPY_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_set_copy_state)"><strong>KS_DVDCOPY_SET_COPY_STATE</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、\_DVDCOPY\_セットであり、DVD デコーダーストリームの著作権保護の状態を記述する\_コピー\_状態の構造を設定します。

<a name="remarks"></a>注釈
-------

このプロパティは、この pin が CSS 認証を必要とするかどうかを示します。 このプロパティが実装されていない場合、既定値は ks [ **\_DVDCOPYSTATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ks_dvdcopystate)列挙からの **\_\_認証\_必要な**値と見なされます。

このプロパティの主な用途は、同じ decrypter を持つ複数の pin をサポートするデコーダーです。 たとえば、1つのフィルターがサブピクチャとビデオのデコードの両方を提供する場合、キーを交換する必要があるのは2つの pin のうちの1つだけです。 フィルターによって Ks\_DVDCOPYSTATE が返される場合\_認証\_いずれかの pin に**必要\_ありません**。その場合は、次の\_ように**要求**されます。プロパティが発行される最初の pin。

このプロパティが**Get**呼び出しとして発行されると、フィルターは **\_DVDCOPYSTATE\_authentication\_REQUIRED**または KS\_DVDCOPYSTATE\_認証\_不要であることを示す応答を返すことができます。

このプロパティが**Set**呼び出しとして発行されると、これは、ハードウェアデコーダーが、入力されている著作権保護ネゴシエーションのフェーズを示すために使用する情報呼び出しです。 デコーダーは、新しい CSS キーが必要であることを示す正しいビットが受信されるまで、次のいずれかを使用して、SET\_状態を保持できます。

<span id="KS_DVDCOPYSTATE_INITIALIZE"></span><span id="ks_dvdcopystate_initialize"></span>**KS\_DVDCOPYSTATE\_INITIALIZE**  
ディスクキーネゴシエーションシーケンスの開始を示します。

<span id="KS_DVDCOPYSTATE_INITIALIZE_TITLE"></span><span id="ks_dvdcopystate_initialize_title"></span>**KS\_DVDCOPYSTATE\_INITIALIZE\_TITLE**  
タイトルキーネゴシエーションシーケンスの開始を示します。

<span id="KS_DVDCOPYSTATE_DONE"></span><span id="ks_dvdcopystate_done"></span>**KS\_DVDCOPYSTATE\_DONE**  
キーネゴシエーションシーケンスの完了を示します。

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
<td>Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KS\_DVDCOPY\_設定\_コピー\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_set_copy_state)

[**KS\_DVDCOPYSTATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ks_dvdcopystate)

[DVD の著作権保護](https://docs.microsoft.com/windows-hardware/drivers/stream/dvd-copyright-protection)

[同じハードウェア上の複数のデータストリーム](https://docs.microsoft.com/windows-hardware/drivers/stream/multiple-data-streams-on-the-same-hardware)

[キー交換とデータフローの同期](https://docs.microsoft.com/windows-hardware/drivers/stream/synchronizing-key-exchange-with-data-flow)

 

 






