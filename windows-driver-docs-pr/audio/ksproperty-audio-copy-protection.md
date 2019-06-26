---
title: KSPROPERTY\_オーディオ\_コピー\_保護
description: KSPROPERTY\_オーディオ\_コピー\_保護プロパティをオーディオ ストリームのコピー防止の状態を指定します。
ms.assetid: 68896bd4-9ffe-4632-a3b2-441b5d04208a
keywords:
- KSPROPERTY_AUDIO_COPY_PROTECTION オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_COPY_PROTECTION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 601da5beb0e302729882b6c7e9e0977d2fecae47
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391484"
---
# <a name="kspropertyaudiocopyprotection"></a>KSPROPERTY\_オーディオ\_コピー\_保護


KSPROPERTY\_オーディオ\_コピー\_保護プロパティをオーディオ ストリームのコピー防止の状態を指定します。

## <span id="ddk_ksproperty_audio_copy_protection_ks"></span><span id="DDK_KSPROPERTY_AUDIO_COPY_PROTECTION_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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
<th align="left">取得</th>
<th align="left">設定</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>〇</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_copy_protection" data-raw-source="[&lt;strong&gt;KSAUDIO_COPY_PROTECTION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_copy_protection)"><strong>KSAUDIO_COPY_PROTECTION</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は型 KSAUDIO の構造体\_コピー\_保護します。 構造体かどうか、ストリームは著作権は; を指定しますまた、ストリームが元のストリームまたは元のストリームのコピーがあるかどうかを指定します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_コピー\_保護プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

KSPROPERTY\_オーディオ\_コピー\_保護プロパティは、シリアル コピー管理システム (SCMS) するような保護スキームをサポートするオーディオ デバイスのプロパティ。 プロパティは、デジタルのストリームが著作権によって保護されているかどうかと、元のストリームとコピーであるかを示します。

SCMS には、オーディオ コンテンツの保護の 3 つのレベルを指定できます。

**レベル 0:** 無制限の著作権が不足していますかを著作権情報をアサートしませんストリームのコピー。

**レベル 1:** 第 1 世代のストリームへのコピーの制限。 ユーザーは、元の著作権で保護されたストリームのコピーを作成できますが、ストリームのコピーのコピーを作成することはできません。

**レベル 2:** ストリームのすべてコピーするありません。

KSPROPERTY\_オーディオ\_コピー\_保護プロパティから独立した関連付けられていない機能の実装に[デジタル著作権管理 (DRM)](https://docs.microsoft.com/windows-hardware/drivers/audio/digital-rights-management)と Windows のセキュリティで保護されたオーディオのパス (SAP)メディア。 SAP の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

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
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

[**KSAUDIO\_コピー\_保護**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_copy_protection)

 

 






