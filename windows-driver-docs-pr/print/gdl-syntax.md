---
title: GDL 構文
description: GDL 構文
ms.assetid: 31f0c2f6-2a6b-4a3c-9da1-6fd586b8ae2a
keywords:
- GDL WDK、構文
- WDK GDL データの解析
- パーサー WDK GDL、データの解析
- GDL WDK、属性
- GDL の WDK を構築します
- WDK GDL 属性
- WDK GDL を構築します。
- WDK GDL、区切り記号を構築します。
- GDL WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35e2eff6572823c0ae648deae3585203a1d34020
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380140"
---
# <a name="gdl-syntax"></a>GDL 構文


GDL パーサーでは、GDL エントリのストリームを処理します。 各エントリは linebreak シーケンスまたはコンストラクトの区切り記号で区切られます。 GDL ストリームでは、1 つのファイルに存在する場合か、1 つのファイルに含まれるストリームに論理的に相当するファイル数のシーケンスを構築できます。

GDL エントリの 2 種類があります: 属性と構成要素。 *GDL 属性*はキーワードと値の単純なペアです。 *GDL 構築*と呼ばれるデータ エントリのコレクションを続けて GDL 属性が含まれて、*構築*します。 構成要素のコレクションは、一連の区切り*区切り記号を作成します。*

GDL エントリ間の空白文字を表示できるし、コメントが GDL ストリームに表示できます。

GDL では、文字列を使用して、データを表します。

このセクションの内容:

[GDL 属性](gdl-attributes.md)

[GDL コンテキスト](gdl-contexts.md)

[GDL コンストラクト](gdl-constructs.md)

[GDL 空白文字](gdl-whitespace-characters.md)

[GDL コメント](gdl-comments.md)

[GDL 文字列](gdl-strings.md)

 

 




