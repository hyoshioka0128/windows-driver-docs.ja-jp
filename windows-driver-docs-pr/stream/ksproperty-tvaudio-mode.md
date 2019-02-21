---
title: KSPROPERTY\_TVAUDIO\_モード
description: KSPROPERTY\_TVAUDIO\_モード プロパティは、デバイスのオーディオ モードを設定します。 このプロパティを実装する必要があります。
ms.assetid: ef2db4b9-307f-4f70-8c9f-1344420c8cba
keywords:
- KSPROPERTY_TVAUDIO_MODE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TVAUDIO_MODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5905d194337034c9b1bb46b9cdb817d87289812
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527708"
---
# <a name="kspropertytvaudiomode"></a>KSPROPERTY\_TVAUDIO\_モード


KSPROPERTY\_TVAUDIO\_モード プロパティは、デバイスのオーディオ モードを設定します。 このプロパティを実装する必要があります。

## <span id="ddk_ksproperty_tvaudio_mode_ks"></span><span id="DDK_KSPROPERTY_TVAUDIO_MODE_KS"></span>


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
<td><p>〇</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565953" data-raw-source="[&lt;strong&gt;KSPROPERTY_TVAUDIO_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565953)"><strong>KSPROPERTY_TVAUDIO_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、モードを指定する、現在テレビ オーディオ ステレオまたはモノラル オーディオおよび言語設定など ULONG。

<a name="remarks"></a>注釈
-------

**モード**、KSPROPERTY のメンバー\_TVAUDIO\_の構造は、オーディオ モードを指定します。

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

[**KSPROPERTY\_TVAUDIO\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565953)

 

 






