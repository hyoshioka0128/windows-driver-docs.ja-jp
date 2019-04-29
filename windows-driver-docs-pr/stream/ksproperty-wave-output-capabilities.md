---
title: KSPROPERTY\_WAVE\_出力\_機能
description: KSPROPERTY\_WAVE\_出力\_機能プロパティは、wave デバイスの波の出力の機能を返します。
ms.assetid: 9e5e8ed1-0d08-45b7-b683-df7ce4424c26
keywords:
- KSPROPERTY_WAVE_OUTPUT_CAPABILITIES ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_WAVE_OUTPUT_CAPABILITIES
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6815546e0e7328dd18f23ba95ff7c920c0777d0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329962"
---
# <a name="kspropertywaveoutputcapabilities"></a>KSPROPERTY\_WAVE\_出力\_機能


KSPROPERTY\_WAVE\_出力\_機能プロパティは、wave デバイスの波の出力の機能を返します。

## <span id="ddk_ksproperty_wave_output_capabilities_ks"></span><span id="DDK_KSPROPERTY_WAVE_OUTPUT_CAPABILITIES_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567248" data-raw-source="[&lt;strong&gt;KSWAVE_OUTPUT_CAPABILITIES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567248)"><strong>KSWAVE_OUTPUT_CAPABILITIES</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、KSWAVE\_出力\_wave デバイス、オーディオ チャンネル、サンプルごとのビットの範囲の範囲の最大数の出力の機能を説明する機能の構造体サンプリング周波数、接続数の合計とアクティブです。

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
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSWAVE\_出力\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff567248)

 

 






