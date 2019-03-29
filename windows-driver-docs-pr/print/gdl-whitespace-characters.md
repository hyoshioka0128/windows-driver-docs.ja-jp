---
title: GDL 空白文字
description: GDL 空白文字
ms.assetid: 703c41c0-3e12-465a-823f-c32990a52382
keywords:
- WDK GDL、空白文字を構築します。
- 継続 linebreak WDK GDL
- linebreak シーケンス WDK GDL
- パーサー WDK GDL、空白の処理
- GDL WDK、空白文字
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 652c91e476f1d749ceb567b20ecfdfafc200b64a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574403"
---
# <a name="gdl-whitespace-characters"></a>GDL 空白文字


*空白文字*スペース、タブ、または継続 linebreak に定義されます。 A*継続 linebreak*はプラス記号 (+) の直後に、linebreak シーケンスです。 (A *linebreak シーケンス*は"\\n\\r「、」\\r\\n「、」\\n"、または"\\r"C 文字列で表されます)。

空白はリテラル内で解釈されます、[文字列を引用符で囲まれた](gdl-quoted-strings.md)と任意の値のコンテキスト内で。 他の場所で発生する空白はリテラルでないと見なされます。 GDL パーサー統合リテラルでない空白です。つまり、任意の数の連続したリテラルでない空白文字が 1 つの空白文字に置き換えられます。 リテラルの空白が統合されていません。

 

 




