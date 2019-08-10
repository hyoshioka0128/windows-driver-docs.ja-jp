---
title: モバイルプランゲートウェイページ
description: モバイルプランゲートウェイページ
ms.assetid: de4c7ae1-c0fc-4e6c-996c-e10f16b62d7e
keywords:
- Windows Mobile プランのモバイルオペレーター
ms.author: windowsdriverdev
ms.date: 07/31/2019
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 910c34c4299c563da899f1b84e7e6904e41c4b8f
ms.sourcegitcommit: f89a978ee23b9d2f925b13ea56b2c6cd48b4603a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/10/2019
ms.locfileid: "68948105"
---
# <a name="mobile-plans-gateway-page"></a>モバイルプランゲートウェイページ

## <a name="overview"></a>概要

モバイルプランアプリは、カタログで有効になっているすべてのモバイルオペレーターのゲートウェイページをホストします。 [ゲートウェイ] ページは、[ようこそ] 手順の一部としてエンドユーザーに表示されます。 これには、携帯電話会社の基本的なブランド要素だけでなく、いくつかのリンクとプライバシーに関する免責事項が含まれています。 [ゲートウェイ] ページには、モバイルオペレーター web ポータルを起動するためのボタンも用意されています。

## <a name="enhanced-gateway-page"></a>[拡張ゲートウェイ] ページ

これは、モバイルプランアプリバージョン**5.1902.331.0**以上でサポートされているオプションの機能です。

[ゲートウェイ] ページは、モバイルオペレーターがページのコンテンツとスタイルを指定することによってカスタマイズできます。 これにより、オファリングと固有のブランド価値を強調することができます。

### <a name="enhanced-gateway-page-content"></a>強化されたゲートウェイページコンテンツ

拡張ゲートウェイページは、定義済みの要素を持つテンプレートを使用して指定します。 強調表示された要素は、携帯電話会社が定義できます。

![強化されたゲートウェイページテンプレート](images/enhanced_gateway_page_template.png)

### <a name="enhanced-gateway-page-templates"></a>強化されたゲートウェイページテンプレート

[拡張ゲートウェイ] ページに表示されるカスタムコンテンツは、次の要素を含む JSON ファイルを使用して定義されます。

```JSON
{ // Root object
  "promotionTemplates": [
    { // PromotionTemplate
      "id": 0,
      "backgroundColor": "0x000000FF", // Black
      "bodyFontColor": "0xFFFFFFFF", // White
      "bodyText": "Stay connected from virtually anywhere.",
      "buttonColor": "0x00B0F0FF", // Light Blue
      "buttonFontColor": "0xFFFFFFFF", // White
      "buttonText": "Get started",
      "hyperlinkFontColor": "0x00B0F0FF", //Light Blue
      "images": [
        { // Image
          "uri": "https://picsum.photos/id/1/740/480",
          "width": 740,
          "height": 480,
        }
      ]
    }
  ]
}
```

次の表では、前の例の各 JSON 要素について説明します。

| JSON 要素 | [フィールド名] | 説明 | 例 |
| --- | --- | --- | --- |
| ルートオブジェクト | promotionTemplates | [拡張ゲートウェイ] ページで使用するテンプレートの一覧。 モバイルオペレーターごとに1つまたは複数のテンプレートを定義できます。 | なし |
| PromotionTemplate | id | 各テンプレートの一意の文字列識別子。 1つのテンプレートのみが定義されている場合の既定値は、"0" にする必要があります。 | 123 |
|   | 背景 | ゲートウェイページの背景の色。 このフィールドは、の`0xRRGGBBAA`形式の16進文字列です。 Undefined の場合は、既定値として白色が使用されます。 | 0x000000FF |
|   | bodyFontColor | 本文のテキストの色。 これは、の`0xRRGGBBAA`形式の16進文字列です。 Undefined の場合は、既定値として黒が使用されます。 | ~ |
|   | bodyText | クライアントの言語のローカライズされた本文。 免責事項のテキストは変更できないことに注意してください。| 事実上どこからでも接続できます。 |
|   | buttonColor | 携帯電話会社の web ポータルを起動する [続行] ボタンの色。 このフィールドは、の`0xRRGGBBAA`形式の16進文字列です。 定義されていない場合は、ユーザーが選択したシステム強調表示色が既定値として使用されます。 | 0x00B0F0FF |
|   | buttonFontColor | [続行] ボタンのテキストの色。 このフィールドは、の`0xRRGGBBAA`形式の16進文字列です。 Undefined の場合は、既定値として白色が使用されます。 | ~ |
|   | buttonText | [続行] ボタンのローカライズされたテキスト。 | 作業開始 |
|   | ハイパーリンクフォントの色 | ハイパーリンクの色。 このフィールドは、の`0xRRGGBBAA`形式の16進文字列です。 定義されていない場合は、ユーザーが選択したシステム強調表示色が既定値として使用されます。 | 0x00B0F0FF |
|   | images | テンプレートに使用するイメージ。 さまざまなサイズがサポートされています。 複数のサイズが含まれている場合、モバイルプランアプリでは、画面の解像度に最適なサイズが使用されます。 イメージの最大サイズは、1200 x 600 ピクセル、ファイル形式*png*です。| https://picsum.photos/id/1/740/480 |

### <a name="sample-enhanced-gateway-page"></a>拡張ゲートウェイのサンプルページ

![携帯電話会社のゲートウェイページ](images/mobile_operator_gateway_page.png)

### <a name="using-multiple-gateway-page-templates"></a>複数のゲートウェイページテンプレートの使用

モバイルオペレーターには、複数のゲートウェイページテンプレートを定義するオプションがあります。 これが行われると、Mobile plan サービスは実行時に Mobile Operator API を呼び出して、ユーザーに表示されるテンプレートの ID を要求します。

要求にはプロファイルとデバイスの識別子が含まれているため、携帯電話事業者は、さまざまなユーザーセグメントに対して複数のテンプレートを定義できます。 これは、A/B テストに使用したり、新しいユーザーにサインアップを招待する1つのテンプレートを表示したり、追加の残高を購入したユーザーを返すための別のテンプレートを表示したりするために使用できます。 ゲートウェイページテンプレートをモバイルプランの通知と組み合わせて、高度なターゲットのキャンペーンを作成することもできます。

> [!NOTE]
> デバイスに携帯電話会社用のアクティブなプロファイルがない場合、要求は行われず、テンプレート ID "0" が既定で使用されます。

Get オファー要求では、ユーザーに表示されるテンプレート ID が返されます。

![モバイルプラン Get の呼び出しフロー](images/mobile_plans_get_offers_callflow.png)

### <a name="getoffers-api-specification"></a>GetOffers 仕様

この`GetOffers` API は、モバイルオペレーターゲートウェイページを表示する前に呼び出されます。 Mobile plan サービスは、この要求のプロキシです。

```HTTP
GET https://{offerUri}sims/{simmri}/offers?limit=1&imei=1234
```

- *{offerUri}* は、携帯電話会社のサービス構成の一部としての offerUri 値オンボードです。

エンドポイントには、次の2つのクエリパラメーターがあります。
- *制限*は必須であり、返されるオファーの数を指定します。
- *imei*。クライアントの imei を指定します (省略可能)。

応答は、オファーの一覧を含む、*オファー*という名前の1つのプロパティを持つ JSON オブジェクトです。 この一覧に表示されるプランの数は、要求の*上限に達し*ています。 この一覧の各プランは、1つのプロパティ*Gatewayid*を持つオブジェクトで、モバイルオペレーターのサービス構成で既存のゲートウェイを識別する必要があります。

このエンドポイントを使用した相互作用の例を次に示します。

```HTTP
GET https://moendpoint.com/v1/sims/iccid:8988247000100003319/offers?limit=1&imei=1234
X-MS-DM-TransactionId: "MSFT-12345678-1234-1234-1234-123456789abc"

HTTP/1.1 200 OK
Content-type: application/json
X-MS-DM-TransactionId: "MSFT-12345678-1234-1234-1234-123456789abc"
{
  "offers" : [
   {
      "gatewayId": "0"
    }
  ]
}
```

## <a name="standard-gateway-page"></a>Standard ゲートウェイページ

拡張ゲートウェイページが定義されていない場合、標準ゲートウェイページは最後に表示されます。 モバイルオペレーターの拡張ゲートウェイページのコンテンツを読み込むときに問題が発生した場合は、standard ゲートウェイページをダウングレードされた experiend として表示することもできます。

標準ゲートウェイページでは、モバイルオペレーターがカスタマイズできない基本テンプレートが使用されています。

![Standard ゲートウェイページ](images/standard_gateway_page.png)
