---
title: KSK プロパティ\_AUDIOENGINE\_バッファー\_サイズ\_範囲
description: KSK プロパティ\_AUDIOENGINE\_BUFFER\_SIZE\_RANGE プロパティは、特定のデータ形式に対してハードウェアオーディオエンジンがサポートできるバッファーの最小サイズと最大サイズを示します。このサイズは、インスタンスが呼び出されたときに指定されます。 バッファーサイズはバイト単位で指定します。
ms.assetid: 6A5DF24C-A328-4814-A410-2B1E13402A2B
keywords:
- KSPROPERTY_AUDIOENGINE_BUFFER_SIZE_RANGE オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOENGINE_BUFFER_SIZE_RANGE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e557bbb6f36e2b8904f29353a62ee3eabffda19
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830925"
---
# <a name="ksproperty_audioengine_buffer_size_range"></a>KSK プロパティ\_AUDIOENGINE\_バッファー\_サイズ\_範囲


**Ksk プロパティ\_AUDIOENGINE\_buffer\_size\_RANGE**プロパティは、特定のデータ形式に対してハードウェアオーディオエンジンがサポートできるバッファーの最小サイズと最大サイズを示します。このサイズは、インスタンスが呼び出されたときに指定されます。 バッファーサイズはバイト単位で指定します。

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
<td align="left"><p>必須ではない</p></td>
<td align="left"><p>フィルターを使用したノード</p></td>
<td align="left"><p>KSP_NODE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagksaudioengine_buffer_size_range" data-raw-source="[&lt;strong&gt;KSAUDIOENGINE_BUFFER_SIZE_RANGE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagksaudioengine_buffer_size_range)"><strong>KSAUDIOENGINE_BUFFER_SIZE_RANGE</strong></a></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

**Ksk プロパティ\_AUDIOENGINE\_BUFFER\_SIZE\_RANGE**プロパティ要求は、正常に完了したことを示す**ステータス\_成功**を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

呼び出し元は、 **Ksk プロパティ\_AUDIOENGINE\_BUFFER\_SIZE\_RANGE**プロパティを呼び出す前に、呼び出し元が[**KSDATAFORMAT\_WAVEFORMATEX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_waveformatex)構造体のフィールドに入力することに注意してください。 そのため、 **Ksk プロパティ\_AUDIOENGINE\_BUFFER\_SIZE\_RANGE**が呼び出されると、オーディオドライバーは KSP\_ノードを受け取り、その後に、呼び出し元から**KSDATAFORMAT\_WAVEFORMATEX**構造体が埋め込まれます。 ドライバーは、この構造体のデータ形式情報を使用して、指定されたデータ形式に合わせて最小バッファーサイズと最大バッファーサイズを決定します。 このプロパティが正常に呼び出されると、カーネルストリーミング (KS) フィルターは、 [**KSAUDIOENGINE\_BUFFER\_SIZE\_RANGE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagksaudioengine_buffer_size_range)構造体の**minbufferbytes**および**maxbufferbytes**フィールドに入力します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 8</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**KSAUDIOENGINE\_BUFFER\_SIZE\_範囲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagksaudioengine_buffer_size_range)

[**KSDATAFORMAT\_WAVEFORMATEX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_waveformatex)

[**KSK プロパティ\_AUDIOENGINE**](ksproperty-audioengine.md)

 

 






