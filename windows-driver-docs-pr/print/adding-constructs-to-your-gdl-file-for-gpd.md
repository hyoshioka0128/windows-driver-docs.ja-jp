---
title: GDL ファイル GPD の構成要素を追加します。
description: GDL ファイル GPD の構成要素を追加します。
ms.assetid: a0ce5a46-152f-47f3-9246-c272224d4be9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0808de9030b2089929445403dec6132f79e93464
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550417"
---
# <a name="adding-constructs-to-your-gdl-file-for-gpd"></a>GDL ファイル GPD の構成要素を追加します。


自動構成をサポートするには、次の新しいキーワードを使用して GDL ファイルに構造を追加する必要があります。\***BidiQuery**、 \* **QueryString**、 \* **BidiResponse**、 \* **ResponseType**、 \* **ResponseData**、および\* **BidiValue**します。 これらのキーワードを使用して、機能とそのオプションに選択肢の 1 つのオプションに関連付けられている bidi スキーマの要求を指定することができます。

A \***機能**コンス トラクターは、1 つを含めることができます\* **BidiQuery**のコンテナーとして機能する、構築、 \* **QueryString**インスタンス。 クエリ文字列を\***機能**コンス トラクターのインスタンスが照会される追加機能への双方向通信スキーマ パスの特定のプロパティの名前で構成される Unicode 文字列、機能です。

A \***機能**コンストラクトでは、1 つを含めることができますも\* **BidiResponse**コンス トラクターは、1 つのコンテナーとして機能する\* **ResponseType**インスタンスと省略可能な\* **ResponseData**インスタンス。

各\***オプション**コンストラクトに関連付けられている、 \***機能**コンス トラクターを含める必要があります、 \* **BidiValue**インスタンス適切な応答の文字列表現を含む\***オプション**します。

次の例では、適切な構成要素を GPD ファイルに示す機能に基づいて、GDL ファイルに追加する方法を示します。 最初の 2 つの例は、GPD サンプルと GDL サンプルの自動検出または特定のインストール可能な機能の自動構成をサポートするために必要な構成要素で構成されます。 3 番目の例では、GDL サンプルは、ハード ドライブの自動検出とのハード ドライブの GPD 特徴の定義が存在することを前提としています。

[両面印刷ユニット GPD の自動検出しています](autodetecting-the-duplex-unit-for-gpd.md)

[Autoconfiguring GPD のプリンターのメモリ](autoconfiguring-the-printer-s-memory-for-gpd.md)

[自動検出、プリンターのハード ドライブ GPD](autodetecting-the-printer-s-hard-drive-for-gpd.md)

 

 




