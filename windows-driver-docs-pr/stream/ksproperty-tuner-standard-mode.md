---
title: KSPROPERTY\_チューナー\_標準\_モード
description: KSPROPERTY\_チューナー\_標準\_モード プロパティは、ドライバーが、チューニング自体の信号から標準のチューナーを自動的に検出するデバイスを設定できるかどうかを示すブール値を取得します。 このプロパティは、必要に応じて実装できます。
ms.assetid: 9c374778-20fd-427a-864f-f57ec14add07
keywords:
- KSPROPERTY_TUNER_STANDARD_MODE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TUNER_STANDARD_MODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7441092ad15848aa48f16cfc30e805f2552a88a9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355967"
---
# <a name="kspropertytunerstandardmode"></a>KSPROPERTY\_チューナー\_標準\_モード


KSPROPERTY\_チューナー\_標準\_モード プロパティは、ドライバーが、チューニング自体の信号から標準のチューナーを自動的に検出するデバイスを設定できるかどうかを示すブール値を取得します。 このプロパティは、必要に応じて実装できます。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_standard_mode_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_STANDARD_MODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_standard_mode_s)"><strong>KSPROPERTY_TUNER_STANDARD_MODE_S</strong></a></p></td>
<td><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、チューニングのデバイスが自体の信号から、チューナーの標準を自動的に検出するかどうかを示すブール値。

<a name="remarks"></a>注釈
-------

詳細については、KSPROPERTY\_チューナー\_標準\_モード プロパティを使用してを参照してください[検出チューナー標準](https://docs.microsoft.com/windows-hardware/drivers/stream/detecting-tuner-standards)。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows Vista およびそれ以降のバージョンのオペレーティング システムで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY\_チューナー\_標準**](ksproperty-tuner-standard.md)

[**KSPROPERTY\_チューナー\_標準\_モード\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_standard_mode_s)

 

 






