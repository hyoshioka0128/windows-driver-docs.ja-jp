---
title: プランのモバイル サービスの構成
description: このトピックでは、Mobile プラン プログラムの構成手順について説明します。
ms.assetid: 95122BBB-0466-4130-9209-7EC6545DFD4D
keywords:
- Windows Mobile のプランの構成、モバイルのプランの構成モバイル演算子
ms.date: 02/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: 771d2674cff145f064aa960b7d18417c08aacfdf
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903660"
---
# <a name="mobile-plans-service-configuration"></a>プランのモバイル サービスの構成

このトピックでは、Mobile の計画をサポートする Windows 接続されているデバイスの基盤を構築する方法を説明します。 Mobile プランにより、サービスの構成情報を提供するエクスペリエンスが適切にレンダリング Windows デバイスでどのように、最適なコンシューマーのエクスペリエンスもさせる、eSIM プロファイルを構成する方法も詳しく説明します。

## <a name="esim-profile-configuration-requirements"></a>esim 状プロファイル構成の要件

次の要件を満たす eSIM プロファイルを準備する必要があります。

- ESIM プロファイルでは、PIN ロックすることはできません。
- Esim 状プロファイルする必要があります、SM から削除できません-DP + サーバー プロファイルのダウンロードが正常に完了したことの確認を受信するまでです。 アクティブ化コードは、ダウンロードを前の試行が失敗した場合、同じプロファイルをダウンロードを再試行する再利用できます。
- 「削除しないでください」または「は非アクティブ化できません」のポリシーの設定、eSIM プロファイルは必要ありません。
- アクティブ化コードがなど任意のプレフィックスを含めるいない必要があります"以下:"です。
- アクティブ化コードは、MO を直接フロー後すぐに使用できます。
- アクティブ化コードでは、「確認コード」は必要ありません必要があります。

### <a name="esim-profile-testing"></a>esim 状プロファイルのテスト

通信事業者がさまざまな Windows デバイスで、esim 状のプロファイルをインストールできることを確認するための検証を実行することが期待されます。 これは、ソースの一部の eSIM 対応デバイスと Windows の設定アプリを使用して、ダウンロード、インストール、およびプロファイルをアクティブ化することをお勧めします。

## <a name="service-configuration"></a>サービス構成

プランのモバイル サービスでは、携帯電話会社をサポートするために一部の構成情報を取り込む必要があります。 構成プロセスを開始する電子メールをお送りください[Mobile 計画の実装サポート](mailto:mpimplementation@microsoft.com)します。

### <a name="minimum-configuration-information"></a>最小の構成情報

1. ブランド名は、自社製品を使用したいです。
2. ブランド ロゴです。 必要な解像度は、300 x 300 ピクセルです。 イメージは、フルブリード透過性なしでもあります。
3. ソリューションがサポートされている国の一覧。 使用してください[ISO 3166 コード](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2)リスト (コンマ区切り) を作成します。
4. MO 直接ポータル URI (ローカリゼーションがサポートされていません)。 これは、アカウントは、 *https*アドレス。 ポート番号はサポートされていません。
5. 通知 URI。 これは、どこからホスト アドレス Javascript コールバック ([コールバック通知](mobile-plans-callback-notifications.md)) を実行します。 これは、アカウントは、 *https*アドレス。 ポート番号はサポートされていません。
6. ICCID 範囲または範囲に関連付ける*Mobile プラン*します。

次の図の例を示します、*標準ゲートウェイ ページ*プランのモバイル アプリでします。 "A"注釈に対応するブランド ロゴを送信して、"B"の注釈は、ブランド名に対応します。

<img src="images/mobile_plans_configuration_mo_page.png" alt="Mobile Plans mobile operator page - asset usage example" title="プランのモバイル携帯電話会社ページ - 資産の使用例" width="600" />

### <a name="enhanced-gateway-page"></a>強化されたゲートウェイ ページ

これは、プランのモバイル アプリのバージョンでサポートされているオプション機能**5.1902.331.0**以降。

標準のランディング ページは、そのオファリングを強調表示する携帯電話会社のルック アンド フィールをブランド化で拡張できます。

#### <a name="enhanced-gateway-content"></a>コンテンツの強化されたゲートウェイ

強化されたゲートウェイのコンテンツは、次の要素を含む JSON ファイルを使用して定義されます。

```JSON
{ // Root object
  "promotionTemplates": [
    { // PromotionTemplate
      "id": 0,
      "backgroundColor": "0x000000FF", // Black
      "bodyFontColor": "0xFFFFFFFF", // White
      "buttonColor": "0x414243FF", // Grey
      "buttonFontColor": "0xFFFFFFFF", // White
      "bodyText": "We’ll help you find a plan so you can get connected when W-Fi isn’t available",
      "buttonText": "Get started",
      "hyperlinkColor": "0xBB8CF9FF", //Purple
      "images": [
        { // Image
          "height": 480,
          "uri": "https://content.windows.com/MO1/landing740x480.png",
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
|   | ButtonText | [続行] ボタンのローカライズされたテキスト。 | 作業開始 |
|   | hyperlinkColor | ゲートウェイのページ内のハイパーリンクは、この色を使用しようとしています。 このフィールドは、16 進数の文字列の形式で`0xRRGGBBAA`します。 未定義の場合、ハイパーリンクの既定の色が使用されます。 | 0xBB8CF9FF |
|   | images | テンプレートを使用するイメージ。 さまざまなサイズがサポートされています。 複数のサイズが含まれる場合は、プランのモバイル アプリは、画面の解像度の最適なサイズを使用します。 イメージの最大サイズは、1200 x 600 ピクセル、ファイル形式*png*します。| ![モバイル プラン サーフェスのランディング ページの例、780 x 480](images/mobile_plans_surface_landing_780x480.png) |

#### <a name="example-enhanced-gateway-landing-page"></a>強化されたゲートウェイのランディング ページの例

![プランのモバイル アプリで強化されたゲートウェイ ランディング ページの例](images/mobile_plans_sample_landing_page.png)