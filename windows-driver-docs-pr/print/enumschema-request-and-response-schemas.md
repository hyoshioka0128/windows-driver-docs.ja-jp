---
title: EnumSchema 要求と応答のスキーマ
description: EnumSchema 要求スキーマと対応する応答スキーマ定義、およびそれぞれの例を以下に示します。
ms.assetid: 031FA2EA-A33B-409C-82FD-B4FE9D0A2E93
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 798cc4d66e12e7627ca9747f55eb3c543b4e8075
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652800"
---
# <a name="enumschema-request-and-response-schemas"></a>EnumSchema 要求と応答のスキーマ


EnumSchema 要求スキーマと対応する応答スキーマ定義、およびそれぞれの例を以下に示します。

## <a name="the-enumschema-request-schema"></a>EnumSchema 要求スキーマ


EnumSchema 要求は、プリンターのプロパティの一覧を取得するために使用されます。

すべての EnumSchema 要求はまったく同じであり、ルート要素のみで構成されています。

```xml
<bidi:EnumSchema xmlns:bidi="https://schemas.microsoft.com/windows/2005/03/printing/bidi"/>
```

EnumSchema 要求スキーマの正式な定義

```xml
<?xml version='1.0'?>
<schema targetNamespace="https://schemas.microsoft.com/windows/2005/03/printing/bidi" 
  xmlns:bidi="https://schemas.microsoft.com/windows/2005/03/printing/bidi" 
  xmlns ='https://www.w3.org/2001/XMLSchema'>
  <element name='EnumSchema'>
    <complexType>
      <anyAttribute namespace='##other' processContents='skip'/>
    </complexType>
  </element>
</schema>
```

## <a name="the-enumschema-response-schema"></a>EnumSchema 応答スキーマ


EnumSchema 応答には、各プロパティの &lt;Schema&gt; 要素があります。

この例では、プリンターにはいくつかのアクセス可能なプロパティしかありません。

```xml
<bidi:EnumSchema xmlns:bidi="https://schemas.microsoft.com/windows/2005/03/printing/bidi">
  <Schema name='\Printer.Configuration.DuplexUnit:Installed' />
  <Schema name='\Printer.Configuration.HardDisk:Installed'/>
  <Schema name='\Printer.Configuration.HardDisk:Capacity'/>
  <Schema name='\Printer.Configuration.HardDisk:FreeSpace'/>
</bidi:EnumSchema>
```

EnumSchema Response スキーマの正式な定義

```xml
<?xml version='1.0'?>
<schema targetNamespace="https://schemas.microsoft.com/windows/2005/03/printing/bidi" 
  xmlns:bidi="https://schemas.microsoft.com/windows/2005/03/printing/bidi" 
  xmlns ='https://www.w3.org/2001/XMLSchema'>
  <element name='EnumSchema'>
    <complexType>
      <sequence maxOccurs='unbounded'>
        <element name='Schema'>
          <complexType>
            <attribute name='name' type='bidi:SCHEMA_STRING' use='required'/>
          </complexType>
        </element>
      </sequence>
    </complexType>
  </element>
  <simpleType name='SCHEMA_STRING'>
    <restriction base='string'>
      <pattern value='\\\w+(\.\w+)*\:\w+'/>
    </restriction>
  </simpleType>
</schema>
```

## <a name="related-topics"></a>関連トピック

[双方向通信スキーマ](bidirectional-communication-schema.md)  

[SendRecvXMLStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/bidispl/nf-bidispl-ibidispl2-sendrecvxmlstream)  

[SendRecvXMLString](https://docs.microsoft.com/windows-hardware/drivers/ddi/bidispl/nf-bidispl-ibidispl2-sendrecvxmlstring)  



