---
title: Get 要求と応答のスキーマ
description: Get 要求スキーマと対応する応答スキーマ定義、およびそれぞれの例を以下に示します。
ms.assetid: 48980220-4DD6-4785-AAC1-850F8FBE49EC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37a04b5a64e5b08bb0540619d09553623414a7a3
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652992"
---
# <a name="get-request-and-response-schemas"></a>Get 要求と応答のスキーマ

Get 要求スキーマと対応する応答スキーマ定義、およびそれぞれの例を以下に示します。

## <a name="the-get-request-schema"></a>Get 要求スキーマ

Get 要求と応答は、プリンターの現在の値の1つまたは複数に対してクエリを実行するために使用されます。

この例では、3つのクエリがあります。 最初のクエリは、特定の双方向通信スキーマ値を指し、2番目のクエリはサブツリーを定義する双方向通信スキーマプロパティを指します。 3番目のエラーは意図的なエラーです。双方向通信スキーマに &lt;Foo&gt; プロパティがありません。 (この要求に対する応答は、 [Get Response スキーマの](#the-get-response-schema)次のセクションにあります)。

```xml
<bidi:Get xmlns:bidi="https://schemas.microsoft.com/windows/2005/03/printing/bidi">
  <Query schema='\Printer.Configuration.DuplexUnit:Installed'/>
  <Query schema='\Printer.Configuration.HardDisk'/>
  <Query schema='\Printer.Foo'/>
</bidi:Get>
```

Get 要求スキーマの正式な定義

```xml
<?xml version='1.0'?>
<schema targetNamespace="https://schemas.microsoft.com/windows/2005/03/printing/bidi"
  xmlns:bidi="https://schemas.microsoft.com/windows/2005/03/printing/bidi" 
  xmlns ='https://www.w3.org/2001/XMLSchema'>
  <element name='Get'>
    <complexType>
      <sequence maxOccurs='unbounded'>
        <element name='Query'>
          <complexType>
            <attribute name='schema' type='bidi:PARTIAL_SCHEMA_STRING' use='required'/>
            <anyAttribute namespace='##other' processContents='skip'/>
          </complexType>
        </element>
      </sequence>
      <anyAttribute namespace='##other' processContents='skip'/>
    </complexType>
  </element>
  <simpleType name='PARTIAL_SCHEMA_STRING'>
    <restriction base='string'>
      <pattern value='\(\w+(\.\w+)*(\:\w+)?)?'/>
    </restriction>
  </simpleType>
</schema>
```

## <a name="the-get-response-schema"></a>Get Response スキーマ

この例は、上記の Get 要求に対する応答です。 成功のクエリの場合、結果は特定のスキーマの値になります。 3番目のクエリが失敗したため、結果はエラーコードになります。 2番目のクエリでは、子を持つプロパティが要求されたため、応答では、すべての子の名前と値が提供されることに注意してください。

```xml
<bidi:Get xmlns:bidi="https://schemas.microsoft.com/windows/2005/03/printing/bidi">
  <Query schema='\Printer.Configuration.DuplexUnit:Installed'/>
    <Schema name='\Printer.Configuration.DuplexUnit:Installed'>
      <BIDI_BOOL>true</BIDI_BOOL>
    </Schema>
  </Query>
  <Query schema='\Printer.HardDisk'>
    <Schema name='\Printer.HardDisk:Installed'>
      <BIDI_BOOL>true</BIDI_BOOL>
    </Schema>
    <Schema name='\Printer.HardDisk:Capacity'>
      <BIDI_INT>20971520</BIDI_INT>
    </Schema>
    <Schema name='\Printer.HardDisk:FreeSpace'>
      <BIDI_INT>10460419</BIDI_INT>
    </Schema>
  </Query>
  <Query schema='\Printer.Foo'>
    <Error>ERROR_BIDI_SCHEMA_NOT_SUPPORTED</Error>
  </Query>
</bidi:Get>
```

Get Response スキーマの正式な定義

```xml
<?xml version='1.0'?>
<schema targetNamespace="https://schemas.microsoft.com/windows/2005/03/printing/bidi" 
  xmlns:bidi="https://schemas.microsoft.com/windows/2005/03/printing/bidi" 
  xmlns ='https://www.w3.org/2001/XMLSchema'>
  <element name='Get'>
    <complexType>
      <sequence maxOccurs='unbounded'>
        <element name='Query'>
          <complexType>
            <choice>
              <sequence maxOccurs='unbounded'>
                <element name='Schema'>
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
                    <attribute name='name' type='bidi:SCHEMA_STRING' use='required'/>
                  </complexType>
                </element>
              </sequence>
              <element name='Error' type='integer'/>
            </choice>
            <attribute name='schema' type='bidi:PARTIAL_SCHEMA_STRING' use='required'/>
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
  <simpleType name='PARTIAL_SCHEMA_STRING'>
    <restriction base='string'>
      <pattern value='\(\w+(\.\w+)*(\:\w+)?)?'/>
    </restriction>
  </simpleType>
</schema>
```

## <a name="related-topics"></a>関連トピック

[双方向通信スキーマ](bidirectional-communication-schema.md)  

[SendRecvXMLStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/bidispl/nf-bidispl-ibidispl2-sendrecvxmlstream)  

[SendRecvXMLString](https://docs.microsoft.com/windows-hardware/drivers/ddi/bidispl/nf-bidispl-ibidispl2-sendrecvxmlstring)  
