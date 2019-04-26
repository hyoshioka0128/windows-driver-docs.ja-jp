---
title: KSPROPERTY\_チューナー\_キャップ
description: KSPROPERTY\_チューナー\_CAPS プロパティが、チューナーの基本的な機能について説明します。 このプロパティを実装する必要があります。
ms.assetid: 70255053-d241-44ca-ba24-cfc442629ab3
keywords:
- KSPROPERTY_TUNER_CAPS ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TUNER_CAPS
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ffe9f65fb1c54bdb8f016cb7a8374ce350f8d2a0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355851"
---
# <a name="kspropertytunercaps"></a>KSPROPERTY\_チューナー\_キャップ


KSPROPERTY\_チューナー\_CAPS プロパティが、チューナーの基本的な機能について説明します。 このプロパティを実装する必要があります。

## <span id="ddk_ksproperty_tuner_caps_ks"></span><span id="DDK_KSPROPERTY_TUNER_CAPS_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565828" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_CAPS_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565828)"><strong>KSPROPERTY_TUNER_CAPS_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、ストリーミングのミニドライバーでサポートされるチューニング モードを指定する LONG が。

<a name="remarks"></a>注釈
-------

**ModesSupported** 、KSPROPERTY のメンバー\_チューナー\_CAP\_構造がビデオ キャプチャ ミニドライバーでサポートされるチューニング モードを示します。

1 つのチューニング デバイスがデジタル テレビ、アナログ テレビ、AM のチューニングをサポートする場合があります/FM ラジオとデジタル サテライト システム (DSS)。

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

[**KSPROPERTY\_チューナー\_CAP\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565828)

[**KSPROPERTY\_チューナー\_モード\_キャップ**](ksproperty-tuner-mode-caps.md)

 

 






