---
title: GDL スキーマのコンストラクト要素
description: GDL スキーマのコンストラクト要素
ms.assetid: 46653504-4ce7-455c-a22a-a6032cbd6a3e
keywords:
- GDL WDK、要素
- GDL WDK、スキーマ
- WDK GDL 要素を構築します。
- スナップショット WDK GDL、構造体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3328437244059dc780f95ceae244ffe0c9d53c3c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366434"
---
# <a name="gdl-schema-construct-element"></a>GDL スキーマのコンストラクト要素


GDL パーサーによって生成される XSD スキーマでは、としては、次のように構成要素を定義します。

```cpp
    <complexType name="GDL_ConstructType">
        <sequence>
            <any processContents="lax" minOccurs="0" maxOccurs="unbounded"/>
        </sequence>
        <attribute name="Name" type="string" use="required"/>
        <attribute name="Instance" type="string" use="required"/>
        <attribute name="Constrained" type="boolean" use="optional"/>
    </complexType>
```

前の定義の定義に似ています、 [ &lt;SnapshotRoot&gt;要素](gdl-schema-root-element.md)します。 ルート要素と同様の要素を構築、構成要素を保持することができます (&lt;構築&gt;) と属性 (&lt;GDL\_属性&gt;) 要素。 ただし、 &lt;GDL\_ConstructType&gt;追加の 3 つの XML 属性を持つことができます。**名前**、**インスタンス**、および**制約付き**します。 **名前**と**インスタンス**必要し、それぞれ名前とインスタンス GDL の構造を保持します。 **制約付き**は省略可能で、かどうかのオプションが制約されるかどうかを示すブール値を保持します。 この属性は、に対してのみ表示されます&lt;構築&gt;に対応する要素\*オプションの構成要素。

たとえば、次の GDL エントリを検討してください。

```cpp
*Feature:  PaperSize
{
   *Option:  Letter
   {
   }
}
```

上記のエントリは、次の XML のスナップショットの結果します。

```cpp
     <CONSTRUCT Name="*Feature" Instance="PaperSize">
        <CONSTRUCT Name="*Option" Instance="Letter" Constrained="FALSE" >
        </CONSTRUCT>
    </CONSTRUCT>
```

特定のオプションは、指定された構成と、一連の GDL インスタンス データで定義されている制約によって制約付きでマークされます。

 

 




