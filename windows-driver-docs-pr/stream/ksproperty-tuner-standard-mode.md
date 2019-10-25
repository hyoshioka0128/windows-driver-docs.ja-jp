---
title: KSK プロパティ\_チューナー\_標準\_モード
description: KSK プロパティ\_チューナー\_標準\_モードプロパティは、ドライバーがチューニングデバイスを設定して、自動的にチューナー標準を信号自体から検出するかどうかを示すブール値を取得します。 このプロパティは、必要に応じて実装できます。
ms.assetid: 9c374778-20fd-427a-864f-f57ec14add07
keywords:
- KSPROPERTY_TUNER_STANDARD_MODE ストリーミングメディアデバイス
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
ms.openlocfilehash: e6c497d7f5c9bbfc053035b2ad2b38943d6ede4b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837902"
---
# <a name="ksproperty_tuner_standard_mode"></a>KSK プロパティ\_チューナー\_標準\_モード


KSK プロパティ\_チューナー\_標準\_モードプロパティは、ドライバーがチューニングデバイスを設定して、自動的にチューナー標準を信号自体から検出するかどうかを示すブール値を取得します。 このプロパティは、必要に応じて実装できます。

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
<th>セット</th>
<th>的を絞る</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>はい</p></td>
<td><p>いいえ</p></td>
<td><p>ピン</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_standard_mode_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_STANDARD_MODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_standard_mode_s)"><strong>KSPROPERTY_TUNER_STANDARD_MODE_S</strong></a></p></td>
<td><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、チューニングデバイスが、信号自体からチューナー標準を自動的に検出できるかどうかを示すブール値です。

<a name="remarks"></a>解説
-------

KSK プロパティ\_チューナー\_標準\_モードプロパティの使用方法の詳細については、「[チューナー標準の検出](https://docs.microsoft.com/windows-hardware/drivers/stream/detecting-tuner-standards)」を参照してください。

<a name="requirements"></a>前提条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows Vista 以降のバージョンのオペレーティングシステムで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>ヘッダー</p></td>
<td>Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSK プロパティ\_チューナー\_STANDARD**](ksproperty-tuner-standard.md)

[**KSK プロパティ\_チューナー\_標準\_モード\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_standard_mode_s)

 

 






