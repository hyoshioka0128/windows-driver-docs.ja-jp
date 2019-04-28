---
title: PCMCIA デバイスの識別子
description: PCMCIA デバイスの識別子
ms.assetid: 7eaf6372-a9cc-4714-8955-52653ec57141
keywords:
- デバイスの識別文字列 WDK、PCMCIA デバイス
- 識別文字列の WDK デバイス、PCMCIA デバイス
- 識別子の WDK デバイス、PCMCIA デバイス
- PCMCIA デバイス識別子 WDK デバイスのインストール
- デバイス Id の WDK デバイスのインストール
- ハードウェア Id の WDK デバイスのインストール
- 互換性のある Id WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d244ddd3d19256849ec6a7860156b87eb1c50962
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363011"
---
# <a name="identifiers-for-pcmcia-devices"></a>PCMCIA デバイスの識別子





パーソナル コンピューター メモリ カード International Association (PCMCIA) デバイス、デバイス ID を行うにはいくつかの異なるフォームがかかります。 デバイスの多機能でない場合、デバイス id は次の形式します。

PCMCIA\\Manufacturer-Product-Crc(4)

各項目の意味は次のとおりです。

-   *製造元*製造元の名前を指定します。

-   *製品*製品の名前を指定します。

PCMCIA 列挙子は、カード上の組から直接これらの文字列を取得します。 両方*製造元*と*製品*は 64 文字を超えない可変長文字列です。 *Crc(4)* はカードの 4 桁の 16 進数 CRC (巡回冗長検査) checksum です。 数値の先頭 4 桁よりもゼロ埋め込み。 たとえば、ネットワーク アダプターのデバイス ID では、これに可能性があります。

PCMCIA\\MEGAHERTZ-CC10BT/2-BF05

多機能カードでは、すべての関数形式の識別子があります。

PCMCIA\\Manufacturer-Product-DEVd(4)-Crc(4)

子関数の数 (*d(4)* この例では) は先行ゼロなし 10 進数です。

カードが製造元の名前を持たない場合、これら 3 つの形式のいずれかがその識別子には。

PCMCIA\\UNKNOWN_MANUFACTURER-Crc(4)

PCMCIA\\UNKNOWN_MANUFACTURER-DEVd(4)-Crc(4)

PCMCIA\\MTD-MemoryType(4)

これら 3 つの選択肢の最後のタスクは、カードの製造元識別子なしのフラッシュ メモリ カード用です。 *MemoryType(4)* は 2 つの 4 桁の 16 進数の 1 つです。SRAM カード 0000 と 0002 ROM カード。

デバイスのさまざまなフォームだけでなく ID に記載した INF ファイルの[**セクションをモデル化**](inf-models-section.md) 4 桁の 16 進数巡回冗長検査 (CRC) を置き換えることで、構成、ハードウェア ID を含めることもできます4 桁の 16 進数の製造元コード、ハイフン、および 4 桁の 16 進数の製造元情報コード (内蔵型のタプルの両方) を含む文字列。 次に、例を示します。

PCMCIA\\MEGAHERTZ-CC10BT/2-0128-0103

PCMCIA と互換性のある Id は、汎用的なデバイスで説明されている Id に対応、[ジェネリック識別子](generic-identifiers.md)セクション。 現時点では、次の表に示す 3 つだけのデバイスの種類の PCMCIA と互換性のある Id が生成されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">PCMCIA と互換性のある ID</th>
<th align="left">デバイスの種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>PNP0600</p></td>
<td align="left"><p>添付ファイル (ATA) でのディスク ドライバー</p></td>
</tr>
<tr class="even">
<td align="left"><p></em>PNP0D00</p></td>
<td align="left"><p>多機能 3.0 PC カード</p></td>
</tr>
<tr class="odd">
<td align="left"><p>* PNPC200</p></td>
<td align="left"><p>モデムのカード</p></td>
</tr>
</tbody>
</table>

 

 

 





