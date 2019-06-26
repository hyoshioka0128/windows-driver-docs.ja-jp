---
title: KSPROPERTY\_SYSAUDIO\_アタッチ\_仮想\_ソース
description: KSPROPERTY\_SYSAUDIO\_アタッチ\_仮想\_ソース プロパティは、仮想のオーディオ デバイスの暗証番号 (pin) のインスタンスに仮想のソースをアタッチします。
ms.assetid: cb677eb2-b58d-4f36-b729-d0bfc06db07f
keywords:
- KSPROPERTY_SYSAUDIO_ATTACH_VIRTUAL_SOURCE オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_SYSAUDIO_ATTACH_VIRTUAL_SOURCE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b095a7e805e06a9d0af3c6654eec4ee5035dc5de
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358719"
---
# <a name="kspropertysysaudioattachvirtualsource"></a>KSPROPERTY\_SYSAUDIO\_アタッチ\_仮想\_ソース


KSPROPERTY\_SYSAUDIO\_アタッチ\_仮想\_ソース プロパティは、仮想のオーディオ デバイスの暗証番号 (pin) のインスタンスに仮想のソースをアタッチします。

## <span id="ddk_ksproperty_sysaudio_attach_virtual_source_ks"></span><span id="DDK_KSPROPERTY_SYSAUDIO_ATTACH_VIRTUAL_SOURCE_KS"></span>


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
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-sysaudio_attach_virtual_source" data-raw-source="[&lt;strong&gt;SYSAUDIO_ATTACH_VIRTUAL_SOURCE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-sysaudio_attach_virtual_source)"><strong>SYSAUDIO_ATTACH_VIRTUAL_SOURCE</strong></a></p></td>
<td align="left"><p>なし</p></td>
</tr>
</tbody>
</table>

 

プロパティ記述子 (インスタンス データ) は、型 SYSAUDIO の構造\_アタッチ\_仮想\_プロパティと仮想のソースのインデックスを指定するソース。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_SYSAUDIO\_アタッチ\_仮想\_ソース プロパティの要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

このプロパティは、仮想のソースを仮想のオーディオ デバイスの暗証番号 (pin) のインスタンスにアタッチします。 詳細については、次を参照してください。 [ **KSPROPERTY\_SYSAUDIO\_作成\_仮想\_ソース**](ksproperty-sysaudio-create-virtual-source.md)します。

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
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**SYSAUDIO\_アタッチ\_仮想\_ソース**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-sysaudio_attach_virtual_source)

[**KSPROPERTY\_SYSAUDIO\_作成\_仮想\_ソース**](ksproperty-sysaudio-create-virtual-source.md)

 

 






