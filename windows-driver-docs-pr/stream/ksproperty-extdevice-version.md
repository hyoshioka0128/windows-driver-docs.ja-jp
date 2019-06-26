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
ms.openlocfilehash: af94fe725d7143020cd75419c6e821e77bf2b8bd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354869"
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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_extdevice_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_extdevice_s)"><strong>KSPROPERTY_EXTDEVICE_S</strong></a></p></td>
<td><p>WCHAR 配列</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) には、外部のデバイスのバージョンが含まれる WCHAR 配列です。 配列は、自由な形式の文字列です。

<a name="remarks"></a>注釈
-------

**PawchString** 、KSPROPERTY のメンバー\_EXTDEVICE\_S 構造体には、外部のデバイスのバージョンがについて説明します。

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

[**KSPROPERTY\_EXTDEVICE\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_extdevice_s)

 

 






