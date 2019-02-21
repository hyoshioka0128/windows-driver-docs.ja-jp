---
title: キャンペーンのコンテンツをモバイル プラン
description: キャンペーンのコンテンツをモバイル プラン
ms.assetid: FB789462-732C-436A-B69C-43940F7F8A77
keywords:
- Windows Mobile はキャンペーン プラン コンテンツの携帯電話会社
ms.date: 10/23/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7dee8cee963f766c18e915f51ea85d0065030deb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556955"
---
# <a name="mobile-plans-promotional-content"></a>キャンペーンのコンテンツをモバイル プラン

[!include[Mobile Plans Beta Prerelease](../mobile-plans-beta-prerelease.md)]

## <a name="overview"></a>概要

このトピックでは、作成し、プランのモバイル アプリでの販売促進キャンペーンのコンテンツを送信するための手順を説明します。

## <a name="promotional-notifications"></a>プロモーションの通知

Windows には、テキスト、イメージのボタン入力対話型トースト通知のサポートが含まれています。 プランのモバイル アプリにより、トースト通知をアプリでトリガーできるキャンペーンのコンテンツを表示します。

## <a name="promotional-gateways"></a>キャンペーンのゲートウェイ

プランのモバイル アプリには、すべての通信事業者のランディング ページが含まれています。 キャンペーンのコンテンツを貴社のブランドやキャンペーンのメッセージを強調表示するには、ランディング ページをカスタマイズできます。

### <a name="promotional-gateway-content"></a>ゲートウェイのキャンペーンのコンテンツ

ゲートウェイのキャンペーンのコンテンツは、次の要素を含む JSON ファイルを使用して定義されます。

```JSON
{ // Root object
  "promotionTemplates": [
    { // PromotionTemplate
      "id": 123,
      "backgroundColor": "0x000000FF", // Black
      "bodyFontColor": "0xFFFFFFFF", // White
      "buttonColor": "0x414243FF", // Grey
      "buttonFontColor": "0xFFFFFFFF", // White
      "bodyText": "We’ll help you find a plan so you can get connected when W-Fi isn’t available",
      "buttonText": "Get started",
      "images": [
        { // Image
          "height": 480,
          "uri": "https://storagetos.datamart.windows.com/MO1/v1/en-US/landing740x480.png",
          "width": 740,
        }
      ]
    }
  ]
}
```

次の表では、前の例では、各 JSON オブジェクトについて説明します。

| JSON オブジェクト | フィールド名 | 説明 | 例 |
| --- | --- | --- | --- |
| ルート オブジェクト | promotionTemplates | [ゲートウェイ] ページに表示される昇格テンプレートの一覧。 1 つだけ昇格テンプレートについては、各携帯電話会社のサポートします。 | なし |
| PromotionTemplate | id | テンプレートの一意の文字列識別子です。 | 123 |
|   | BackgroundColor | ゲートウェイのページの背景色。 このフィールドは、16 進数の文字列の形式で`0xRRGGBBAA`します。 未定義の場合、空白は、既定値として使用されます。 | 0x000000FF |
|   | bodyFontColor | 本文テキストのフォントの色。 このフィールドは、16 進数の文字列の形式で`0xRRGGBBAA`します。 黒の未定義の場合は、既定値として使用されます。 | 0 xffffffff |
|   | buttonColor | 携帯電話会社のポータルを起動する [続行] ボタンの色。 このフィールドは、16 進数の文字列の形式で`0xRRGGBBAA`します。 未定義の場合、ユーザーが選択したシステムの強調表示色は、既定値として使用されます。 | 0x414243FF |
|   | buttonFontColor | [続行] ボタンのテキストのフォントの色。 このフィールドは、16 進数の文字列の形式で`0xRRGGBBAA`します。 未定義の場合、空白は、既定値として使用されます。 | 0 xffffffff | 
|   | bodyText | クライアントの言語のローカライズされた本文。 | Wi-fi を使用できないときに接続を取得できるように、プランを見つけることをお手伝いします。 |
|   | ButtonText | [続行] ボタンのローカライズされたテキスト。 | はじめに |
|   | images | テンプレートを使用するイメージ。 さまざまなサイズがサポートされています。 複数のサイズが含まれる場合は、プランのモバイル アプリは、画面の解像度の最適なサイズを使用します。 | ![モバイル プラン サーフェスのランディング ページの例、780 x 480](images/mobile_plans_surface_landing_780x480.png) |

### <a name="example-promotional-gateway-landing-page"></a>キャンペーンのゲートウェイのランディング ページの例

![プランのモバイル アプリでキャンペーン ゲートウェイ ランディング ページの例](images/mobile_plans_sample_landing_page.png)