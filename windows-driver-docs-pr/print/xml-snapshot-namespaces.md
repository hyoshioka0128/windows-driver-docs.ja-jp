---
title: XML スナップショット名前空間
description: XML スナップショット名前空間
ms.assetid: 723f1cfd-633c-4f87-b85f-5ccee45a8c4e
keywords:
- GDL WDK、名前空間
- SnapshotRoot 要素 WDK GDL
- スナップショット WDK GDL, 構造
- スナップショット WDK GDL、名前空間
- 名前空間 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4c8c997a78288cad82da9d32179559ef71ee77b
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75653016"
---
# <a name="xml-snapshot-namespaces"></a>XML スナップショット名前空間


XML スナップショット内の &lt;SnapshotRoot&gt; 要素は、スナップショットの名前空間を定義し、それらを xsd、xsi、および default プレフィックスに関連付けます。

```cpp
<SnapshotRoot xmlns="https://schemas.microsoft.com/2002/print/gdl/1.0"
    xmlns:xsd="https://www.w3.org/2001/XMLSchema"
    xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance">
```

次のコード例は、GDL パーサーによって生成される XSD スキーマの &lt;スキーマ&gt; 要素の開始タグを示しています。

```cpp
<schema
    xmlns="https://www.w3.org/2001/XMLSchema"
    xmlns:gdl="https://schemas.microsoft.com/2002/print/gdl/1.0"
    targetNamespace="https://schemas.microsoft.com/2002/print/gdl/1.0"
    elementFormDefault="qualified"
    attributeFormDefault="unqualified">
```

これらの定義により、スキーマおよびスナップショットで明示的な名前空間プレフィックスを使用する必要が最小限に抑えられます。 一般的なユーザーは、これらの定義の影響について心配する必要はありません。 これらの名前空間規則に注意する必要があるのは、\*DataType: XSD\_定義済みのデータ型を使用する場合のみです。 テンプレートの作成者の場合、\*XSDTypeDefinition ディレクティブを使用して指定するデータ型定義は、&lt;schema&gt; 要素で定義されている名前空間と既定値に従う必要があります。 これらの XSD\_定義されたデータ型のインスタンスデータは、&lt;SnapshotRoot&gt;で定義されている名前空間に従う必要があります。

 

 




