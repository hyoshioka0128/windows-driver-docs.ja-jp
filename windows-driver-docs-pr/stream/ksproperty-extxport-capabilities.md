---
title: KSPROPERTY\_EXTXPORT\_機能
description: KSPROPERTY\_EXTXPORT\_機能プロパティは、外部のデバイスのトランスポートに固有の機能を取得します。
ms.assetid: 5394d05c-0c3e-4413-a61e-21445117a350
keywords:
- KSPROPERTY_EXTXPORT_CAPABILITIES ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTXPORT_CAPABILITIES
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7452cfc1ee0cb2755252cd952a4dabde8fe36351
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354853"
---
# <a name="kspropertyextxportcapabilities"></a>KSPROPERTY\_EXTXPORT\_機能


KSPROPERTY\_EXTXPORT\_機能プロパティは、外部のデバイスのトランスポートに固有の機能を取得します。

## <span id="ddk_ksproperty_extxport_capabilities_ks"></span><span id="DDK_KSPROPERTY_EXTXPORT_CAPABILITIES_KS"></span>


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
<td><p>X</p></td>
<td><p>デバイス</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_extxport_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_extxport_s)"><strong>KSPROPERTY_EXTXPORT_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、外部のトランスポートの機能を指定する ULONG です。

<a name="remarks"></a>注釈
-------

**機能**、KSPROPERTY のメンバー\_EXTXPORT\_構造がトランスポートに固有の機能について説明します。

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

[**KSPROPERTY\_EXTXPORT\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_extxport_s)

 

 






