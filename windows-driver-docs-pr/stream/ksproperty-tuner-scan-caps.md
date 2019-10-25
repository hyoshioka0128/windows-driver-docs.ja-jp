---
title: KSK プロパティ\_チューナー\_スキャン\_CAPS
description: KSK プロパティ\_チューナー\_SCAN\_CAPS プロパティは、デバイスがサポートするネットワークの種類など、チューニングデバイスのスキャン機能について説明します。
ms.assetid: 339d5f6b-81ac-419e-9821-a7f1642e1aa8
keywords:
- KSPROPERTY_TUNER_SCAN_CAPS ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TUNER_SCAN_CAPS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e19f33c1b54b58f29f1840015aecc4aea0b3a2a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837905"
---
# <a name="ksproperty_tuner_scan_caps"></a>KSK プロパティ\_チューナー\_スキャン\_CAPS


KSK プロパティ\_チューナー\_SCAN\_CAPS プロパティは、デバイスがサポートするネットワークの種類など、チューニングデバイスのスキャン機能について説明します。 このプロパティは、Windows Vista 以降で実行される AVStream チューニングミニドライバーに実装する必要があります。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_scan_caps_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_SCAN_CAPS_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_scan_caps_s)"><strong>KSPROPERTY_TUNER_SCAN_CAPS_S</strong></a></p></td>
<td><p>KSPROPERTY_TUNER_SCAN_CAPS_S</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、\_チューナー\_スキャン\_CAPS\_S 構造で、サポートされているネットワークの種類と、チューニングデバイスのドライバーまたはファームウェアがハードウェア支援型のスキャンをサポートできるかどうかを指定します。業務.

<a name="remarks"></a>解説
-------

ドライバーは、サポートするネットワークの種類に対して、次の Guid のうち少なくとも1つを返す必要があります。 これらの Guid は*Bdamedia*で定義されており、 *Bdamedia*から参照する必要があります。 これらの Guid の詳細については、「[ブロードキャストネットワークの種類の guid](broadcast-network-type-guids.md)」を参照してください。

-   デジタル\_ケーブル\_ネットワーク\_の種類

-   アナログ\_TV\_ネットワーク\_の種類

-   アナログ\_AUXIN\_ネットワーク\_の種類

-   アナログ\_FM\_ネットワーク\_の種類

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


[**KSK プロパティ\_チューナー\_スキャン\_CAPS\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_scan_caps_s)

 

 






