---
title: Get 要求と応答のスキーマ
description: Get 要求のスキーマと対応する応答のスキーマ定義と、それぞれの例が下回っています。
ms.assetid: 48980220-4DD6-4785-AAC1-850F8FBE49EC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff1d2e9ab650b9ea94eff9ec5c17f7fbe459e0e3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358748"
---
# <a name="get-request-and-response-schemas"></a>Get 要求と応答のスキーマ

Get 要求のスキーマと対応する応答のスキーマ定義と、それぞれの例が下回っています。

## <a name="the-get-request-schema"></a>Get 要求のスキーマ

Get 要求と応答は、現在の値の 1 つ以上のプリンターをクエリに使用されます。

この例では、3 つのクエリです。 最初のクエリは、双方向通信のスキーマの特定の値と 2 番目のサブツリーを定義する双方向通信のスキーマのプロパティを指します。 3 番目は意図的なエラー: がない&lt;Foo&gt;双方向通信のスキーマ内のプロパティ。 (この要求に応答が、次のセクションでは[取得応答スキーマ](#the-get-response-schema))。

```xml
<bidi:Get xmlns:bidi="http://schemas.microsoft.com/windows/2005/03/printing/bidi">
  <Query schema='\Printer.Configuration.DuplexUnit:Installed'/>
  <Query schema='\Printer.Configuration.HardDisk'/>
  <Query schema='\Printer.Foo'/>
</bidi:Get>
```

Get 要求のスキーマの正式な定義

```xml
<?xml version='1.0'?>
<schema targetNamespace="http://schemas.microsoft.com/windows/2005/03/printing/bidi"
  xmlns:bidi="http://schemas.microsoft.com/windows/2005/03/printing/bidi" 
  xmlns ='http://www.w3.org/2001/XMLSchema'>
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

## <a name="the-get-response-schema"></a>Get 応答スキーマ

この例では、上記の Get 要求に応答を示します。 クエリの成功は、結果は、値の特定のスキーマ。 結果がエラー コード、3 番目のクエリが失敗しました。 2 番目のクエリに子を持つプロパティが要求されたため、応答が提供するすべての子の値と名前に注意してください。

```xml
<bidi:Get xmlns:bidi="http://schemas.microsoft.com/windows/2005/03/printing/bidi">
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

Get 応答スキーマの正式な定義

```xml
<?xml version='1.0'?>
<schema targetNamespace="http://schemas.microsoft.com/windows/2005/03/printing/bidi" 
  xmlns:bidi="http://schemas.microsoft.com/windows/2005/03/printing/bidi" 
  xmlns ='http://www.w3.org/2001/XMLSchema'>
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

[双方向通信のスキーマ](bidirectional-communication-schema.md)  

[SendRecvXMLStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bidispl/nf-bidispl-ibidispl2-sendrecvxmlstream)  

[SendRecvXMLString](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bidispl/nf-bidispl-ibidispl2-sendrecvxmlstring)  
