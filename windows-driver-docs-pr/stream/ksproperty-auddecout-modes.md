---
title: KSPROPERTY\_AUDDECOUT\_モード
description: KSPROPERTY\_AUDDECOUT\_モード プロパティは、オーディオ、デコーダーの使用可能な出力モードを返します。このプロパティは読み取り専用です。
ms.assetid: 5ae62fae-7f13-480f-ba36-3fa72ff547bc
keywords:
- KSPROPERTY_AUDDECOUT_MODES ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDDECOUT_MODES
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 089358193304622fe0d08f06b0cf3ca0d986815b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384149"
---
# <a name="kspropertyauddecoutmodes"></a>KSPROPERTY\_AUDDECOUT\_モード


KSPROPERTY\_AUDDECOUT\_モード プロパティは、オーディオ、デコーダーの使用可能な出力モードを返します。

このプロパティは読み取り専用です。

## <span id="ddk_ksproperty_auddecout_modes_ks"></span><span id="DDK_KSPROPERTY_AUDDECOUT_MODES_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>DWORD</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、ビットマスクのオーディオのデコーダーをサポートするオーディオ出力モードを表す DWORD です。

<a name="remarks"></a>注釈
-------

プロパティの値は、次の定数で定義されているのビットごとの OR を含めることができます、 *Ksmedia.h*ヘッダー ファイル。

<span id="KSAUDDECOUTMODE_STEREO_ANALOG"></span><span id="ksauddecoutmode_stereo_analog"></span>**KSAUDDECOUTMODE\_ステレオ\_アナログ**  
出力がアナログ ステレオであることを示します。

<span id="KSAUDDECOUTMODE_PCM_51"></span><span id="ksauddecoutmode_pcm_51"></span>**KSAUDDECOUTMODE\_PCM\_51**  
デジタル PCM 5.1 チャネルで出力があることを示します。

<span id="KSAUDDECOUTMODE_SPDIFF"></span><span id="ksauddecoutmode_spdiff"></span>**KSAUDDECOUTMODE\_SPDIFF**  
出力が SPDIFF 形式 AC3 デジタルであることを示します。

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
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY\_AUDDECOUT\_CUR\_モード**](ksproperty-auddecout-cur-mode.md)

 

 






