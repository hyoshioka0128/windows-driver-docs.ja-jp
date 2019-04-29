---
title: ISAPNP デバイスの識別子
description: ISAPNP デバイスの識別子
ms.assetid: 67337bd6-3b5f-41a7-b50d-bf3587f243e8
keywords:
- デバイスの識別文字列 WDK、ISAPNP デバイス
- 識別文字列の WDK デバイス、ISAPNP デバイス
- 識別子の WDK デバイス、ISAPNP デバイス
- デバイスのデバイス id の ISAPNP WDK デバイスのインストール
- ハードウェア Id の WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 341d5ef9ae7a5337e0b241f8ede14847e3ec0174
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388760"
---
# <a name="identifiers-for-isapnp-devices"></a>ISAPNP デバイスの識別子





各 ISAPNP カードには、サポートされているリソースとカードによって要求されたものを表す、読み取り可能なリソース データ構造がサポートしています。 この構造体は、ISA のカードを複数の関数 (または「論理デバイス」) の概念をサポートします。 独立した一連の"tags"または「記述子」は、カードの各関数に関連付けられます。 このタグ情報を使用して、ISAPNP 列挙子として書式設定された 2 つのハードウェア識別子を作成します。

ISAPNP\\m(3)d(4)

\*m(3)n(4)

場所*m(3)d(4)* 合わせることで、デバイス - 特定のデバイスを識別するには、製造元と 4 桁の 16 進数を識別するために 3 つの文字の EISA スタイル識別子。

次のハードウェア Id のペアは、多機能のカードで特定の関数によって生成される可能性があります。

ISAPNP\\CSC6835_DEV0000

\*CSC0000

最初の 2 つのハードウェア Id がデバイスの id です。 対象のデバイスが、多機能のカードの 1 つの関数の場合は、このフォームは、デバイス ID を受け取ります。

ISAPNP\\m(3)d(4)_DEVn(4)

場所*n(4)* は関数の (ゼロ) を 10 進数のインデックスです。

2 番目の 2 つのハードウェア識別子も互換性のある id。 ISAPNP 列挙子が 2 つ目のハードウェア ID 1 つ目は常に 1 つ以上の互換性のある Id を生成します 最初の 3 つの文字*m(3)*、続く、"\*"ISAPNP と互換性のある ID では頻繁に"PNP"。 たとえば、シリアル ポートの互換性のある ID この可能性があります。

PNP0501

 

 





