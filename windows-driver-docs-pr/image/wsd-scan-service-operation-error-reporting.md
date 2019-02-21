---
title: WSD スキャン サービス操作エラー報告
description: WSD スキャン サービス操作エラー報告
ms.assetid: 78cf0cf9-f792-4dc9-b0df-c45b408b85ab
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6bf2e54facd2894bcd7320938b6a8ed971883371
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560066"
---
# <a name="wsd-scan-service-operation-error-reporting"></a>WSD スキャン サービス操作エラー報告


このセクションでは、WSD スキャン サービスが生成し、操作のエラー コードを送信する方法について説明します。 ほとんどの操作で返すことができるエラー コードの記述で[**共通 WSD スキャン サービス操作のエラー コード**](common-wsd-scan-service-operation-error-codes.md)します。

WSD スキャン サービスが、処理中にエラーが検出した場合、 *Xxx * * * 要求** の代わりにエラー コードを返しますが、操作、 *Xxx * * * 応答** 要素です。 スキャン サービスのエラー コードを返します、 **&lt;soap エラー:&gt;** 要素。

記載されている規則に従って WSD スキャン サービス内で定義されているすべてのエラー メッセージを送信する必要があります、 [Web Services Addressing (Ws-addressing) 仕様](https://go.microsoft.com/fwlink/p/?linkid=70144)します。 具体的には、WSD スキャン サービスでは、次の場所に順番にフォールト メッセージを送信する必要があります。

1.  \[フォールト エンドポイント\]存在し、有効である場合、します。

2.  それ以外の場合、\[エンドポイントを返信\]が存在する場合は、します。

3.  それ以外の場合、\[ソース エンドポイント\]します。

エンドポイントは、すべてのエラー メッセージで必要なメッセージはヘッダーを含める必要があります。 使用して返信としてエラー メッセージが関連付けられる、\[リレーションシップ\]Ws-addressing で定義されているプロパティ。 次\[アクション\]プロパティは、エラー メッセージを指定します。

```xml
http://schemas.xmlsoap.org/ws/2004/08/addressing/fault
```

エラーの定義は、次のプロパティを使用します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fault プロパティ</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>[コード]</p></td>
<td><p>エラー コード。</p></td>
</tr>
<tr class="even">
<td><p>[サブコード]</p></td>
<td><p>エラーのサブコード。</p></td>
</tr>
<tr class="odd">
<td><p>[理由]</p></td>
<td><p>英語理由要素。</p></td>
</tr>
<tr class="even">
<td><p>[詳細]</p></td>
<td><p>詳細要素。 この要素が存在しない場合はエラーに detail 要素は定義されません。</p></td>
</tr>
</tbody>
</table>

 

次のコード例に示すように、これらのプロパティが SOAP 1.2 エラーにバインドします。

```xml
<S:Envelope>
  <S:Header>
    <wsa:Action>http://schemas.xmlsoap.org/ws/2004/08/addressing/fault</wsa:Action>
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

次のコード例は、SOAP の例を示しています。**フォールト**します。

```xml
<soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soapelope"
    xmlns:xml="http://www.w3.org/XML/1998/namespace"
    xmlns:wsa="http://schemas.xmlsoap.org/ws/2004/08/addressing"
    xmlns:nprt="http://schemas.microsoft.com/windows/2006/01/wdp/scan">
  <soap:Header>
    <wsa:Action>http://schemas.xmlsoap.org/ws/2004/08/addressing/fault</wsa:Action>
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

 

 





