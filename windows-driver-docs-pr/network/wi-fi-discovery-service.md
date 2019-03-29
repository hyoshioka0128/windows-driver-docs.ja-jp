---
title: Wi-Fi 探索サービス
description: Wi-Fi 探索サービス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 008b4f87b21fc8da11193247b952dd0598e924dd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573854"
---
# <a name="wi-fi-discovery-service"></a>Wi-Fi 探索サービス

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]

Wi-fi の探索サービスでは、Wi-fi ホット スポットへの移動体通信トラフィックをオフロードして、データのコストを削減することができます。 探索サービスは、既知の Wi-fi ホット スポットのディレクトリを生成するには、モバイル演算子、およびその他のソースなど、プロバイダーからの Wi-fi ホット スポットのデータを集計します。 このディレクトリを使用すると、ユーザーは、現在の位置の近くのホット スポットに関する情報を取得できます。

モバイル演算子は、HTTP POST 要求を送信することによって、または Microsoft によって提供されるコマンド ライン ツールを使用して、サービスにホット スポットのデータを送信できます。

## <a name="instructions"></a>手順

Wi-fi ホット スポットのデータで説明されている形式である必要があります[Wi-fi ホット スポットのデータの送信形式](wi-fi-hotspot-data-submission-format.md)します。

探索サービスでは、すべてのプロバイダーのホット スポットが 1 つのバッチで送信されたことが必要です。 各バッチは、少量のデータを複数の送信要求を含めることができます。 たとえば、1,000 のホット スポットを含むバッチは 10 件の送信要求、100 のホット スポットのデータを含む各を送信することによって探索サービスにアップロードできます。 各送信要求には、同じバッチ番号が割り当てられます。 最終的な送信要求を含める必要があります、`X-FinalBatchRequest`ヘッダー、バッチ内のホット スポットの合計数を設定します。 このヘッダーで送信要求を受け取るまで、バッチは処理されません。 ヘッダーが、バッチ内のホット スポットの数が一致しない場合、送信は処理されません。

### <a name="submitting-hotspot-data-by-using-http-post"></a>HTTP POST を使用してホット スポットのデータを送信します。

次の例では、標準的な送信要求を示します。 有無、`X-FinalBatchRequest`ヘッダーと「1」の数値の値は、このバッチで 1 つだけのホット スポットがあり、これが、最終的な送信要求ことを示します。 そのため、これは、唯一の送信要求です。 バッチに複数のホット スポットが含まれている場合は、すべての送信要求が最後の 1 つの行を削除してください。

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

移行先サーバーで、メッセージが受信したときに**SubmitHotspots**要求を検証し、ホット スポットのデータを探索サービスに送信する前に、送信者を認証します。

### <a name="submitting-hotspot-data-by-using-the-command-line-tool"></a>コマンド ライン ツールを使用してホット スポットのデータを送信します。

WifiProviderExe.exe は、データ ファイル、必須の形式に変換および指定した探索サービスのサーバーにアップロードのホット スポットを入力として受け取り、マイクロソフトによって提供された、コマンド ライン ツールです。

WiFiProvider.exe を実行するには、次の構文を使用します。

```cmd
WifiProviderExe –DataFile filename -ProviderId GUID -ServiceEndpoint URL -CustomTransformer filename.dll [-MappingFile filename.xml] [-CertFile filename.pfx] [-CertPassword password] [-CertSubject name]
```

例:

```cmd
WifiProviderExe -DataFile "file.txt" -ProviderId 00000000-0000-0000-0000-000000000000 -ServiceEndpoint "https://submitwifiservice.windowsphone.com/v1/SubmitHotspots" -CustomTransformer "transformer.dll"
```

次の表には、WiFiProvider.exe の可能なパラメーターの一覧が含まれています。

| パラメーター | 説明 |
| --- | --- |
| データ ファイル | 必須。 ホット スポットのデータを格納しているファイルの名前。 |
| ProviderId | 必須。 Microsoft によって割り当てられたプロバイダーの ID (GUID)。 |
| サービス エンドポイント | 必須。 ホット スポットのデータのアップロード先となる検出サービス サーバーの URL。 たとえば、 https://wifi.windowsphone.com/v1/submithotspots と記述します。 |
| CustomerTransformer | 必須。 トランスフォーマーを格納するアセンブリの名前。 | 
| MappingFile | 任意。 プロバイダーのホット スポットのデータを探索サービスで必要な形式にマップするマッピング ファイル。 |
| CertFile | 任意。 認証に証明書を含む実際の pfx ファイルへのポインター。 証明書のパスワードのパラメーター (**CertPassword**) この認証方法を使用する場合に指定する必要があります。 |
| CertPassword | 任意。 指定された証明書にパスワード**CertFile**します。 |
| CertSubject | 任意。 証明書のサブジェクト名。 現在のあるユーザーの My 証明書ストア。 この認証メカニズムを使用する場合**CertFile**と**CertPassword**は必要ありません。 ただし、証明書の秘密キーを作成し、アクセス制御リストでは、キーの証明書を使用するアカウントへのアクセス権を付与することが必要です。 |

#### <a name="transformers"></a>トランスフォーマー

ホット スポットのデータは、任意の形式にできます。 ただし、ホット スポットのデータを探索サービスで必要な形式に変換するコマンド ライン ツールにアクセスできる「データ トランスフォーマー」を指定するために必要です。

次の表では、コマンド ライン ツールで提供されるサンプルの変換機能を示します。 これらは、特定のデータ形式を必要な形式に変換するができます。

| トランスフォーマー | データ形式 | 説明 |
| --- | --- | --- |
| Microsoft.Wps.WifiService.ProviderSdk.JsonHotspotDataTransformer.dll | JSON | データがで指定された JSON 形式に準拠する必要があります[Wi-fi ホット スポットのデータの送信形式](wi-fi-hotspot-data-submission-format.md)します。 |
| Microsoft.Wps.WifiService.ProviderSdk.JsonHotspotDataTransformer.dll | 単純な Excel | マッピング ファイルを指定する必要があります。 |

#### <a name="mapping-files"></a>マッピング ファイル

ホット スポット データは、単純な Excel 形式では、対応する必須の JSON 要素を Excel ファイル内の列をマップする XML ファイルを指定してください。 次に、許可されている列の名前を示します。

* 緯度
* 経度
* RadialUncertainty
* 高度
* AltitudeUncertainty
* HotspotName
* SSID
* 範囲
* Address
* 市区町村
* StateOrProvince
* PostalCode
* CountryOrRegion
* Bssid
* ProviderHotspotId
* IsPublic
* IsFree
* PhoneNumbers

次の例では、マッピング ファイルの一部を示します。 各**MappingRule**要素を Excel 列に関連付けます (**PartnerColumnName**と**PartnerColumnNumber**) 必須の JSON 要素を持つ (**MicrosoftColumnName**)。 **ContainsHeaderRow**終了後にある、要素タグのルール (`</Rules>`)、ファイルにデータを読み取るときにスキップするヘッダー行が含まれていることを示します。

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

