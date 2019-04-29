---
title: GDL 引用符付き文字列
description: GDL 引用符付き文字列
ms.assetid: 52d6f1bf-0b8c-4aa7-8cc8-1a18def224be
keywords:
- WDK GDL、文字列を構築します。
- GDL WDK、文字列
- WDK GDL、文字列を引用符で囲まれた文字列します。
- 引用符で囲まれた文字列 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0911ff78717c40e1bdc78f39c7fd1a4c2e5306e1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366342"
---
# <a name="gdl-quoted-strings"></a>GDL 引用符付き文字列


A*文字列を引用符で囲まれた*始まりの二重引用符文字 (") で終了します。 間に表示される任意の文字は、次の例外を引用符で囲まれた文字列の一部として文字どおり扱われます。

-   パーセント記号と二重引用符 (%") は、リテラル二重引用符文字 (") として扱われます。

-   パーセント記号と小なり記号 (%&lt;) 記号よりも小さいか、リテラルとして扱われます (&lt;)。

-   その他の任意の文字の後に、パーセント記号はパーセント記号 (%) をリテラルとして扱われます。

-   記号よりも低い (&lt;) が導入されています、 [HexSubString](gdl-hexsubstrings.md)コンテキスト。

-   引用符で囲まれた文字列が入れ子になったコンテキスト内で表示できます。uoted 文字列内にある HexSubString コンテキストのみが認識されます。

 

 




