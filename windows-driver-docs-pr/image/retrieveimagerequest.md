---
title: RetrieveImageRequest 要素
description: RetrieveImageRequest 操作の必要な要素には、クライアントのスキャン ジョブが作成された後、デバイスからスキャン データを取得する要求が含まれています。
ms.assetid: 4f6d6bd0-b323-4f95-b380-2be9cec1ee6e
keywords:
- RetrieveImageRequest 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn RetrieveImageRequest
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0023e7ca3f8211e5d626455ae634e983b79145c2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582486"
---
# <a name="retrieveimagerequest-element"></a>RetrieveImageRequest 要素


必要な**RetrieveImageRequest**操作の要素には、クライアントのスキャン ジョブが作成された後、デバイスからスキャン データを取得する要求が含まれています。

<a name="usage"></a>使用方法
-----

```xml
<wscn:RetrieveImageRequest>
  child elements
</wscn:RetrieveImageRequest>
```

<a name="attributes"></a>属性
----------

属性はありません。

## <a name="child-elements"></a>子要素


<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="documentdescription.md" data-raw-source="[&lt;strong&gt;DocumentDescription&lt;/strong&gt;](documentdescription.md)"><strong>DocumentDescription</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobid.md" data-raw-source="[&lt;strong&gt;JobId&lt;/strong&gt;](jobid.md)"><strong>JobId</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="jobtoken.md" data-raw-source="[&lt;strong&gt;JobToken&lt;/strong&gt;](jobtoken.md)"><strong>JobToken</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>親要素


親要素はありません。

<a name="remarks"></a>コメント
-------

WSD スキャン サービスをサポートする必要があります、 **RetrieveImageRequest**操作の要素。

スキャン サービスを検証する必要があります、 [ **JobId** ](jobid.md)と[ **JobToken** ](jobtoken.md)ジョブが有効であることを確認するクライアントを提供する要素と取得を要求しているクライアントによって作成されました。 スキャン サービスが応答する必要があります、要求が有効な場合、 [ **RetrieveImageResponse** ](retrieveimageresponse.md)操作の要素。

この操作は、のすべてを返すことができます、 [ **WSD スキャン サービス操作の一般的なエラー コード**](common-wsd-scan-service-operation-error-codes.md)します。 エラーを報告する方法の詳細については、次を参照してください。 [WSD スキャン サービス操作エラー報告](wsd-scan-service-operation-error-reporting.md)します。

この操作は、次のエラーを返すも可能性があります。

-   **ClientErrorJobIdNotFound**スキャナーは、ジョブ Id 値と一致するジョブを見つけることができませんまたはジョブ Id 値が定義された範囲内です。

    | Fault プロパティ | 定義                         |
    |----------------|------------------------------------|
    | \[コード\]       | soap 送信者:                        |
    | \[サブコード\]    | wscn:ClientErrorJobIdNotFound      |
    | \[理由\]     | 指定したジョブ Id が見つかりませんでした。 |
    | \[詳細\]     | JobId:JobId が正しくありません。             |

     

-   **ClientErrorNoImagesAvailable**スキャナーには、クライアントを取得するために使用できるその他のイメージはありません。

    | Fault プロパティ | 定義                                     |
    |----------------|------------------------------------------------|
    | \[コード\]       | soap 送信者:                                    |
    | \[サブコード\]    | wscn:ClientErrorNoImagesAvailable              |
    | \[理由\]     | サーバーには、取得に使用できるイメージがありません。 |
    | \[詳細\]     | なし                                           |

     

-   **ClientErrorInvalidJobToken**JobToken 値として指定したが、指定したスキャン JobId 無効です。

    | Fault プロパティ | 定義                                                          |
    |----------------|---------------------------------------------------------------------|
    | \[コード\]       | soap 送信者:                                                         |
    | \[サブコード\]    | wscn:ClientErrorInvalidJobToken                                     |
    | \[理由\]     | JobId パラメーターを持つ JobToken パラメーターの値が正しくありません。 |
    | \[詳細\]     | なし                                                                |

     

-   **ClientErrorJobCancelled**

    | Fault プロパティ | 定義                              |
    |----------------|-----------------------------------------|
    | \[コード\]       | soap 送信者:                             |
    | \[サブコード\]    | wscn:ClientErrorJobCancelled            |
    | \[理由\]     | 現在のスキャン ジョブが取り消されました。 |
    | \[詳細\]     | なし                                    |

     

<a name="examples"></a>使用例
--------

次のコード例では、JobId 1 によって識別されるジョブのイメージ データを取得するクライアント要求を示しています。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="http://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:wscn="http://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='http://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>AddressofScannerService</wsa:To>
    <wsa:Action>
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/RetrieveImage
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:RetrieveImageRequest>
      <wscn:JobId>1</wscn:JobId>
      <wscn:JobToken>Job9876TokenString</wscn:JobToken>
      <wscn:DocumentDescription>
        <wscn:DocumentName>Scan001.jpg</DocumentName>
      </wscn:DocumentDescription>
    </wscn:RetrieveImageRequest>
  </soap:Body>
</soap:Envelope>
```

## <a name="see-also"></a>関連項目


[**DocumentDescription**](documentdescription.md)

[**JobId**](jobid.md)

[**JobToken**](jobtoken.md)

[**RetrieveImageResponse**](retrieveimageresponse.md)

 

 






