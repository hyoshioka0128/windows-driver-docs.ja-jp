---
title: KSPROPERTY\_チューナー\_スキャン\_キャップ
description: KSPROPERTY\_チューナー\_スキャン\_CAPS プロパティが、デバイスをサポートするネットワークの種類を含め、チューニング、デバイスのスキャン機能について説明します。
ms.assetid: 339d5f6b-81ac-419e-9821-a7f1642e1aa8
keywords:
- KSPROPERTY_TUNER_SCAN_CAPS ストリーミング メディア デバイス
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
ms.openlocfilehash: a6f6244fa9f9a6915515502e58ad6881a647a6b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538147"
---
# <a name="kspropertytunerscancaps"></a>KSPROPERTY\_チューナー\_スキャン\_キャップ


KSPROPERTY\_チューナー\_スキャン\_CAPS プロパティが、デバイスをサポートするネットワークの種類を含め、チューニング、デバイスのスキャン機能について説明します。 このプロパティは、Windows Vista 以降を実行している AVStream チューニング ミニドライバーを実装する必要があります。

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
<td><p>Pin</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565892" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_SCAN_CAPS_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565892)"><strong>KSPROPERTY_TUNER_SCAN_CAPS_S</strong></a></p></td>
<td><p>KSPROPERTY_TUNER_SCAN_CAPS_S</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、KSPROPERTY\_チューナー\_スキャン\_CAP\_構造をサポートされているネットワークの種類と、ドライバーまたはチューニングのデバイスのファームウェアをサポートできるかどうかを指定します。ハードウェア依存の操作をスキャンします。

<a name="remarks"></a>注釈
-------

ドライバーは、少なくとも 1 つのネットワークの種類でサポートされるは、次の Guid を返す必要があります。 これらの Guid が定義されている*Bdamedia.h*からは参照する必要があります*Bdamedia.h*します。 これらの Guid の詳細については、[ブロードキャスト ネットワークの種類の Guid](broadcast-network-type-guids.md)を参照してください。

-   デジタル\_ケーブル\_ネットワーク\_型

-   アナログ\_テレビ\_ネットワーク\_型

-   アナログ\_AUXIN\_ネットワーク\_型

-   アナログ\_FM\_ネットワーク\_型

<a name="requirements"></a>要件
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


[**KSPROPERTY\_チューナー\_スキャン\_CAP\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565892)

 

 






