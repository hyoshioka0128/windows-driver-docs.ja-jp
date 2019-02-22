---
title: スナップショットの XML 名前空間
description: スナップショットの XML 名前空間
ms.assetid: 723f1cfd-633c-4f87-b85f-5ccee45a8c4e
keywords:
- GDL WDK、名前空間
- SnapshotRoot 要素 WDK GDL
- スナップショット WDK GDL、構造体
- スナップショット WDK GDL、名前空間
- WDK GDL 名前空間
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcc840e67d0a1d348d9ab1fe64ad6364ee42e3c8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528110"
---
# <a name="xml-snapshot-namespaces"></a>スナップショットの XML 名前空間


&lt;SnapshotRoot&gt; XML スナップショット内の要素は、スナップショットの名前空間を定義し、xsd、xsi、および既定のプレフィックスに関連付けられます。

```cpp
<SnapshotRoot xmlns="http://schemas.microsoft.com/2002/print/gdl/1.0"
    xmlns:xsd="http://www.w3.org/2001/XMLSchema"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
```

次のコード例は、&lt;スキーマ&gt;GDL パーサーによって生成される XSD スキーマで要素の開始タグ。

```cpp
<schema
    xmlns="http://www.w3.org/2001/XMLSchema"
    xmlns:gdl="http://schemas.microsoft.com/2002/print/gdl/1.0"
    targetNamespace="http://schemas.microsoft.com/2002/print/gdl/1.0"
    elementFormDefault="qualified"
    attributeFormDefault="unqualified">
```

これらの定義には、スキーマとスナップショット内の明示的な名前空間プレフィックスを使用する必要が最小限に抑えます。 一般的なユーザーは、これらの定義の影響について心配する必要はありません。 使用する場合にのみ、これらの規則の名前空間を意識する必要があります\*データ型。XSD\_定義します。 テンプレート作成者は、データ型の定義を使用して指定されている、 \*XSDTypeDefinition ディレクティブが、名前空間とで定義されている既定の設定に従う必要があります、&lt;スキーマ&gt;要素。 これらの XSD のインスタンス データ\_定義データ型で定義されている名前空間に従う必要がある&lt;SnapshotRoot&gt;します。

 

 




