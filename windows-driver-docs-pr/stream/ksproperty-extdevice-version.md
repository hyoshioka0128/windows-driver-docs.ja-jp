---
title: KSPROPERTY\_EXTDEVICE\_バージョン
description: KSPROPERTY\_EXTDEVICE\_バージョン プロパティは、外部のデバイスのバージョンを取得します。
ms.assetid: cb5133c9-b723-4d28-b591-8c65a8cc52a5
keywords:
- KSPROPERTY_EXTDEVICE_VERSION ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTDEVICE_VERSION
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8fc7f824f3237cc07c923e01017db8529a639192
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364048"
---
# <a name="kspropertyextdeviceversion"></a>KSPROPERTY\_EXTDEVICE\_バージョン


KSPROPERTY\_EXTDEVICE\_バージョン プロパティは、外部のデバイスのバージョンを取得します。

## <span id="ddk_ksproperty_extdevice_version_ks"></span><span id="DDK_KSPROPERTY_EXTDEVICE_VERSION_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565156" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565156)"><strong>KSPROPERTY_EXTDEVICE_S</strong></a></p></td>
<td><p>WCHAR 配列</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) には、外部のデバイスのバージョンが含まれる WCHAR 配列です。 配列は、自由な形式の文字列です。

<a name="remarks"></a>注釈
-------

**PawchString** 、KSPROPERTY のメンバー\_EXTDEVICE\_S 構造体には、外部のデバイスのバージョンがについて説明します。

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

[**KSPROPERTY\_EXTDEVICE\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565156)

 

 






