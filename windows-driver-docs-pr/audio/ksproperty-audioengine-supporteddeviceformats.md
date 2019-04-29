---
title: KSPROPERTY\_AUDIOENGINE\_SUPPORTEDDEVICEFORMATS
description: KSPROPERTY\_AUDIOENGINE\_SUPPORTEDDEVICEFORMATS プロパティ要求が、ハードウェアのオーディオ エンジンでサポートされているデバイスの形式を取得します。
ms.assetid: BF602B17-09E2-4003-95F8-CB45605EFA09
keywords:
- KSPROPERTY_AUDIOENGINE_SUPPORTEDDEVICEFORMATS オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOENGINE_SUPPORTEDDEVICEFORMATS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14f3ca98d9fc476975b35e30f57b3d40113ec2de
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332804"
---
# <a name="kspropertyaudioenginesupporteddeviceformats"></a>KSPROPERTY\_AUDIOENGINE\_SUPPORTEDDEVICEFORMATS


**KSPROPERTY\_AUDIOENGINE\_SUPPORTEDDEVICEFORMATS**プロパティ要求が、ハードウェアのオーディオ エンジンでサポートされているデバイスの形式を取得します。

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
<td align="left"><p>A <a href="https://msdn.microsoft.com/library/windows/hardware/ff563441" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563441)"> <strong>KSMULTIPLE_ITEM</strong> </a>のシーケンスに続く構造<a href="https://msdn.microsoft.com/library/windows/hardware/ff537095" data-raw-source="[&lt;strong&gt;KSDATAFORMAT_WAVEFORMATEX&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537095)"> <strong>KSDATAFORMAT_WAVEFORMATEX</strong> </a>構造体</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

**KSPROPERTY\_AUDIOENGINE\_SUPPORTEDDEVICEFORMATS**プロパティ要求を返します**状態\_成功**を正常に完了したことを示します. それ以外の場合、要求は、適切なエラー状態コードを返します。

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


[**KSDATAFORMAT\_WAVEFORMATEX**](https://msdn.microsoft.com/library/windows/hardware/ff537095)

[**KSMULTIPLE\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff563441)

[**KSPROPERTY\_AUDIOENGINE**](ksproperty-audioengine.md)

[**KSPROPERTY\_AUDIOENGINE\_VOLUMELEVEL**](ksproperty-audioengine-volumelevel.md)

 

 






