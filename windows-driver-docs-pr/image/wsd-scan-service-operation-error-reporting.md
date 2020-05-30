---
title: WSD スキャン サービス操作エラー報告
description: WSD スキャン サービス操作エラー報告
ms.assetid: 78cf0cf9-f792-4dc9-b0df-c45b408b85ab
ms.date: 05/29/2020
ms.localizationpriority: medium
ms.openlocfilehash: fed607d22461edf55d8bb4400490d13a5b53778a
ms.sourcegitcommit: 609c5731b2db4c17b9959082c4621c001e012db1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/30/2020
ms.locfileid: "84223515"
---
# <a name="wsd-scan-service-operation-error-reporting"></a>WSD スキャン サービス操作エラー報告

このセクションでは、WSD スキャンサービスが操作のエラーコードを生成して送信する方法について説明します。 ほとんどの操作で返すことができるエラーコードについては、「 [**COMMON WSD Scan Service Operation Error コード**](common-wsd-scan-service-operation-error-codes.md)」で説明されています。

WSD スキャンサービスが*xxx *** * 要求 * 操作の処理中にエラーを検出すると、 *xxx *** * * * 要素ではなくエラーコードが返されます。 スキャンサービスは、 ** &lt; Soap: Fault &gt; **要素のエラーコードを返します。

WSD Scan サービス内で定義されているすべてのエラーメッセージは、 [Web サービスアドレス指定 (ws-addressing) 仕様](https://www.w3.org/Submission/ws-addressing/)で説明されている規則に従って送信する必要があります。 具体的には、WSD Scan サービスは次の場所にエラーメッセージを順番に送信する必要があります。

1. \[エラーエンドポイント \] (存在し、有効な場合)。

1. それ以外の \[ 場合は、応答エンドポイント \] (存在する場合)。

1. それ以外の場合は、 \[ ソースエンドポイント \] 。

エンドポイントには、すべてのエラーメッセージに必要なメッセージ情報ヘッダーを含める必要があります。 エラーメッセージは、 \[ \] ws-addressing で定義されているリレーションシッププロパティを使用して、応答として関連付けられます。 次の \[ アクション \] プロパティは、エラーメッセージを指定します。

```xml
https://schemas.xmlsoap.org/ws/2004/08/addressing/fault
```

エラーの定義には、次のプロパティが使用されます。

| Fault プロパティ | 定義 |
| --- | --- |
| コード | エラーコード。 |
| コード | エラーのサブコード。 |
| 理由 | English language reason 要素。 |
| データ | Detail 要素。 この要素が存在しない場合、エラーの詳細要素は定義されません。 |

これらのプロパティは、次のコード例に示すように、SOAP 1.2 エラーにバインドされます。

```xml
<S:Envelope>
  <S:Header>
    <wsa:Action>https://schemas.xmlsoap.org/ws/2004/08/addressing/fault</wsa:Action>
    <!-- Headers excluded for clarity -->
  </S:Header>
  <S:Body>
    <S:Fault>
      <S:Code>
        <S:Value>[Code]</S:Value>
        <S:Subcode>
          <S:Value>[Subcode]</S:Value>
        </S:Subcode>
      </S:Code>
      <S:Reason>
        <S:Text xml:lang="en">[Reason]</S:Text>
      </S:Reason>
      <S:Detail>[Detail]</S:Detail>
    </S:Fault>
  </S:Body>
</S:Envelope>
```

SOAP**エラー**の例を次のコード例に示します。

```xml
<soap:Envelope xmlns:soap="https://www.w3.org/2003/05/soapelope"
    xmlns:xml="https://www.w3.org/XML/1998/namespace"
    xmlns:wsa="https://schemas.xmlsoap.org/ws/2004/08/addressing"
    xmlns:nprt="https://schemas.microsoft.com/windows/2006/01/wdp/scan">
  <soap:Header>
    <wsa:Action>https://schemas.xmlsoap.org/ws/2004/08/addressing/fault</wsa:Action>
    <!-- Headers excluded for brevity -->
  </soap:Header>
  <soap:Body>
    <soap:Fault>
      <soap:Code>
        <soap:Value>env:Sender</soap:Value>
        <soap:Subcode>
          <soap:Value>wscn:OperationFailed</soap:Value>
        </soap:Subcode>
      </soap:Code>
      <soap:Reason>
        <soap:Text xml:lang="en">Service cannot perform the requested operation</soap:Text>
      </soap:Reason>
    </soap:Fault>
  </soap:Body>
</soap:Envelope>
```
