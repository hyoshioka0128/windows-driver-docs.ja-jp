---
title: KSPROPERTY\_EXTDEVICE\_ID
description: KSPROPERTY\_EXTDEVICE\_ID プロパティは、外部のデバイスの汎用化されたシステムの id を取得します。
ms.assetid: ff0f37f8-55a8-45b9-8cf1-81e2cc5ac3aa
keywords:
- KSPROPERTY_EXTDEVICE_ID ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTDEVICE_ID
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c0cdefc40de4f831240723d0ec68528cad14fd0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532734"
---
# <a name="kspropertyextdeviceid"></a>KSPROPERTY\_EXTDEVICE\_ID


KSPROPERTY\_EXTDEVICE\_ID プロパティは、外部のデバイスの汎用化されたシステムの id を取得します。

## <span id="ddk_ksproperty_extdevice_id_ks"></span><span id="DDK_KSPROPERTY_EXTDEVICE_ID_KS"></span>


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
<td><p>DWORD の配列</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、外部のデバイスの一意のノード Id を指定する DWORD 配列です。

<a name="remarks"></a>注釈
-------

**NodeUniqueID** 、KSPROPERTY のメンバー\_EXTDEVICE\_構造を指定、外部のデバイスの一意のノード id。

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

 

 






