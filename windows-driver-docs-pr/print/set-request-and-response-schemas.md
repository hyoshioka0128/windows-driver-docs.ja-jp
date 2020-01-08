---
title: Set 要求と応答のスキーマ
description: Set 要求スキーマと対応する応答スキーマ定義、およびそれぞれの例を以下に示します。
ms.assetid: 88E7F06C-3232-48C3-A0D6-2BEFF4ABA188
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53c1b87b5da29438077e6dc92f0b55ae602ca221
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652960"
---
# <a name="set-request-and-response-schemas"></a>Set 要求と応答のスキーマ


Set 要求スキーマと対応する応答スキーマ定義、およびそれぞれの例を以下に示します。

## <a name="set-request-schema"></a>要求スキーマの設定


設定要求は、プリンターのプロパティに値を書き込むために使用されます。

この例では、要求は2つのプロパティを設定しようとします。 2つ目は意図的な誤りです。メモリプロパティは書き込み可能ではありません。 この要求に対する応答については、以下の「応答スキーマを設定する」を参照してください。

```xml
<bidi:Set xmlns:bidi="https://schemas.microsoft.com/windows/2005/03/printing/bidi">
  <Query schema='\Printer.DeviceInfo:Location'>
    <BIDI_STRING>supply room</BIDI_STRING>
  </Query>
  <Query schema='\Printer.Configuration.Memory:Size'>
    <BIDI_INT>4096</BIDI_INT>
  </Query>
</bidi:Set>
```

Set 要求スキーマの正式な定義

```xml
<?xml version='1.0'?>
<schema targetNamespace="https://schemas.microsoft.com/windows/2005/03/printing/bidi" 
     xmlns:bidi="https://schemas.microsoft.com/windows/2005/03/printing/bidi" 
     xmlns ='https://www.w3.org/2001/XMLSchema'>
  <element name='Set'>
    <complexType>
      <sequence maxOccurs='unbounded'>
        <element name='Query'>
          <complexType>
            <choice>
              <element name='BIDI_STRING' type='string'/>
              <element name='BIDI_TEXT'   type='string'/>
              <element name='BIDI_ENUM'   type='string'/>
              <element name='BIDI_INT'    type='integer'/>
              <element name='BIDI_FLOAT'  type='float'/>
              <element name='BIDI_BOOL'   type='boolean'/>
              <element name='BIDI_BLOB'   type='base64Binary'/>
            </choice>
            <attribute name='schema' type='bidi:SCHEMA_STRING' use='required'/>
            <anyAttribute namespace='##other' processContents='skip'/>
          </complexType>
          </element>
      </sequence>
      <anyAttribute namespace='##other' processContents='skip'/>
    </complexType>
  </element>
  <simpleType name='SCHEMA_STRING'>
    <restriction base='string'>
      <pattern value='\\\w+(\.\w+)*\:\w+'/>
    </restriction>
  </simpleType>
</schema>
```

## <a name="set-response-schema"></a>応答スキーマの設定


これは、上記の Set 要求に対する応答です。 書き込み操作が成功すると、元のクエリ値が値なしで返されることに注意してください。 操作が失敗した場合は、エラーコードが返されます。

```xml
<bidi:Set xmlns:bidi="https://schemas.microsoft.com/windows/2005/03/printing/bidi">
  <Query schema='\Printer.DeviceInfo:Location'/>
  <Query schema='\Printer.Configuration.Memory:Size'>
    <Error>ERROR_BIDI_SCHEMA_READ_ONLY</Error>
  </Query>
</bidi:Set>
```

Set Response スキーマの正式な定義

```xml
<?xml version='1.0'?>
<schema targetNamespace="https://schemas.microsoft.com/windows/2005/03/printing/bidi" 
     xmlns:bidi="https://schemas.microsoft.com/windows/2005/03/printing/bidi" 
     xmlns ='https://www.w3.org/2001/XMLSchema'>
  <element name='Set'>
    <complexType>
      <sequence maxOccurs='unbounded'>
        <element name='Query'>
          <complexType>
            <sequence minOccurs='0' maxOccurs='1'>
              <element name='Error' type='integer'/>
            </sequence>
            <attribute name='schema' type='bidi:SCHEMA_STRING' use='required'/>
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
