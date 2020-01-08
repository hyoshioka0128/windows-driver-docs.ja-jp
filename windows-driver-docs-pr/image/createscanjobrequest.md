---
title: /の要求要素
description: 必要なのは、スキャンデバイスをスキャンするように要求します。
ms.assetid: ce3aafe2-71b0-4875-852a-f3ab78684329
keywords:
- //ジョブ要求要素のイメージ作成デバイス
topic_type:
- apiref
api_name:
- wscn CreateScanJobRequest
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f03a0ab1e814a9dd4acf8a6df0ea7e92d9b7924c
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652988"
---
# <a name="createscanjobrequest-element"></a>/の要求要素


必要なのは、スキャンデバイスをスキャンするように**要求**します。

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

None

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
<td><p><a href="scanticket.md" data-raw-source="[&lt;strong&gt;ScanTicket&lt;/strong&gt;](scanticket.md)"><strong>スキャンチケット</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>親要素


親要素はありません。

<a name="remarks"></a>注釈
-------

WSD スキャン**サービスでは、"** /" をサポートする必要があります。

使用可能なイメージをスキャンするようにスキャンデバイスを準備する主なメカニズムとして、"ファイルの作成 **" 操作が**あります。 この操作は、2つの異なる方法で開始できます。 各メソッドは、異なる引数を///出力**要求**に送信します。 2つのメソッドと引数は次のとおりです。

-   ユーザーは、変換先を選択し、デバイスに [スキャン] ボタンをプッシュします。 このメソッドでは、クライアントは、次の子要素を使用して、の**出力を送信**します。
    -   スキャンサービスが Scanidentifier イベントを使用してクライアントに返す ScanIdentifier 要素。 スキャンサービスは、ユーザーが対象を選択した後に、正しいクライアントがスキャンを要求していることを確認するために、この識別子を確認する必要があります。
    -   スキャンが利用できるイベントイベントの受信をサブスクライブしているときに、WSD Scan サービスがクライアントに返す DestinationToken 要素。 スキャンサービスは、このトークンを確認することによって、正しいクライアントがスキャンを要求していることを確認する必要があります。
    -   スキャンの処理を制御するための ScanTicket 要素。 スキャンチケットの値は、ユーザーがデバイスにログオンしてからスキャンを開始する前にクライアントで設定される既定値です。
-   ユーザーは、クライアントでアプリケーションを起動し、イメージを取得します。 このメソッドでは、クライアントは**Scancanjobrequest**を**scanticket**要素だけで送信します。

**MustHonor**のブール属性を格納**できるのは、構成**要素の属性を持つことができます。 **MustHonor**が存在し、true の場合、WSD Scan サービスは要求された要素とその値を受け入れ、スキャンジョブ要求を拒否する必要があります。 サポートされていない要素に**MustHonor**属性がない場合、または**MustHonor**属性が FALSE の場合、WSD Scan サービスはそれを無視する必要があります。 サポートされている要素の**MustHonor**属性が false の場合、WSD Scan サービスは要求された値をサポートされているものと substitue 必要があります。

クライアントがスキャンジョブ要求で要素の競合する組み合わせ ( [**Inputsource**](inputsource.md)や[**Resolution**](resolution.md)など) を提供する場合、競合する要素の**MustHonor**属性値が true に設定されていると、WSD scan サービスはスキャンジョブ要求を拒否する必要があります。

**MustHonor**属性には、 [**colorprocessing**](colorprocessing.md)、 [**CompressionQualityFactor**](compressionqualityfactor.md)、 [**ContentType**](contenttype.md)、[**露光**](exposure.md)、 [**filmscanmode**](filmscanmode.md)、 [**ImagesToTransfer**](imagestotransfer.md)、 [**inputsize**](inputsize.md)、 [**inputsize**](inputsource.md)、 [**mediasides**](mediasides.md)、 [**Resolution**](resolution.md)、 [**Rotation**](rotation.md)、 [**Scaling**](scaling.md)、 [**scanregionheight**](scanregionheight.md)、 [**scanregionheight**](scanregionwidth.md)、 [**scanregionxoffset**](scanregionxoffset.md)、および[**ScanRegionYOffset**](scanregionyoffset.md)の各要素を含めることができます。

この操作は、[**一般的な WSD Scan サービス操作のエラーコード**](common-wsd-scan-service-operation-error-codes.md)をすべて返すことができます。 エラーを報告する方法の詳細については、「 [WSD Scan サービス操作のエラー報告](wsd-scan-service-operation-error-reporting.md)」を参照してください。

また、この**要求**は、次のエラーを返すこともできます。

-   **Servererrornotacceptingjobs**サーバーは、新しいスキャンジョブを受け付けることができません。 このエラーは、スキャナーがサービスモードになったか、ユーザーの介入条件があり、すべてのメモリバッファーが使い果たされたことが原因で発生する可能性があります。 クライアントは、サーバーがブロック解除され、スキャナーがジョブを再度受け入れることを見込んで、変更されていない要求を後でもう一度試すことができます。

    | Fault プロパティ | 定義                                                                         |
    |----------------|------------------------------------------------------------------------------------|
    | \[コード\]       | soap: レシーバー                                                                      |
    | \[サブコード\]    | wscn: ServerErrorNotAcceptingJobs                                                   |
    | \[Reason\]     | サービスは一時的にブロックされ、新しいジョブまたはドキュメント要求を受け入れることができません。 |
    | \[詳細\]     | None                                                                               |

     

-   **ClientErrorFormatNotSupported**スキャナーは、指定されたフォーマット値をサポートしていません。

    | Fault プロパティ | 定義                                                                                                                                      |
    |----------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
    | \[コード\]       | soap: 送信者                                                                                                                                     |
    | \[サブコード\]    | wscn: ClientErrorFormatNotSupported                                                                                                              |
    | \[Reason\]     | ドキュメント形式のパラメーター値はサポートされていません。                                                                                           |
    | \[詳細\]     | (省略可能)。 スキャンサービスは、サポートされている形式の一覧を返すことができます。 この要素のデータは、wscn: FormatSupportedType&gt;&lt;型である必要があります。 |

     

-   **Clienterrorinvalidscanidentifier**指定された ScanIdentifier 値は、現在、スキャンデバイス内では有効ではありません。

    | Fault プロパティ | 定義                                                 |
    |----------------|------------------------------------------------------------|
    | \[コード\]       | soap: 送信者                                                |
    | \[サブコード\]    | wscn: ClientErrorInvalidScanIdentifier                      |
    | \[Reason\]     | ScanIdentifier パラメーターの値が現在有効ではありません。 |
    | \[詳細\]     | None                                                       |

     

-   **Clienterrorinvaliddestinationtoken**指定された DestinationToken 値はスキャンデバイスに対して無効です。

    | Fault プロパティ | 定義                                                   |
    |----------------|--------------------------------------------------------------|
    | \[コード\]       | soap: 送信者                                                  |
    | \[サブコード\]    | wscn: ClientErrorInvalidDestinationToken                      |
    | \[Reason\]     | DestinationToken パラメーター値は現在有効ではありません。 |
    | \[詳細\]     | None                                                         |

     

-   **ClientErrorNoImagesAvailable**スキャンするメディアがないため、サーバーは新しいスキャンジョブを受け入れることができません。 たとえば、スキャナーに接続されている自動ドキュメントフィーダーからスキャンジョブが実行され、フィーダーが空の場合に、このエラーが生成されます。 クライアントは、条件が修正されたことを見込んで、変更されていない要求を後でもう一度試すことができます。また、スキャナーにはメディアがスキャンされるようになります。

    | Fault プロパティ | 定義                                     |
    |----------------|------------------------------------------------|
    | \[コード\]       | soap: 送信者                                    |
    | \[サブコード\]    | wscn: ClientErrorNoImagesAvailable              |
    | \[Reason\]     | サーバーで取得できるイメージがありません。 |
    | \[詳細\]     | None                                           |

     

<a name="examples"></a>例
--------

次のコード例は、スキャンがスキャンデバイスから開始されたときのスキャンジョブ要求を示しています。

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
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/CreateScanJob
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

次のコード例は、スキャンがクライアント上のアプリケーションから開始されたときのスキャンジョブ要求を示しています。

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
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/CreateScanJob
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

## <a name="see-also"></a>「


[**ColorProcessing**](colorprocessing.md)

[**CompressionQualityFactor**](compressionqualityfactor.md)

[**ContentType**](contenttype.md)

[ **//ジョブ応答**](createscanjobresponse.md)

[**DestinationToken**](destinationtoken.md)

[**見る**](exposure.md)

[**FilmScanMode**](filmscanmode.md)

[**ImagesToTransfer**](imagestotransfer.md)

[**InputSize**](inputsize.md)

[**InputSource**](inputsource.md)

[**MediaSides**](mediasides.md)

[**解決**](resolution.md)

[**ローテーション**](rotation.md)

[**幅**](scaling.md)

[**スキャンが発生したイベント**](scanavailableevent.md)

[**ScanIdentifier**](scanidentifier.md)

[**ScanRegionHeight**](scanregionheight.md)

[**ScanRegionWidth**](scanregionwidth.md)

[**ScanRegionXOffset**](scanregionxoffset.md)

[**ScanRegionYOffset**](scanregionyoffset.md)

[**スキャンチケット**](scanticket.md)

 

 






