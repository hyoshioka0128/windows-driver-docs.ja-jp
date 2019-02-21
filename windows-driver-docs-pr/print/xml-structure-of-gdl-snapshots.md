---
title: GDL スナップショットの XML 構造
description: GDL スナップショットの XML 構造
ms.assetid: 46051e45-da46-488c-9d70-2299954445be
keywords:
- GDL WDK、スナップショット
- スナップショット WDK GDL、構造体
- パーサー WDK GDL、スナップショット
- GDL WDK、データのツリー
- データは、WDK GDL をツリーします。
- GDL WDK、エントリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28eda4cbe723ae5efeded569785b783fa3be5978
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556663"
---
# <a name="xml-structure-of-gdl-snapshots"></a>GDL スナップショットの XML 構造


XML のスナップショットは、クライアントが指定した構成に適合するこれらのスイッチとケース分岐を含む GDL データ ツリーのサブセットです。 データのツリーは、すべての構成の依存関係のうちいくつかあります、GDL データ エントリによって構成されるツリーです。 構成の依存関係の詳細については、次を参照してください。 [GDL 構成に依存するデータを作成する](creating-gdl-configuration-dependent-data.md)します。

だけでなく、XML のスナップショットを生成するには、GDL パーサーのスナップショットの全体的な構造を記述する別の XSD スキーマを生成できます。 このスキーマには、GDL テンプレートを定義する列挙型のデータ型の定義も含まれています。 これらの定義には、必要な場合は、スナップショットのすべてのプリミティブ データ型のスキーマ検証を実行するクライアントが有効にします。 場合は、スキーマの検証は実行されず、列挙型のチェックを行わないの有効性、DOM ツリーが読み込まれる。GDL パーサーは、独自の列挙の有効性チェックを実行するため、このチェックは必要ではありません。

有効な XML ドキュメント、napshot には、単一のルート要素が含まれています。&lt;SnapshotRoot&gt;します。 この要素は、GDL ツリーのルート コンテキストを表します。 &lt;SnapshotRoot&gt;要素が子を含めることができます&lt;構築&gt;または&lt;GDL\_属性&gt;要素。 &lt;構築&gt;GDL の構成体を表す要素を使用し、 &lt;GDL\_属性&gt;GDL 属性を表す要素を使用します。

各&lt;構築&gt;要素はその他を含めることができます&lt;構築&gt;と&lt;GDL\_属性&gt;要素。 &lt;GDL\_属性&gt;要素はその属性に関連付けられたを含まない値のみを保持&lt;構築&gt;または&lt;GDL\_属性&gt;要素。 &lt;GDL\_属性&gt;値が文字データのコンテンツとして直接表示できます、 &lt;GDL\_属性&gt;非複合データ型の要素または 1 つで表現できるか値が、GDL として定義されている場合は、複数の子要素は複合データ型です。

GDL パーサーで属性を属性の値のデータ型を定義するテンプレートに関連付けることはできない場合、またはある値が、対応する、宣言されたデータ型に準拠していない場合&lt;GDL\_属性&gt;XML スナップショット内の要素には、 &lt;CDATA&gt; GDL ファイルで指定された元の値を格納するセクション。

GDL では、スナップショット スキーマ要素の次の種類をサポートしています。

-   [ルート](gdl-schema-root-element.md)

-   [コンス トラクター](gdl-schema-construct-element.md)

-   [属性](gdl-schema-attribute-element.md)

次のトピックでは、スナップショットの XML スキーマで使用される追加のデータ型について説明します。

[列挙体および XSD 定義データ型](enumerations-and-xsd-defined-data-types.md)

[データ型のラッパー](data-type-wrappers.md)

スナップショット、XML スキーマの名前空間の詳細については、次を参照してください。 [XML スナップショットの名前空間](xml-snapshot-namespaces.md)します。

文字データを XML スナップショットについては、次のトピックを参照してください。

[XML スキーマ Linebreak 翻訳](xml-schema-linebreak-translations.md)

[XML のスナップショットでの Unicode 表現](unicode-representations-in-xml-snapshots.md)

[XML のスナップショットで使用できる文字の制限](xml-restrictions-on-allowed-characters-in-snapshots.md)

 

 




