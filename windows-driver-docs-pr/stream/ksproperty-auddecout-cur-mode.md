---
title: KSK プロパティ\_\_\_モードになっています
description: KSK プロパティ\_"\_"\_MODE プロパティは、現在のオーディオ出力モードを示します。
ms.assetid: 4ac6d181-f532-4ac6-b8fd-2975214a3618
keywords:
- KSPROPERTY_AUDDECOUT_CUR_MODE ストリーミングメディアデバイス
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
ms.openlocfilehash: 78c3c44a23cc9cc3b452470bbc9fe922953e47e7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845379"
---
# <a name="ksproperty_auddecout_cur_mode"></a>KSK プロパティ\_\_\_モードになっています


KSK プロパティ\_"\_"\_MODE プロパティは、現在のオーディオ出力モードを示します。

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
<td><p>DWORD</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、オーディオデコーダーの現在の出力モードを表す DWORD です。

<a name="remarks"></a>注釈
-------

プロパティ値には、次のいずれかのモード定数を指定することができ*ます。*

<span id="KSAUDDECOUTMODE_STEREO_ANALOG"></span><span id="ksauddecoutmode_stereo_analog"></span>**KSK の\_ステレオ\_アナログ**  
は、出力がアナログステレオであることを示します。

<span id="KSAUDDECOUTMODE_PCM_51"></span><span id="ksauddecoutmode_pcm_51"></span>**KSK の\_PCM\_51**  
出力が PCM 5.1 チャネルデジタル内にあることを示します。

<span id="KSAUDDECOUTMODE_SPDIFF"></span><span id="ksauddecoutmode_spdiff"></span>**KSK\_の SPDIFF**  
出力が SPDIFF 形式の AC3 デジタルであることを示します。

オーディオミニポートドライバーの get プロパティハンドラーはデコーダーの現在のモードを返しますが、オーディオミニポートドライバーのセットプロパティハンドラーはデコーダーが出力オーディオ形式を要求されたモードに切り替えるように要求します。

レジストリに設定されているミニドライバーのシリアル化されたプロパティで、KSK プロパティ\_"\_"\_MODE プロパティに既定値を指定することをお勧めします。

詳細については、「[オーディオミニポートドライバー](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-miniport-drivers)」を参照してください。

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


[**KSPROPERTY\_\_モード**](ksproperty-auddecout-modes.md)

 

 






