---
title: KSPROPERTY\_TVAUDIO\_現在\_利用可能な\_モード
description: KSPROPERTY\_TVAUDIO\_現在\_利用可能な\_モード プロパティは、デバイスで利用可能なテレビ オーディオ モードを取得します。 このプロパティを実装する必要があります。
ms.assetid: 9c98771a-7a41-469d-a441-da5c1ac5a697
keywords:
- KSPROPERTY_TVAUDIO_CURRENTLY_AVAILABLE_MODES ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TVAUDIO_CURRENTLY_AVAILABLE_MODES
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a4bd1450090346b39c9ff22802c9cb2f2a8c921
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358215"
---
# <a name="kspropertytvaudiocurrentlyavailablemodes"></a>KSPROPERTY\_TVAUDIO\_現在\_利用可能な\_モード


KSPROPERTY\_TVAUDIO\_現在\_利用可能な\_モード プロパティは、デバイスで利用可能なテレビ オーディオ モードを取得します。 このプロパティを実装する必要があります。

## <span id="ddk_ksproperty_tvaudio_currently_available_modes_ks"></span><span id="DDK_KSPROPERTY_TVAUDIO_CURRENTLY_AVAILABLE_MODES_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565953" data-raw-source="[&lt;strong&gt;KSPROPERTY_TVAUDIO_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565953)"><strong>KSPROPERTY_TVAUDIO_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、現在使用できるテレビ オーディオ モード、ステレオまたはモノラル オーディオおよび複数の言語設定などを指定する ULONG。

<a name="remarks"></a>注釈
-------

**モード**、KSPROPERTY のメンバー\_TVAUDIO\_の構造は、オーディオ モードを指定します。 KS のビットごとの or 演算が含まれている\_TVAUDIO\_モード\_\*情報が要求された時点で、デバイスでサポートされるモードを示すフラグ。

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

[**KSPROPERTY\_TVAUDIO\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565953)

 

 






