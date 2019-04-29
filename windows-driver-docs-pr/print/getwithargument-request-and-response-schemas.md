---
title: GetWithArgument 要求と応答のスキーマ
description: GetWithArgument 要求スキーマと対応する応答のスキーマ定義と、それぞれの例が下回っています。
ms.assetid: F68731BC-2907-4FA2-B5A4-0FAC0A9F663A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6de45195127289ddbf510ea008aa0a65efbf4d19
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385241"
---
# <a name="getwithargument-request-and-response-schemas"></a>GetWithArgument 要求と応答のスキーマ


GetWithArgument 要求スキーマと対応する応答のスキーマ定義と、それぞれの例が下回っています。

## <a name="getwithargument-request-schema"></a>GetWithArgument 要求スキーマ


GetWithArgument 要求は、現在の値の 1 つ以上のプリンターをクエリに使用されます。

この要求に応答が、次のセクションでは[GetWithArgument 応答スキーマ](#getwithargument-response-schema)します。

```xml
<bidi:GetWithArgument xmlns:bidi='http://schemas.microsoft.com/windows/2005/03/printing/bidi'>
  <Query schema='\Printer.Resources:Data'>
    <BIDI_STRING>en-us</BIDI_STRING>
  </Query>
</bidi:GetWithArgument>
```

GetWithArgument Request スキーマの正式な定義

```xml
<?xml version='1.0'?>  
<schema targetNamespace='http://schemas.microsoft.com/windows/2005/03/printing/bidi'  
    xmlns:bidi='http://schemas.microsoft.com/windows/2005/03/printing/bidi'   
    xmlns ='http://www.w3.org/2001/XMLSchema'>  
    <element name='GetWithArgument'>  
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
                        <attribute name='schema' type='bidi:PARTIAL_SCHEMA_STRING' use='required'/>  
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
    <simpleType name='PARTIAL_SCHEMA_STRING'>  
        <restriction base='string'>  
            <pattern value='\(\w+(\.\w+)*(\:\w+)?)?'/>  
        </restriction>  
    </simpleType>   
</schema>
```

## <a name="getwithargument-response-schema"></a>GetWithArgument 応答スキーマ

この例では、上記の GetWithArgument 要求に対する応答です。 成功したクエリでは、特定のスキーマの値になります。 失敗したクエリでは、結果は、エラー コードです。

```xml
<bidi:GetWithArgumentResponse xmlns:bidi="http://schemas.microsoft.com/windows/2005/03/printing/bidi">
  <Query schema="\Printer.Data:GetWithArgument">
    <Schema name="\Printer.Data:GetWithArgument">
      <BIDI_BLOB>Base64 Encoded XML resource file data to be used by Print Config<BIDI_BLOB>
    </Schema>
  </Query>
</bidi:GetWithArgumentResponse>
```

GetWithArgument 応答スキーマの正式な定義

```xml
<?xml version='1.0'?>  
<schema targetNamespace='http://schemas.microsoft.com/windows/2005/03/printing/bidi'  
    xmlns:bidi='http://schemas.microsoft.com/windows/2005/03/printing/bidi'   
    xmlns ='http://www.w3.org/2001/XMLSchema'>  
    <element name='GetWithArgumentResponse'>  
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
                                            <element name='Error'       type='integer'/>  
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
