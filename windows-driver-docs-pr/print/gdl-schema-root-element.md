---
title: GDL スキーマのルート要素
description: GDL スキーマのルート要素
ms.assetid: 6148f026-52fa-452d-aa81-564d6ee5288d
keywords:
- GDL WDK、要素
- GDL WDK、スキーマ
- SnapshotRoot 要素 WDK GDL
- WDK GDL のルート要素
- スナップショット WDK GDL、構造体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0064121920559af2d9dd36dd8acb1a2337fd66bb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551176"
---
# <a name="gdl-schema-root-element"></a>GDL スキーマのルート要素


GDL パーサーによって生成される XSD スキーマにルート要素が定義されています (&lt;SnapshotRoot&gt;) 次のようにします。

```cpp
    <element name="SnapshotRoot" type="gdl:GDL_RootType"/>

    <complexType name="GDL_RootType"  >
        <sequence>
            <any processContents="lax" minOccurs="0" maxOccurs="unbounded"/>
        </sequence>
    </complexType>
```

XSD スキーマが許可しない&lt;任意&gt;パーサーのスキーマがルート要素の定義が非常に柔軟なのでと共存させる要素が要素の型を定義します。 XSD スキーマの意図的に非常に一般的なままですが、 &lt;SnapshotRoot&gt;要素は、任意の数を保持できる&lt;GDL\_属性&gt;または&lt;構築&gt;任意の順序で要素です。 最近に定義されたエントリに GDL 言語の重点を置いた、ため、XML スナップショット内の要素の外観は GDL ソース ファイル内のエントリの外観の逆では通常です。

&lt;SnapshotRoot&gt;要素は、スナップショットのドキュメントで最も外側の要素と、すべてのスナップショット内の他の要素が含まれています。 1 つしかない&lt;SnapshotRoot&gt;各スナップショット内の要素。

 

 




