---
title: KSPROPERTY\_EXTXPORT\_出力\_信号\_モード
description: KSPROPERTY\_EXTXPORT\_出力\_信号\_モード プロパティを設定または外部のデバイスの出力シグナル モードを取得します。 たとえば DV-SD/NTSC と PAL、DV-SL/NTSC と PAL、MPEG2 TS などです。
ms.assetid: 9cd1bf2a-c241-491a-af22-5cf7b654169d
keywords:
- KSPROPERTY_EXTXPORT_OUTPUT_SIGNAL_MODE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTXPORT_OUTPUT_SIGNAL_MODE
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 873a1ed0aea3a3b67239c44564660cfa79be43f4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573690"
---
# <a name="kspropertyextxportoutputsignalmode"></a>KSPROPERTY\_EXTXPORT\_出力\_信号\_モード


KSPROPERTY\_EXTXPORT\_出力\_信号\_モード プロパティを設定または外部のデバイスの出力シグナル モードを取得します。 たとえば DV-SD/NTSC と PAL、DV-SL/NTSC と PAL、MPEG2 TS などです。

## <span id="ddk_ksproperty_extxport_output_signal_mode_ks"></span><span id="DDK_KSPROPERTY_EXTXPORT_OUTPUT_SIGNAL_MODE_KS"></span>


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
<th>Set</th>
<th>移行先</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>デバイス</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565167" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565167)"><strong>KSPROPERTY_EXTXPORT_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、外部のトランスポートの現在の出力シグナル モードを指定する ULONG です。

<a name="remarks"></a>コメント
-------

**SignalMode** 、KSPROPERTY のメンバー\_EXTXPORT\_構造が出力信号のモードを指定します。

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
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_EXTXPORT\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565167)

 

 






