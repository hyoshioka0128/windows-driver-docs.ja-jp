---
title: KSPROPERTY\_チューナー\_モード
description: ユーザー モードのクライアントの使用、KSPROPERTY\_チューナー\_モード プロパティを取得または設定、アナログ テレビ、デジタル テレビ、FM AM などのデバイスのチューニング モードまたは DSS します。 このプロパティを実装する必要があります。
ms.assetid: 84df4030-3836-48de-be83-ecd749839081
keywords:
- KSPROPERTY_TUNER_MODE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TUNER_MODE
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e9df3e6ec8ac23a883b5d75a7a9dd2f5e2a09a8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570562"
---
# <a name="kspropertytunermode"></a>KSPROPERTY\_チューナー\_モード


ユーザー モードのクライアントの使用、KSPROPERTY\_チューナー\_モード プロパティを取得または設定、アナログ テレビ、デジタル テレビ、FM AM などのデバイスのチューニング モードまたは DSS します。 このプロパティを実装する必要があります。

## <span id="ddk_ksproperty_tuner_mode_ks"></span><span id="DDK_KSPROPERTY_TUNER_MODE_KS"></span>


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
<td><p>Pin</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565878" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_MODE_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565878)"><strong>KSPROPERTY_TUNER_MODE_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、チューナーの現在のチューニング モードを指定する ULONG です。

<a name="remarks"></a>コメント
-------

**モード**、KSPROPERTY のメンバー\_チューナー\_モード\_の構造をチューナーの現在のモードを指定します。

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

[**KSPROPERTY\_チューナー\_モード\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565878)

 

 






