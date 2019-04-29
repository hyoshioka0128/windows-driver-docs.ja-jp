---
title: KSPROPERTY\_SOUNDDETECTOR\_SUPPORTEDPATTERNS
description: KSPROPERTY\_SOUNDDETECTOR\_SUPPORTEDPATTERNS プロパティがサポートされているパターンの種類を識別する Guid の一覧を取得するために使用します。
ms.assetid: 8D840204-ADE8-4146-B88C-C0750B8FC33A
keywords:
- KSPROPERTY_SOUNDDETECTOR_SUPPORTEDPATTERNS オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_SOUNDDETECTOR_SUPPORTEDPATTERNS
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6646e168cfa0b4ff0c7b10150516598a56468429
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332634"
---
# <a name="kspropertysounddetectorsupportedpatterns"></a>KSPROPERTY\_SOUNDDETECTOR\_SUPPORTEDPATTERNS


**KSPROPERTY\_SOUNDDETECTOR\_SUPPORTEDPATTERNS**プロパティがサポートされているパターンの種類を識別する Guid の一覧を取得するために使用します。

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
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563441" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563441)"><strong>KSMULTIPLE_ITEM</strong></a></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

プロパティの値は、 [ **KSMULTIPLE\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff563441)構造が続く一連の Guid。

<a name="remarks"></a>注釈
-------

GUID のパターンでは、これらの特性があります。

-   OEM が生成されます。

-   オペレーティング システム クラス id (CLSID) として対応ドライバーと対話するのにために使用する OEM DLL COM クラスをインスタンス化に使用します。

-   OEM で定義されたパターンのデータの形式を意味します。

-   OEM が定義されている結果のデータの形式を意味します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>サポートされている最小のクライアント</p></td>
<td align="left"><p>Windows 10</p></td>
</tr>
<tr class="even">
<td align="left"><p>サポートされている最小のサーバー</p></td>
<td align="left"><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff564262)

[**KSMULTIPLE\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff563441)

 

 






