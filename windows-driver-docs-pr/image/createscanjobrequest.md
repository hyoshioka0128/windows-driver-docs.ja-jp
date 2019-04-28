---
title: CreateScanJobRequest 要素
description: 必要な CreateScanJobRequest 操作では、スキャンするスキャン デバイスを準備します。
ms.assetid: ce3aafe2-71b0-4875-852a-f3ab78684329
keywords:
- CreateScanJobRequest 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn CreateScanJobRequest
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8221ab8d8df854c6a32b280ab29898afd21e196a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368544"
---
# <a name="createscanjobrequest-element"></a>CreateScanJobRequest 要素


必要な**CreateScanJobRequest**操作をスキャンするスキャン デバイスを準備します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:CreateScanJobRequest>
  child elements
</wscn:CreateScanJobRequest>
```

<a name="attributes"></a>属性
----------

属性はありません。

<a name="text-value"></a>テキスト値
----------

なし

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
<td><p><a href="destinationtoken.md" data-raw-source="[&lt;strong&gt;DestinationToken&lt;/strong&gt;](destinationtoken.md)"><strong>DestinationToken</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="scanidentifier.md" data-raw-source="[&lt;strong&gt;ScanIdentifier&lt;/strong&gt;](scanidentifier.md)"><strong>ScanIdentifier</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="scanticket.md" data-raw-source="[&lt;strong&gt;ScanTicket&lt;/strong&gt;](scanticket.md)"><strong>ScanTicket</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>親要素


親要素はありません。

<a name="remarks"></a>注釈
-------

WSD スキャン サービスをサポートする必要があります、 **CreateScanJobRequest**操作。

**CreateScanJobRequest**操作は、メインのメカニズムを使用することは画像をスキャンするスキャン デバイスを準備します。 この操作は、2 つの方法で開始できます。 各メソッドは別に引数を渡す**CreateScanJobRequest**します。 2 つのメソッドと引数は。

-   ユーザーは、変換先を選択し、[スキャン] ボタンをデバイスにプッシュします。 このメソッドは、クライアントが送信を**CreateScanJobRequest**次の子要素を使用します。
    -   スキャン サービスが ScanAvailableEvent を使用してクライアントに返す ScanIdentifier 要素。 スキャン サービスは、ユーザーが、変換先を選択した後、正しいクライアントがスキャンを要求することを確認するには、この識別子を確認する必要があります。
    -   DestinationToken 要素は、受信 ScanAvailableEvent イベントをサブスクライブしたときに、WSD スキャン サービスがクライアントに返します。 スキャン サービスは、適切なクライアントがこのトークンをチェックして、スキャンを要求することを確認する必要があります。
    -   スキャンの処理を制御する ScanTicket 要素。 スキャン チケット内の値は、ユーザーに、デバイスのスキャンを開始する前に、クライアント側で設定されている既定値です。
-   ユーザーは、クライアントで、アプリケーションを起動し、イメージを取得します。 このメソッドは、クライアントが送信**CreateScanJobRequest**だけを持つ、 **ScanTicket**要素。

特定の要素内で、 **CreateScanJobRequest**階層に含めることができます、 **MustHonor**ブール属性。 場合**MustHonor**が存在し、true の場合、WSD スキャン サービスが要求された要素とその値を維持するかスキャン ジョブ要求を拒否する必要があります。 サポートされていない要素がない場合、 **MustHonor**属性、またはその**MustHonor**属性が false で、WSD スキャン サービスは、それを無視する必要があります。 サポートされている要素の場合、 **MustHonor**属性が false で、WSD スキャン サービスがその要求された値でサポートされている必要があります。

クライアントが競合するスキャン ジョブ要求内の要素の組み合わせを提供するかどうか (など[**指定**](inputsource.md)と[**解決**](resolution.md))、競合している要素がある場合、WSD スキャン サービスでスキャン ジョブの要求を拒否する必要があります、 **MustHonor**属性の値は true。

次の要素を持つことができます、 **MustHonor**属性。[**ColorProcessing**](colorprocessing.md)、 [ **CompressionQualityFactor**](compressionqualityfactor.md)、 [ **ContentType**](contenttype.md)、 [**露出**](exposure.md)、 [ **FilmScanMode**](filmscanmode.md)、 [ **ImagesToTransfer** ](imagestotransfer.md)、 [ **InputSize**](inputsize.md)、 [**指定**](inputsource.md)、 [ **MediaSides** ](mediasides.md)、 [**解決**](resolution.md)、 [**回転**](rotation.md)、 [**スケーリング** ](scaling.md)、 [ **ScanRegionHeight**](scanregionheight.md)、 [ **ScanRegionWidth**](scanregionwidth.md)、 [**ScanRegionXOffset**](scanregionxoffset.md)、および[ **ScanRegionYOffset**](scanregionyoffset.md)します。

この操作は、のすべてを返すことができます、 [ **WSD スキャン サービス操作の一般的なエラー コード**](common-wsd-scan-service-operation-error-codes.md)します。 エラーを報告する方法の詳細については、次を参照してください。 [WSD スキャン サービス操作エラー報告](wsd-scan-service-operation-error-reporting.md)します。

**CreateScanJobRequest**次のエラーを返すこともできます。

-   **ServerErrorNotAcceptingJobs**サーバーは、新しいスキャン ジョブを受け入れることはできません。 スキャナーがサービス モードに設定されているため、またはユーザーの介入の条件があり、すべてのメモリ バッファーがなくなるために、このエラーが発生する可能性があります。 クライアントでは、スキャナーでは、ジョブをもう一度同意は、サーバーがブロックされていないになり、という前提で時間の後でもう一度変更されていない要求を再試行できます。

    | Fault プロパティ | 定義                                                                         |
    |----------------|------------------------------------------------------------------------------------|
    | \[コード\]       | soap の受信者:                                                                      |
    | \[サブコード\]    | wscn:ServerErrorNotAcceptingJobs                                                   |
    | \[Reason\]     | サービスが一時的にブロックされて、新しいジョブまたはドキュメントの要求を受け入れることはできません。 |
    | \[詳細\]     | なし                                                                               |

     

-   **ClientErrorFormatNotSupported**スキャナーは指定された形式の値をサポートしていません。

    | Fault プロパティ | 定義                                                                                                                                      |
    |----------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
    | \[コード\]       | soap 送信者:                                                                                                                                     |
    | \[サブコード\]    | wscn:ClientErrorFormatNotSupported                                                                                                              |
    | \[Reason\]     | ドキュメント形式のパラメーター値がサポートされていません。                                                                                           |
    | \[詳細\]     | (省略可能)。 スキャン サービスは、サポートされている形式の一覧を返すことができます。 この要素のデータ型でなければなりません&lt;wscn:FormatSupportedType&gt;します。 |

     

-   **ClientErrorInvalidScanIdentifier** ScanIdentifier 値として指定したが、スキャン デバイス内で現在無効です。

    | Fault プロパティ | 定義                                                 |
    |----------------|------------------------------------------------------------|
    | \[コード\]       | soap 送信者:                                                |
    | \[サブコード\]    | wscn:ClientErrorInvalidScanIdentifier                      |
    | \[Reason\]     | ScanIdentifier パラメーターの値は現在無効です。 |
    | \[詳細\]     | なし                                                       |

     

-   **ClientErrorInvalidDestinationToken** DestinationToken 値として指定したが、デバイスのスキャンを無効です。

    | Fault プロパティ | 定義                                                   |
    |----------------|--------------------------------------------------------------|
    | \[コード\]       | soap 送信者:                                                  |
    | \[サブコード\]    | wscn:ClientErrorInvalidDestinationToken                      |
    | \[Reason\]     | DestinationToken パラメーターの値は現在無効です。 |
    | \[詳細\]     | なし                                                         |

     

-   **ClientErrorNoImagesAvailable**スキャンするメディアがないため、サーバーが新しいスキャン ジョブを受け入れることはできません。 たとえば、スキャナーに接続されている自動ドキュメント フィーダーからスキャン ジョブを実行して、フィーダーが空、このエラーが生成されます。 クライアントは、条件は修正され、スキャナーがスキャンされるメディアになりましたことを見込んで変更されていない要求を後でもう一度試すことができます。

    | Fault プロパティ | 定義                                     |
    |----------------|------------------------------------------------|
    | \[コード\]       | soap 送信者:                                    |
    | \[サブコード\]    | wscn:ClientErrorNoImagesAvailable              |
    | \[Reason\]     | サーバーには、取得に使用できるイメージがありません。 |
    | \[詳細\]     | なし                                           |

     

<a name="examples"></a>例
--------

次のコード例は、スキャンのデバイスからスキャンが開始されると、スキャン ジョブの要求を示します。

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
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/CreateScanJob
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:CreateScanJobRequest>
      <wscn:ScanIdentifier>
        uuid:12e7a983-1034-5428-d298-0016f11097fa
      </wscn:ScanIdentifier>
      <wscn:DestinationToken>
        Dest1234TokenString
      </wscn:DestinationToken>
      <wscn:ScanTicket>
        <wscn:JobDescription>
          <wscn:JobName>Photo Scan</wscn:JobName>
          <wscn:JobOriginatingUserName>RogerSmith</JobOriginatingUserName>
        </wscn:JobDescription>
        <wscn:DocumentParameters>
          <wscn:Format>jfif</wscn:Format>
          <wscn:CompressionQualityFactor>45</wscn:CompressionQualityFactor>
          <wscn:InputSource>Platen</wscn:InputSource>
          <wscn:ContentType>Auto</wscn:ContentType>
          <wscn:InputSize>
            <wscn:DocumentSizeAutoDetect>true</wscn:DocumentSizeAutoDetect>
          </wscn:InputSize>
          <wscn:Scaling wscn:MustHonor="1">
            <wscn:ScalingWidth>125</wscn:ScalingWidth>
            <wscn:ScalingHeight>125</wscn:ScalingHeight>
          </wscn:Scaling>
          <wscn:MediaSides>
            <wscn:MediaFront>
              <wscn:Resolution wscn:MustHonor="1">
                <wscn:Width>300</wscn:Width>
                <wscn:Height>300</wscn:Height>
              </wscn:Resolution>
            </wscn:MediaFront>
          </wscn:MediaSides>
        </wscn:DocumentParameters>
      </wscn:ScanTicket>
    </wscn:CreateScanJobRequest>
  </soap:Body>
</soap:Envelope>
```

次のコード例は、クライアント上のアプリケーションから、スキャンが開始されると、スキャン ジョブの要求を示します。

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
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/CreateScanJob
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:CreateScanJobRequest>
      <wscn:ScanTicket>
        <wscn:JobDescription>
          <wscn:JobName>Application Scan</wscn:JobName>
          <wscn:JobOriginatingUserName>RogerSmith</JobOriginatingUserName>
        </wscn:JobDescription>
        <wscn:DocumentParameters>
          <wscn:Format>xps</wscn:Format>
          <wscn:ImagesToTransfer>0</wscn:ImagesToTransfer>
          <wscn:InputSource>ADF</wscn:InputSource>
          <wscn:ContentType>Auto</wscn:ContentType>
          <wscn:InputSize>
            <wscn:DocumentSizeAutoDetect>true</wscn:DocumentSizeAutoDetect>
          </wscn:InputSize>
          <wscn:MediaSides>
            <wscn:MediaFront>
              <wscn:ColorProcessing>RGB48</wscn:ColorProcessing>
              <wscn:Resolution>
                <wscn:Width>1200</wscn:Width>
              </wscn:Resolution>
            </wscn:MediaFront>
          </wscn:MediaSides>
        </wscn:DocumentParameters>
        <wscn:DocumentDescription>
          <wscn:DocumentName>Scan001.jpg</DocumentName>
        </wscn:DocumentDescription>
      </wscn:ScanTicket>
    </wscn:CreateScanJobRequest>
  </soap:Body>
</soap:Envelope>
```

## <a name="see-also"></a>関連項目


[**ColorProcessing**](colorprocessing.md)

[**CompressionQualityFactor**](compressionqualityfactor.md)

[**ContentType**](contenttype.md)

[**CreateScanJobResponse**](createscanjobresponse.md)

[**DestinationToken**](destinationtoken.md)

[**公開**](exposure.md)

[**FilmScanMode**](filmscanmode.md)

[**ImagesToTransfer**](imagestotransfer.md)

[**InputSize**](inputsize.md)

[**指定**](inputsource.md)

[**MediaSides**](mediasides.md)

[**解決方法**](resolution.md)

[**回転**](rotation.md)

[**スケーリング**](scaling.md)

[**ScanAvailableEvent**](scanavailableevent.md)

[**ScanIdentifier**](scanidentifier.md)

[**ScanRegionHeight**](scanregionheight.md)

[**ScanRegionWidth**](scanregionwidth.md)

[**ScanRegionXOffset**](scanregionxoffset.md)

[**ScanRegionYOffset**](scanregionyoffset.md)

[**ScanTicket**](scanticket.md)

 

 






