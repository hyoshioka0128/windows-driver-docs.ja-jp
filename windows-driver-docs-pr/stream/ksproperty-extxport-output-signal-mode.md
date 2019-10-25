---
title: KSK プロパティ\_EXTXPORT\_出力\_シグナル\_モード
description: KSK プロパティ\_EXTXPORT\_OUTPUT\_SIGNAL\_MODE プロパティは、外部デバイスの出力シグナルモードを設定または取得します。 たとえば、DV-SD/NTSC/PAL、DV-SL/NTSC/PAL、MPEG2-TS などです。
ms.assetid: 9cd1bf2a-c241-491a-af22-5cf7b654169d
keywords:
- KSPROPERTY_EXTXPORT_OUTPUT_SIGNAL_MODE ストリーミングメディアデバイス
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
ms.openlocfilehash: ace92bc093569f2a6f31a638c113b24f250155d9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838059"
---
# <a name="ksproperty_extxport_output_signal_mode"></a>KSK プロパティ\_EXTXPORT\_出力\_シグナル\_モード


KSK プロパティ\_EXTXPORT\_OUTPUT\_SIGNAL\_MODE プロパティは、外部デバイスの出力シグナルモードを設定または取得します。 たとえば、DV-SD/NTSC/PAL、DV-SL/NTSC/PAL、MPEG2-TS などです。

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
<th>[購入]</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
<td><p>デバイス</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s)"><strong>KSPROPERTY_EXTXPORT_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、外部トランスポートの現在の出力シグナルモードを指定する ULONG です。

<a name="remarks"></a>注釈
-------

EXTXPORT\_S 構造体\_KSK プロパティの**Signalmode**メンバーは、出力シグナルモードを指定します。

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
<td>Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSK プロパティ\_EXTXPORT\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s)

 

 






