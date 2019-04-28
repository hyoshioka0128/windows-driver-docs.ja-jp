---
title: GDL HexSubStrings
description: GDL HexSubStrings
ms.assetid: 7451fd1f-a765-486a-bd90-bc01eac2c388
keywords:
- WDK GDL、文字列を構築します。
- GDL WDK、文字列
- 文字列 WDK GDL、HexSubString
- HexSubString WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 403becf4763b4a4fcd9eb0446c2fd97e44b0146d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372130"
---
# <a name="gdl-hexsubstrings"></a>GDL HexSubStrings


A *HexSubString*は引用符で囲まれた文字列内の非表示文字を表す方法です。 小なり記号によって、HexSubString が導入されました (&lt;) は大なり記号で終了し、(&gt;)。

HexSubString コンテキスト内で文字のみを許可する 16 進数、空白文字と改行のシーケンスと継続の改行に示します。 HexSubString コンテキスト内で発生するすべての空白および改行文字は無視されます。 2 桁の 16 進数字が 1 バイトを定義する必要があるために、各 HexSubString は偶数の 16 進数の数字を含める必要があります。

HexSubString で、パーセント記号を表す必要がある場合は、パーセント記号 (%) で終わる引用符で囲まれた文字列を作成するには、"&lt;25&gt;"。

HexSubString コンテキストは、引用符で囲まれた文字列のコンテキスト内でのみ表示できます。 コメントは、HexSubString コンテキスト内で表示できます。

 

 




