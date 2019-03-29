---
title: EnumSchema 要求と応答のスキーマ
description: EnumSchema 要求スキーマと対応する応答のスキーマ定義と、それぞれの例が下回っています。
ms.assetid: 031FA2EA-A33B-409C-82FD-B4FE9D0A2E93
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05c4ea5d217578e313ff39a8b68cebe85be49169
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570255"
---
# <a name="enumschema-request-and-response-schemas"></a>EnumSchema 要求と応答のスキーマ


EnumSchema 要求スキーマと対応する応答のスキーマ定義と、それぞれの例が下回っています。

## <a name="the-enumschema-request-schema"></a>EnumSchema 要求スキーマ


EnumSchema 要求を使用して、プリンターのプロパティの一覧を取得できます。

EnumSchema のすべての要求はまったく同じと、ルート要素のみで構成されます。

```xml
<bidi:EnumSchema xmlns:bidi="http://schemas.microsoft.com/windows/2005/03/printing/bidi"/>
```

EnumSchema Request スキーマの正式な定義

```xml
<?xml version='1.0'?>
<schema targetNamespace="http://schemas.microsoft.com/windows/2005/03/printing/bidi" 
  xmlns:bidi="http://schemas.microsoft.com/windows/2005/03/printing/bidi" 
  xmlns ='http://www.w3.org/2001/XMLSchema'>
  <element name='EnumSchema'>
    <complexType>
      <anyAttribute namespace='##other' processContents='skip'/>
    </complexType>
  </element>
</schema>
```

## <a name="the-enumschema-response-schema"></a>EnumSchema 応答スキーマ


EnumSchema 応答に、&lt;スキーマ&gt;の各プロパティの要素。

この例では、プリンターは、いくつかアクセス可能なプロパティのみを持ちます。

```xml
<bidi:EnumSchema xmlns:bidi="http://schemas.microsoft.com/windows/2005/03/printing/bidi">
  <Schema name='\Printer.Configuration.DuplexUnit:Installed' />
  <Schema name='\Printer.Configuration.HardDisk:Installed'/>
  <Schema name='\Printer.Configuration.HardDisk:Capacity'/>
  <Schema name='\Printer.Configuration.HardDisk:FreeSpace'/>
</bidi:EnumSchema>
```

EnumSchema 応答スキーマの正式な定義

```xml
<?xml version='1.0'?>
<schema targetNamespace="http://schemas.microsoft.com/windows/2005/03/printing/bidi" 
  xmlns:bidi="http://schemas.microsoft.com/windows/2005/03/printing/bidi" 
  xmlns ='http://www.w3.org/2001/XMLSchema'>
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

[双方向通信のスキーマ](bidirectional-communication-schema.md)  

[SendRecvXMLStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bidispl/nf-bidispl-ibidispl2-sendrecvxmlstream)  

[SendRecvXMLString](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bidispl/nf-bidispl-ibidispl2-sendrecvxmlstring)  



