---
title: KSK プロパティ\_AUDIO\_コピー\_保護
description: KSK プロパティ\_AUDIO\_COPY\_PROTECTION プロパティは、オーディオストリームのコピー防止の状態を指定します。
ms.assetid: 68896bd4-9ffe-4632-a3b2-441b5d04208a
keywords:
- KSPROPERTY_AUDIO_COPY_PROTECTION オーディオデバイス
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
ms.openlocfilehash: e07a90b94148bad35114a5d6be35d121b08fd7c7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831059"
---
# <a name="ksproperty_audio_copy_protection"></a>KSK プロパティ\_AUDIO\_コピー\_保護


KSK プロパティ\_AUDIO\_COPY\_PROTECTION プロパティは、オーディオストリームのコピー防止の状態を指定します。

## <span id="ddk_ksproperty_audio_copy_protection_ks"></span><span id="DDK_KSPROPERTY_AUDIO_COPY_PROTECTION_KS"></span>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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
<th align="left">[購入]</th>
<th align="left">設定</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>[はい]</p></td>
<td align="left"><p>[はい]</p></td>
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_copy_protection" data-raw-source="[&lt;strong&gt;KSAUDIO_COPY_PROTECTION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_copy_protection)"><strong>KSAUDIO_COPY_PROTECTION</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、KSK AUDIO\_COPY\_PROTECTION 型の構造体です。 構造体は、ストリームに著作権があるかどうかを指定します。また、ストリームが元のストリームであるか、元のストリームのコピーであるかも指定します。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

\_\_コピー\_保護プロパティ要求\_KSK プロパティは、正常に完了したことを示すステータス成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

KSK プロパティ\_AUDIO\_COPY\_PROTECTION プロパティは、シリアルコピー管理システム (SCMS) と同様の保護スキームをサポートするオーディオデバイスのプロパティです。 プロパティは、デジタルストリームが著作権によって保護されているかどうか、および元のストリームまたはコピーかどうかを示します。

SCMS は、次の3つのレベルのオーディオコンテンツ保護を提供できます。

**レベル 0:** 著作権が不足している、または著作権をアサートしていないストリームの無制限のコピー。

**レベル 1:** 最初の生成ストリームへのコピーの制限。 ユーザーは、元の著作権を持つストリームのコピーを作成できますが、ストリームのコピーを作成することはできません。

**レベル 2:** すべてのストリームでコピーすることはできません。

KSK プロパティ\_AUDIO\_COPY\_PROTECTION プロパティは、[デジタル Rights Management (DRM)](https://docs.microsoft.com/windows-hardware/drivers/audio/digital-rights-management)と Windows Media のセキュリティで保護されたオーディオパス (SAP) の実装とは別のものです。 SAP の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

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
<td align="left">Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

[**KSAUDIO\_コピー\_保護**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_copy_protection)

 

 






