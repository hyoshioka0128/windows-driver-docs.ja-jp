---
title: KSK プロパティ\_EXTXPORT\_入力\_シグナル\_モード
description: KSK プロパティ\_EXTXPORT\_入力\_SIGNAL\_MODE プロパティは、外部デバイスの現在の入力シグナルモードを設定または取得します。 たとえば、DV-SD/NTSC/PAL、DV-SL/NTSC/PAL、MPEG2-TS などです。
ms.assetid: 3af5c2fb-c7dc-4dfb-b66d-fc16091fa5ad
keywords:
- KSPROPERTY_EXTXPORT_INPUT_SIGNAL_MODE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTXPORT_INPUT_SIGNAL_MODE
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ad1ec005f0c3d8559586b14a932623a3447a87a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837951"
---
# <a name="ksproperty_extxport_input_signal_mode"></a>KSK プロパティ\_EXTXPORT\_入力\_シグナル\_モード


KSK プロパティ\_EXTXPORT\_入力\_SIGNAL\_MODE プロパティは、外部デバイスの現在の入力シグナルモードを設定または取得します。 たとえば、DV-SD/NTSC/PAL、DV-SL/NTSC/PAL、MPEG2-TS などです。

## <span id="ddk_ksproperty_extxport_input_signal_mode_ks"></span><span id="DDK_KSPROPERTY_EXTXPORT_INPUT_SIGNAL_MODE_KS"></span>


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

 

プロパティ値 (操作データ) は、外部トランスポートの現在の入力シグナルモードを指定する ULONG です。

<a name="remarks"></a>注釈
-------

EXTXPORT\_S 構造体\_KSK プロパティの**Signalmode**メンバーは、入力信号モードを指定します。

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

 

 






