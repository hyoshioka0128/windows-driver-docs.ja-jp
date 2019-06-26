---
title: KSPROPERTY\_ストリーム\_TIMEFORMAT
description: KSPROPERTY\_ストリーム\_TIMEFORMAT プロパティを使用して、特定の暗証番号 (pin) 接続で使用される時刻形式を取得します。
ms.assetid: bf8c32b2-401f-4f89-bcca-97a07c50cc45
keywords:
- KSPROPERTY_STREAM_TIMEFORMAT ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_STREAM_TIMEFORMAT
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c66ce9b849197e58e4a9a1c3457d85a4916ef423
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368842"
---
# <a name="kspropertystreamtimeformat"></a>KSPROPERTY\_ストリーム\_TIMEFORMAT


KSPROPERTY\_ストリーム\_TIMEFORMAT プロパティを使用して、特定の暗証番号 (pin) 接続で使用される時刻形式を取得します。

## <span id="ddk_ksproperty_stream_timeformat_ks"></span><span id="DDK_KSPROPERTY_STREAM_TIMEFORMAT_KS"></span>


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
<th>取得</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>〇</p></td>
<td><p>いいえ</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>GUID</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

プロパティは、接続に使用して、プレゼンテーション時間とエクステントの形式を示す時間形式を指定する GUID を返します。 定義されている時刻の形式は、DirectShow によって定義されているものに対応します。

KSPROPERTY\_ストリーム\_TIMEFORMAT 率、プレゼンテーション時間/エクステント、pin をサポートする場合に実装する必要がありますまたは低下プロパティをスキップする省略可能なプロパティは、(これらのプロパティの詳細についてを参照してください[品質管理](https://docs.microsoft.com/windows-hardware/drivers/stream/quality-management))。 これにより、クライアントを接続し、使用率、プレゼンテーション時間/エクステント、タイムスタンプ情報の形式の使用時間形式を特定し、パフォーマンス低下の操作をスキップできます。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ks.h (Ks.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

 

 






