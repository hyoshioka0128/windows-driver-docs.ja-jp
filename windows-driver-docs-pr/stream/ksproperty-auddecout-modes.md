---
title: KSPROPERTY\_\_モード
description: "\"\\_\\_\" の KSK プロパティは、音声デコーダーの使用可能な出力モードを返します。このプロパティは読み取り専用です。"
ms.assetid: 5ae62fae-7f13-480f-ba36-3fa72ff547bc
keywords:
- KSPROPERTY_AUDDECOUT_MODES ストリーミングメディアデバイス
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
ms.openlocfilehash: fcd8409e13d1c2558bcbf523d94f2a62a41460b8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842162"
---
# <a name="ksproperty_auddecout_modes"></a>KSPROPERTY\_\_モード


"\_\_" の KSK プロパティは、音声デコーダーの使用可能な出力モードを返します。

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
<td><p>DWORD</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、オーディオデコーダーがサポートするオーディオ出力モードのビットマスクを表す DWORD です。

<a name="remarks"></a>注釈
-------

プロパティ値には、 *Ksmedia .h*ヘッダーファイルで定義されている次の定数のビットごとの or を含めることができます。

<span id="KSAUDDECOUTMODE_STEREO_ANALOG"></span><span id="ksauddecoutmode_stereo_analog"></span>**KSK の\_ステレオ\_アナログ**  
は、出力がアナログステレオであることを示します。

<span id="KSAUDDECOUTMODE_PCM_51"></span><span id="ksauddecoutmode_pcm_51"></span>**KSK の\_PCM\_51**  
出力が PCM 5.1 チャネルデジタル内にあることを示します。

<span id="KSAUDDECOUTMODE_SPDIFF"></span><span id="ksauddecoutmode_spdiff"></span>**KSK\_の SPDIFF**  
出力が SPDIFF 形式の AC3 デジタルであることを示します。

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


[**KSK プロパティ\_\_\_モードになっています**](ksproperty-auddecout-cur-mode.md)

 

 






