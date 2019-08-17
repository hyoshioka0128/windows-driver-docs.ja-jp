---
title: Wi-fi 探索サービスの概要
description: Wi-fi 探索サービスの概要
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7df6dd1bbac3ef1ddb59cb126985ef09beb486f0
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565720"
---
# <a name="wi-fi-discovery-service-overview"></a>Wi-fi 探索サービスの概要

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]

Wi-fi 探索サービスを使用すると、ユーザーは携帯ネットワークトラフィックを Wi-fi ホットスポットにオフロードすることで、データコストを削減することができます。 探索サービスは、携帯電話などのプロバイダーから Wi-fi ホットスポットデータを集約して、既知の Wi-fi ホットスポットのディレクトリを作成します。 このディレクトリを使用して、ユーザーは現在の位置の近くにあるホットスポットに関する情報を取得できます。

携帯電話事業者は、HTTP POST 要求を送信するか、Microsoft によって提供されるコマンドラインツールを使用して、サービスにホットスポットデータを送信できます。

## <a name="instructions"></a>手順

Wi-fi ホットスポットデータは、「 [Wi-fi Hotspot データ送信形式](wi-fi-hotspot-data-submission-format.md)」で説明されている形式にする必要があります。

探索サービスでは、すべてのプロバイダーのホットスポットが1つのバッチで送信される必要があります。 各バッチには、少量のデータを含む複数の送信要求を含めることができます。 たとえば、1000のホットスポットを含むバッチを探索サービスにアップロードするには、それぞれに100ホットスポットのデータを含む10個の送信要求を送信します。 各送信要求には、同じバッチ番号が割り当てられます。 最終的な送信要求には、 `X-FinalBatchRequest`バッチ内のホットスポットの合計数に設定されたヘッダーを含める必要があります。 このヘッダーを持つ送信要求が受信されるまで、バッチは処理されません。 ヘッダーがバッチ内のホットスポットの数と一致しない場合、送信は処理されません。

### <a name="submitting-hotspot-data-by-using-http-post"></a>HTTP POST を使用したホットスポットデータの送信

次の例は、一般的な送信要求を示しています。 `X-FinalBatchRequest`ヘッダーが存在し、数値が "1" の場合は、このバッチにホットスポットが1つしかないことを示しています。これは最終的な送信要求です。 そのため、これは唯一の送信要求です。 バッチに複数のホットスポットが含まれている場合は、すべての送信要求に対してこの行を削除する必要があります。

```http
POST https://submitwifiservice.windowsphone.com/v1/SubmitHotspots HTTP/1.1
Content-Type: application/json
X-FinalBatchRequest: 1
 [More headers…]
{
      "Header": {
            "BatchId": "2E20A8DB-9AFA-4A5A-AF6E-5F87DA639C15", 
            "TransactionId": 1, 
            "ProviderId": "FD9E5EE6-75C7-4A54-8B29-45A3FC83AD63"
      }, 
      "Hotspots": {
            "add": {
                  "Address": "123 abc street", 
                  "City": "Redmond", 
                  "CountryOrRegion": "USA", 
                  "PostalCode": "98052", 
                  "StateOrProvince": "WA"
            },

            "bssids":["00:aa:bb:cc:dd:ee"],
            "free": true, 
            "pub": true, 
            "loc": {
                  "Latitude": 47.01, 
                  "Longitude": 121.1234, 
                  "RadialUncertainty": 300, 
                  "Altitude": 638.34, 
                  "AltitudeUncertainty": 100.0 
            }, 
            "name": "Joes Coffee Shop", 
            "phid": "abcdefg", 
            "ran": 100, 
            "ssid": "JoesCoffee", 
            "phone": ["425-882-8080"]
      }
}
```

送信先サーバーでメッセージが受信されると、サブスポットデータを探索サービスに送信する前に、 **Submithotspots**が要求を検証し、送信側を認証します。

### <a name="submitting-hotspot-data-by-using-the-command-line-tool"></a>コマンドラインツールを使用したホットスポットデータの送信

WifiProviderExe は、Microsoft によって提供されるコマンドラインツールであり、ホットスポットデータファイルを入力として受け取り、それを必要な形式に変換し、指定された探索サービスサーバーにアップロードします。

WiFiProvider を実行するには、次の構文を使用します。

```cmd
WifiProviderExe –DataFile filename -ProviderId GUID -ServiceEndpoint URL -CustomTransformer filename.dll [-MappingFile filename.xml] [-CertFile filename.pfx] [-CertPassword password] [-CertSubject name]
```

以下に例を示します。

```cmd
WifiProviderExe -DataFile "file.txt" -ProviderId 00000000-0000-0000-0000-000000000000 -ServiceEndpoint "https://submitwifiservice.windowsphone.com/v1/SubmitHotspots" -CustomTransformer "transformer.dll"
```

次の表に、WiFiProvider で使用できるパラメーターの一覧を示します。

| パラメーター | 説明 |
| --- | --- |
| データ | 必須。 ホットスポットデータを含むファイルの名前。 |
| ProviderId | 必須。 Microsoft によって割り当てられたプロバイダー ID (GUID)。 |
| ServiceEndpoint | 必須。 ホットスポットデータのアップロード先となる探索サービスサーバーの URL。 例、 https://wifi.windowsphone.com/v1/submithotspots |
| 顧客のトランスフォーマー | 必須。 トランスフォーマーを含むアセンブリの名前。 | 
| MappingFile | 任意。 プロバイダーのホットスポットデータを探索サービスが必要とする形式にマップするマッピングファイル。 |
| CertFile | 任意。 認証用の証明書を含む実際の pfx ファイルへのポインター。 この認証方法を使用する場合は、証明書パスワードパラメーター (**certpassword**) を指定する必要があります。 |
| CertPassword | 任意。 **CertFile**に指定された証明書のパスワード。 |
| CertSubject | 任意。 証明書のサブジェクト名。 現在のユーザーの My Cert ストアに配置されています。 この認証メカニズムを使用する場合、 **CertFile**と**certpassword**は必要ありません。 ただし、証明書の秘密キーを作成し、アクセス制御リストでその証明書を使用するアカウントにキーのアクセス権を付与する必要があります。 |

#### <a name="transformers"></a>トランスフォーマー

ホットスポットデータは任意の形式にすることができます。 ただし、ホットスポットデータを探索サービスで必要な形式に変換するために、コマンドラインツールがアクセスできる "データトランスフォーマー" を指定する必要があります。

次の表は、コマンドラインツールで提供されるサンプルのトランスフォーマーを示しています。 特定のデータ形式を必要な形式に変換するために使用できます。

| 変換 | データ形式 | 説明 |
| --- | --- | --- |
| WifiService. JsonHotspotDataTransformer..... | JSON | データは、 [Wi-fi ホットスポットデータ送信形式](wi-fi-hotspot-data-submission-format.md)で指定された JSON 形式に準拠している必要があります。 |
| WifiService. JsonHotspotDataTransformer..... | 単純な Excel | マッピングファイルを指定する必要があります。 |

#### <a name="mapping-files"></a>マッピングファイル

ホットスポットデータが単純な Excel 形式の場合は、Excel ファイルの列を対応する必須の JSON 要素にマップする XML ファイルを指定する必要があります。 次の一覧は、許可される列名を示しています。

* 自由
* 経度
* 放射 Al不明確
* 対地
* AltitudeUncertainty
* HotspotName
* SSID
* 範囲
* Address
* City
* StateOrProvince
* PostalCode
* CountryOrRegion
* Bssids
* ProviderHotspotId
* IsPublic
* IsFree
* PhoneNumbers

次の例は、マッピングファイルの一部を示しています。 各**MappingRule**要素は、Excel 列 (**Partnercolumnname**と**partnercolumnnumber**) を必要な JSON 要素 (**microsoft columnname**) に関連付けます。 終了ルールタグ (`</Rules>`) の後にある ContainsHeaderRow 要素は、ファイルにヘッダー行が含まれていることを示します。これは、データの読み取り時にスキップする必要があります。

```xml
<?xml version="1.0" encoding="utf-8"?>
<MappingRules xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
  <Rules>
    <MappingRule>
      <PartnerColumnName>english_hotspot_name</PartnerColumnName>
      <PartnerColumnNumber>3</PartnerColumnNumber>
      <MicrosoftColumnName>HotspotName</MicrosoftColumnName> 
    </MappingRule>
    <MappingRule>
      <PartnerColumnName>english_city_name</PartnerColumnName>
      <PartnerColumnNumber>2</PartnerColumnNumber>
      <MicrosoftColumnName>City</MicrosoftColumnName>
    </MappingRule>
    <MappingRule>
      <PartnerColumnName>ssid</PartnerColumnName>
      <PartnerColumnNumber>4</PartnerColumnNumber>
      <MicrosoftColumnName>SSID</MicrosoftColumnName>
    </MappingRule>
    <MappingRule>
      <PartnerColumnName>venue</PartnerColumnName>
      <PartnerColumnNumber>7</PartnerColumnNumber>
      <MicrosoftColumnName>HotspotType</MicrosoftColumnName>
    </MappingRule>
        .
        .
        .
        .    
  </Rules>
  <ContainsHeaderRow>true</ContainsHeaderRow>
</MappingRules>
```

