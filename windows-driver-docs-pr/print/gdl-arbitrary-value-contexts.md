---
title: GDL 任意の値のコンテキスト
description: GDL 任意の値のコンテキスト
ms.assetid: 6de79b2b-5f0f-4d6c-8a95-d9ef2266c2ef
keywords:
- GDL WDK、コンテキスト
- WDK GDL、任意の値のコンテキストのコンテキスト
- 任意の値のコンテキスト WDK GDL
- WDK GDL、コンテキストの値
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87476d59772c779e52899e3a05f6a678c68234e5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363332"
---
# <a name="gdl-arbitrary-value-contexts"></a>GDL 任意の値のコンテキスト


*任意の値のコンテキスト*GDL 構文規則に違反している場合でも、任意の文字の順序を含む値を定義するために使用します。

任意の値のコンテキストが導入されたときに、"&lt;BeginValue:*シンボル*&gt;"文字のシーケンスが検出され、終了するときに、"&lt;EndValue:*シンボル*&gt;"文字のシーケンスが発生しました。 *シンボル*は選択した任意の有効なシンボル トークンです。 BeginValue と EndValue の両方の呼び出しで同じシンボルが表示する必要があります。 BeginValue と EndValue タグにある空白文字を表示できません。

コメントまたは引用符で囲まれた文字列内で任意の値コンテキスト以外では、任意の値のコンテキストを定義できます。 任意の値のコンテキストは、入れ子になったコンテキスト内で表示できます。 コンテキストは、任意の値のコンテキスト内で認識されないが、内で任意のバイト シーケンスを定義することができます。

任意の値のコンテキスト シンボルは、トークンのセットの文字で構成される\[A ~ Z、a ~ z、0-9、 \_ \]します。 シンボルの長さに制限はありません。

 

 




