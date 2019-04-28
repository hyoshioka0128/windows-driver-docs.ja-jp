---
title: ドライバーへの WDI TLV ジェネレーター/パーサーの追加
description: WDI TLV ジェネレーター/パーサーをドライバーを追加するには、次の手順に従います。
ms.assetid: 625FDE43-7A42-4840-9AFD-B8F5850F845E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c14b1dc89b3b7f9882b858d61f0c5fbe1aa8536
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367674"
---
# <a name="adding-the-wdi-tlv-generatorparser-to-your-driver"></a>ドライバーへの WDI TLV ジェネレーター/パーサーの追加


WDI TLV ジェネレーター/パーサーをドライバーを追加するには、次の手順に従います。

1.  この追加 dot11wdi.h と wditypes.hpp が含まれます。

    `#include "TlvGeneratorParser.hpp"`

2.  このライブラリをリンカーに追加します。

    `TLVGeneratorParser.lib`

3.  定義、作成、およびメモリ Api を記述 (新規/削除演算子をオーバー ロードされた)。

4.  Api の呼び出しを開始します。

 

 





