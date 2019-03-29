---
title: Wi-Fi ホット スポット データ送信形式
description: Wi-Fi ホット スポット データ送信形式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: abe78dbc18f82563b1835c12a36ba33accac982c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577738"
---
# <a name="wi-fi-hotspot-data-submission-format"></a>Wi-Fi ホット スポット データ送信形式

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]

探索サービスに送信されたデータをホット スポットでは、JavaScript Object Notation (JSON) である必要があり、次の要素を使用する必要があります。

| 要素 | 型 | 説明 |
| --- | --- | --- |
| バッチ Id | GUID | プロバイダーは、複数の送信に複数のホット スポットを含む 1 つのサブミッションを分割できます。 送信するたびには、同じバッチ Id の GUID が割り当てられます。 |
| ProviderId | GUID | プロバイダー ID は Microsoft がプロバイダーに割り当てられます。 |
| TransactionId | int | バッチ内の各要求に対して、増分する番号。 Degbugging 目的で使用します。 |
| ホット スポット |  | アップロードするホット スポットの一覧。 |
| 追加 |  | 次のサブ要素を含む完全なアドレス プロパティ:**アドレス**、**市区町村**、 **StateOrProvince**、 **PostalCode**、および**CountryOrRegion**します。 |
| Bssid| リスト\<文字列 > | ホット スポットを構成する Bssid の一覧。 各 BSSID から成る 8 で、2 つの桁の 16 進数の値は、次の形式で。*00:aa:bb:cc:dd:ee*します。 |
| 無料 | ブール値 | ホット スポットが無料かどうかを示すブール値。 |
| pub | ブール値 | ホット スポットがパブリックかどうかを示すブール値。 |
| Loc |  | 次のサブ要素を含む完全な場所のプロパティ:**緯度**、**経度**、 **RadialUncertainty**、**高度**、および**AltitudeUncertainty**します。 |
| NAME | string | ホット スポットのフレンドリ名。 |
| phid | string | プロバイダーのホット スポットの id。 デバッグ目的で使用します。 |
| 実行 | uint | ホット スポットの範囲。 |
| ssid | string | ホット スポットの SSID です。 |
| [電話] | string | ホット スポットに関連付けられているすべての電話番号の一覧。 |

**注:**

* ヘッダーとそのサブ要素 (**ProviderId**、 **BatchId**、および**TransactionId**) が必要です。
* ホット スポットの一覧は空にできません。
* Location 要素を指定した場合**緯度**と**経度**が必要です。
* Location 要素が指定されていない場合、少なくとも 1 つ BSSID を指定してください。 それ以外の場合、警告が返され、探索サービスでは、ホット スポットは処理されません。

次の例では、完全なデータを 1 つのホット スポットを示しています。

```JSON
{
      "Header": {
            "BatchId": "BA85A383-5943-4D84-8ACB-B113BDEA3783", 
            "ProviderId": "AE012377-B0B4-4096-B5D5-D7EFBDC170EC", 
            "TransactionId": 1
      }, 
      "Hotspots":[{
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

探索サービスでは、デバッグ目的で、探索サービスのホット スポットのデータの検証時に生成された警告の一覧に使用するアクティビティ ID を含む JSON 形式でも、単純な応答を返します。 探索サービスによって返されるすべての文字列は、utf-8 でエンコードされます。

次の表では、探索サービスの応答の JSON 要素を示します。

| 要素 | 型 | 説明 |
| --- | --- | --- |
| ActivityId | string | 必須。 これは問題をデバッグする際に、プロバイダーを使用している文字列です。 |
| 警告 | リスト\<文字列 > | 警告の人間が判読できる一覧。 |

次の例は、ホット スポットのデータの送信に典型的な応答を示しています。

```JSON
{
     "ActivityId": "d2856c06-e4a1-4434-90e8-ced0c9ee6e10",
     "Warnings": ["Invalid Latitude: 247.67 – Hotspot Id: abcdefg"]
}
```

