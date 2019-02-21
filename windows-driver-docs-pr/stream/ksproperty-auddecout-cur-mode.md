---
title: KSPROPERTY\_AUDDECOUT\_CUR\_モード
description: KSPROPERTY\_AUDDECOUT\_CUR\_モード プロパティは、現在のオーディオ出力モードを示します。
ms.assetid: 4ac6d181-f532-4ac6-b8fd-2975214a3618
keywords:
- KSPROPERTY_AUDDECOUT_CUR_MODE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDDECOUT_CUR_MODE
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6de09fbd9bbd31a4242a411f26ddd2c54728ffa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528643"
---
# <a name="kspropertyauddecoutcurmode"></a>KSPROPERTY\_AUDDECOUT\_CUR\_モード


KSPROPERTY\_AUDDECOUT\_CUR\_モード プロパティは、現在のオーディオ出力モードを示します。

## <span id="ddk_ksproperty_auddecout_cur_mode_ks"></span><span id="DDK_KSPROPERTY_AUDDECOUT_CUR_MODE_KS"></span>


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
<td><p>〇</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>DWORD</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、オーディオ、デコーダーの現在の出力モードを表す DWORD です。

<a name="remarks"></a>注釈
-------

プロパティの値は、ヘッダー ファイルで定義されている次のモードの定数のいずれかを指定できます*ksmedia.h*:

<span id="KSAUDDECOUTMODE_STEREO_ANALOG"></span><span id="ksauddecoutmode_stereo_analog"></span>**KSAUDDECOUTMODE\_ステレオ\_アナログ**  
出力がアナログ ステレオであることを示します。

<span id="KSAUDDECOUTMODE_PCM_51"></span><span id="ksauddecoutmode_pcm_51"></span>**KSAUDDECOUTMODE\_PCM\_51**  
デジタル PCM 5.1 チャネルで出力があることを示します。

<span id="KSAUDDECOUTMODE_SPDIFF"></span><span id="ksauddecoutmode_spdiff"></span>**KSAUDDECOUTMODE\_SPDIFF**  
出力が SPDIFF 形式 AC3 デジタルであることを示します。

オーディオのミニポート ドライバーのプロパティの get ハンドラーは、デコーダーの現在のモードを返し、オーディオのミニポート ドライバー セット プロパティのハンドラーがデコーダーが出力オーディオ形式を要求されたモードに切り替えることを要求します。

KSPROPERTY の既定値を指定することをお勧めします。\_AUDDECOUT\_CUR\_、ミニドライバーの MODE プロパティ プロパティ、レジストリの設定をシリアル化します。

詳細については、次を参照してください。[オーディオ ミニポート ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff536206)します。

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


[**KSPROPERTY\_AUDDECOUT\_モード**](ksproperty-auddecout-modes.md)

 

 






