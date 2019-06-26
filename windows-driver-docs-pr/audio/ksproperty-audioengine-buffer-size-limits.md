---
title: KSPROPERTY\_AUDIOENGINE\_バッファー\_サイズ\_範囲
description: KSPROPERTY\_AUDIOENGINE\_バッファー\_サイズ\_範囲プロパティになったときにインスタンスを指定したデータ形式については、ハードウェアのオーディオ エンジンがサポートできるバッファーの最小値と最大サイズを示しますと呼ばれる。 バッファー サイズはバイト単位で指定します。
ms.assetid: 6A5DF24C-A328-4814-A410-2B1E13402A2B
keywords:
- KSPROPERTY_AUDIOENGINE_BUFFER_SIZE_RANGE オーディオ デバイス
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
ms.openlocfilehash: 622430152078bfd316c54fa07b66ca101d8bc36d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358858"
---
# <a name="kspropertyaudioenginebuffersizerange"></a>KSPROPERTY\_AUDIOENGINE\_バッファー\_サイズ\_範囲


**KSPROPERTY\_AUDIOENGINE\_バッファー\_サイズ\_範囲**プロパティは、特定のデータ、ハードウェアのオーディオ エンジンがサポートできるバッファーの最小値と最大サイズを示します。呼び出されると、インスタンスで、フォーマットします。 バッファー サイズはバイト単位で指定します。

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
<td align="left"><p>X</p></td>
<td align="left"><p>フィルターを使用してノード</p></td>
<td align="left"><p>KSP_NODE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_tagksaudioengine_buffer_size_range" data-raw-source="[&lt;strong&gt;KSAUDIOENGINE_BUFFER_SIZE_RANGE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_tagksaudioengine_buffer_size_range)"><strong>KSAUDIOENGINE_BUFFER_SIZE_RANGE</strong></a></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

A **KSPROPERTY\_AUDIOENGINE\_バッファー\_サイズ\_範囲**プロパティ要求を返します**状態\_成功**ことを示しますそれが正常に完了しました。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

呼び出し元を呼び出す前に注意することが重要、 **KSPROPERTY\_AUDIOENGINE\_バッファー\_サイズ\_範囲**のフィールドのプロパティ、呼び出し元の入力を[**KSDATAFORMAT\_WAVEFORMATEX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdataformat_waveformatex)構造体。 したがって**KSPROPERTY\_AUDIOENGINE\_バッファー\_サイズ\_範囲**を呼び出すと、オーディオ ドライバー、KSP の受信\_、入力では、ノードの後に**KSDATAFORMAT\_WAVEFORMATEX**呼び出し元からの構造体。 ドライバーは、指定したデータ形式を対応するために最小および最大バッファー サイズを決定するのに、この構造体で、データの書式情報を使用します。 このプロパティに呼び出しの成功時に (KS) フィルターをストリーミングし、カーネルの設定、 **MinBufferBytes**と**MaxBufferBytes**のフィールド、 [ **KSAUDIOENGINE\_バッファー\_サイズ\_範囲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_tagksaudioengine_buffer_size_range)構造体。

<a name="requirements"></a>必要条件
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

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSAUDIOENGINE\_バッファー\_サイズ\_範囲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_tagksaudioengine_buffer_size_range)

[**KSDATAFORMAT\_WAVEFORMATEX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdataformat_waveformatex)

[**KSPROPERTY\_AUDIOENGINE**](ksproperty-audioengine.md)

 

 






