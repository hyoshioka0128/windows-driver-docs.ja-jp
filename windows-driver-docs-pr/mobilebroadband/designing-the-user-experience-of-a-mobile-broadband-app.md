---
title: モバイル ブロードバンド アプリのユーザー エクスペリエンスの設計
description: モバイル ブロードバンド アプリのユーザー エクスペリエンスの設計
ms.assetid: c84e2814-69ba-4cd0-ba11-1b035ccdfbde
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c66929c7f9dda7dd000bbf2f5347a7004ba85ab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574907"
---
# <a name="designing-the-user-experience-of-a-mobile-broadband-app"></a>モバイル ブロードバンド アプリのユーザー エクスペリエンスの設計


このトピックでは、Windows 10 用 UWP モバイル ブロード バンド アプリを設計する方法についての情報を提供します。 ユーザーがモバイル ブロード バンド アカウントとサービスを管理するアプリをデザインするユーザー エクスペリエンス デザインのガイドラインを提供します。 モバイル ブロード バンド技術、Windows モバイル ブロード バンド ネットワークでは、Microsoft Store アプリのプラットフォームと使い慣れた想定します。

次のセクションでは、このトピックで使用できるとおりです。

-   [主なシナリオ](#keyui)

-   [組織のアプリ](#apporg)

-   [その他のリソース](#resources)

## <a name="span-idkeyuispanspan-idkeyuispankey-scenarios"></a><span id="keyui"></span><span id="KEYUI"></span>主なシナリオ


モバイル ブロード バンド アプリでは、次の主要なシナリオを含める必要があります。

-   **プランを購入**

    -   データ サービスに新しいサブスクリプションを購入します。

    -   プランにアカウントの残高を補充します。

-   **アカウント管理**アカウント データと現在のプラン情報が表示されます。

-   **データ使用状況の表示**

    -   現在のデータ使用量と課金サイクルの情報を表示します。

    -   最新のデータの使用状況では、Windows を更新します。

-   **通知**データ使用量およびその他の重要なアカウントとサービスのメッセージを表示します。

-   **ヘルプし、サポート**表示のトラブルシューティングとお客様の連絡先情報をサポートします。

## <a name="span-idapporgspanspan-idapporgspanapp-organization"></a><span id="apporg"></span><span id="APPORG"></span>組織のアプリ


アプリでさまざまなページを次に示します整理できます。

![概要](images/mb-fig1-overview-uwp-device-app.png)

-   アプリでは、お客様のアカウントとデータの使用量の概要を提供するアカウントの概要ランディング ページがあります。 その他のアプリ ページへのリンクも含まれています。

-   ランディング ページで、エンドユーザーは、課金、プラン、サービス、またはヘルプを表示およびサポートの詳細の [ハブ] ページにアクセスできます。

-   一部のハブ ページは、タスクの各ページと購入のチェック アウト フローなどのフローにつながります。

**ヒント:**   前払いプランの場合、アカウントの概要をリンク直接でした、**支払を行う**補充シナリオのページ。

 

これらのページを設計する方法の詳細については、次のトピックを参照してください。

-   [モバイル ブロード バンドのアプリのランディング ページのデザイン](design-the-landing-page-of-a-mobile-broadband-app.md)

-   [モバイル ブロード バンド アプリでのブランド化を設計します。](design-branding-in-a-mobile-broadband-app.md)

-   [モバイル ブロード バンド アプリでアカウントの残高と使用状況情報を設計します。](design-account-balance-and-usage-info-in-a-mobile-broadband-app.md)

-   [モバイル ブロード バンド アプリでのメッセージを設計します。](design-messages-in-a-mobile-broadband-app.md)

-   [モバイル ブロード バンド アプリ内課金のページをデザインします。](design-billing-pages-in-a-mobile-broadband-app.md)

-   [モバイル ブロード バンド アプリ内購入フローをデザイン](design-purchase-flows-in-a-mobile-broadband-app.md)

-   [ヘルプを設計し、モバイル ブロード バンド アプリでページをサポートします。](design-help-and-support-pages-in-a-mobile-broadband-app.md)

-   [モバイル ブロード バンド アプリでのサービスと商品ページをデザインします。](design-services-and-goods-pages-in-a-mobile-broadband-app.md)

-   [その他の Windows コンポーネントと統合して、モバイル ブロード バンド アプリ](integrate-a-mobile-broadband-app-with-other-windows-components.md)

## <a name="span-idresourcesspanspan-idresourcesspanadditional-resources"></a><span id="resources"></span><span id="RESOURCES"></span>その他のリソース


-   [UWP アプリ用のインデックスの UX のガイドライン](https://msdn.microsoft.com/library/windows/apps/hh465424)

-   [モバイル ブロード バンドの概要](overview-of-mobile-broadband.md)

 

 





