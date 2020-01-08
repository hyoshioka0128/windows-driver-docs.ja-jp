---
title: RetrieveImageRequest 要素
description: Required RetrieveImageRequest operation 要素には、スキャンジョブの作成後にデバイスからスキャンデータを取得するためのクライアントの要求が含まれています。
ms.assetid: 4f6d6bd0-b323-4f95-b380-2be9cec1ee6e
keywords:
- RetrieveImageRequest 要素イメージングデバイス
topic_type:
- apiref
api_name:
- wscn RetrieveImageRequest
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf1c5900fce4ef892f9ba129f182c9dc04cecf01
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652946"
---
# <a name="retrieveimagerequest-element"></a>RetrieveImageRequest 要素


Required **RetrieveImageRequest** operation 要素には、スキャンジョブの作成後にデバイスからスキャンデータを取得するためのクライアントの要求が含まれています。

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

<a name="remarks"></a>注釈
-------

WSD Scan サービスは、 **RetrieveImageRequest** operation 要素をサポートしている必要があります。

スキャンサービスは、ジョブが有効であり、取得を要求しているクライアントによって作成されたことを確認するために、クライアントが提供する[**JobId**](jobid.md)および[**jobtoken**](jobtoken.md)要素を検証する必要があります。 要求が有効な場合、スキャンサービスは[**RetrieveImageResponse**](retrieveimageresponse.md) operation 要素を使用して応答する必要があります。

この操作は、[**一般的な WSD Scan サービス操作のエラーコード**](common-wsd-scan-service-operation-error-codes.md)をすべて返すことができます。 エラーを報告する方法の詳細については、「 [WSD Scan サービス操作のエラー報告](wsd-scan-service-operation-error-reporting.md)」を参照してください。

この操作では、次のエラーが返されることもあります。

-   **ClientErrorJobIdNotFound**スキャナーが JobId 値に一致するジョブを見つけることができません。または、JobId 値が定義された範囲内にありません。

    | Fault プロパティ | 定義                         |
    |----------------|------------------------------------|
    | \[コード\]       | soap: 送信者                        |
    | \[サブコード\]    | wscn: ClientErrorJobIdNotFound      |
    | \[Reason\]     | 指定された JobId が見つかりませんでした。 |
    | \[詳細\]     | JobId: JobId が正しくありません             |

     

-   **ClientErrorNoImagesAvailable**スキャナーにクライアントが取得できるイメージがありません。

    | Fault プロパティ | 定義                                     |
    |----------------|------------------------------------------------|
    | \[コード\]       | soap: 送信者                                    |
    | \[サブコード\]    | wscn: ClientErrorNoImagesAvailable              |
    | \[Reason\]     | サーバーで取得できるイメージがありません。 |
    | \[詳細\]     | None                                           |

     

-   **Clienterrorinvalidjobtoken**指定された JobToken 値は、指定されたスキャンジョブ Id に対して無効です。

    | Fault プロパティ | 定義                                                          |
    |----------------|---------------------------------------------------------------------|
    | \[コード\]       | soap: 送信者                                                         |
    | \[サブコード\]    | wscn: ClientErrorInvalidJobToken                                     |
    | \[Reason\]     | JobToken パラメーター値は、JobId パラメーターでは無効です。 |
    | \[詳細\]     | None                                                                |

     

-   **ClientErrorJobCancelled れました**

    | Fault プロパティ | 定義                              |
    |----------------|-----------------------------------------|
    | \[コード\]       | soap: 送信者                             |
    | \[サブコード\]    | wscn: ClientErrorJobCancelled 取り消されました            |
    | \[Reason\]     | 現在のスキャンジョブは取り消されました。 |
    | \[詳細\]     | None                                    |

     

<a name="examples"></a>例
--------

次のコード例は、JobId 1 で識別されるジョブのイメージデータを取得するクライアント要求を示しています。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="https://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:wscn="https://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='https://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>AddressofScannerService</wsa:To>
    <wsa:Action>
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/RetrieveImage
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

## <a name="see-also"></a>「


[**DocumentDescription**](documentdescription.md)

[**JobId**](jobid.md)

[**JobToken**](jobtoken.md)

[**RetrieveImageResponse**](retrieveimageresponse.md)

 

 






