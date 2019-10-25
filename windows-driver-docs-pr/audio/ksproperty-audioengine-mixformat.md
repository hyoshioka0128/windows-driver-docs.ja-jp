---
title: KSK プロパティ\_AUDIOENGINE\_MIXFORMAT
description: KSK プロパティ\_AUDIOENGINE\_MIXFORMAT property 要求は、ハードウェアオーディオエンジンのミキサーの設定を取得します。
ms.assetid: 12353E72-1092-44B4-861A-90C198237670
keywords:
- KSPROPERTY_AUDIOENGINE_MIXFORMAT オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOENGINE_MIXFORMAT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ecbb3c9f68a494f6054bc0c9569ee4150cd460d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830896"
---
# <a name="ksproperty_audioengine_mixformat"></a>KSK プロパティ\_AUDIOENGINE\_MIXFORMAT


**Ksk プロパティ\_AUDIOENGINE\_MIXFORMAT** property 要求は、ハードウェアオーディオエンジンのミキサーの設定を取得します。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_waveformatex" data-raw-source="[&lt;strong&gt;KSDATAFORMAT_WAVEFORMATEX&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_waveformatex)"><strong>KSDATAFORMAT_WAVEFORMATEX</strong></a></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

**Ksk プロパティ\_AUDIOENGINE\_MIXFORMAT** property 要求は、正常に完了したことを示す**ステータス\_成功**を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

また、任意の時点のオーディオエンジンノードに設定されているミックス形式は、オフロードピンファクトリでもサポートされている必要があります。

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


[**KSDATAFORMAT\_WAVEFORMATEX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_waveformatex)

[**KSK プロパティ\_AUDIOENGINE**](ksproperty-audioengine.md)

 

 






