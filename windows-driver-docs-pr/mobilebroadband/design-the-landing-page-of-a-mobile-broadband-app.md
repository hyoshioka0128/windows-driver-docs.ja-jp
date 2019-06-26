---
title: モバイル ブロードバンド アプリのランディング ページを設計する
description: モバイル ブロードバンド アプリのランディング ページを設計する
ms.assetid: 3a42886f-8a32-4576-af31-65443bb718ca
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c54350bcb3064dc7a21b23143306483734b87f58
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393476"
---
# <a name="design-the-landing-page-of-a-mobile-broadband-app"></a>モバイル ブロードバンド アプリのランディング ページを設計する


ランディング ページに記載されている特定の場合を除いて、モバイル ブロード バンドのアプリを開始するときにユーザーに表示される最初のページは、[他の Windows コンポーネントと統合して、モバイル ブロード バンド アプリ](integrate-a-mobile-broadband-app-with-other-windows-components.md#launchpts)します。

![後払いランディング ページ](images/mb-fig1-landing-page-postpaid.png)

ランディング ページは、アプリのレイアウトの UWP アプリのガイドラインに従う必要があります。 わかりやすくするためと移動しやすさを促進するには、1 つのページにランディング ページのすべての内容を合わせることをお勧めします。 ランディング ページは、アプリの中央のハブです。 プライマリ ナビゲーション メソッドまたは管理ページではありませんが、アプリとその主要な機能を紹介します。

次のセクションでは、ランディング ページに含めることができるコンテンツの一部について説明します。

-   [使用状況-概要またはリンクを表示します。](#usageov)

-   [演算子メッセージ – 概要またはリンクを表示します。](#opmsg)

-   [その他のキーのページへのリンク](#keylinks)

-   [アプリのナビゲーション](#appnav)

-   [ブランド化演算子](#opbrand)

-   [簡単な概要](#sum)

-   [その他のリソース](#res)

## <a name="span-idusageovspanspan-idusageovspanusage--show-an-overview-or-link"></a><span id="usageov"></span><span id="USAGEOV"></span>使用状況-概要またはリンクを表示します。


### <a name="span-idpostpaidplansspanspan-idpostpaidplansspanspan-idpostpaidplansspanpostpaid-plans"></a><span id="Postpaid_plans"></span><span id="postpaid_plans"></span><span id="POSTPAID_PLANS"></span>後払い計画

重要なユーザーがデータの使用量に関する情報を表示できるため、使用状況は強調表示されますのランディング ページ可能な場合。 概要を使用することをお勧めはまたはを含む詳細については、アプリに別のページへのリンクを提供できます。 データ使用状況のセクションでは、追加の詳細の推奨事項を確認できます。 参照してください[モバイル ブロード バンド アプリでアカウントの残高と使用状況の情報を設計](design-account-balance-and-usage-info-in-a-mobile-broadband-app.md)の詳細。

### <a name="span-idprepaidplansspanspan-idprepaidplansspanspan-idprepaidplansspanprepaid-plans"></a><span id="Prepaid_plans"></span><span id="prepaid_plans"></span><span id="PREPAID_PLANS"></span>前払いプラン

データ使用状況の表示は、プリペイド プランの単純化されます。 ユーザーは、再充電、またはそのプランを補充するオプション提供する必要があります。 お支払い方法を提供するページへのリンクを行うことができます。 参照してください[モバイル ブロード バンド アプリでの課金のページをデザイン](design-billing-pages-in-a-mobile-broadband-app.md)の詳細。 前払いプランの一般的な概要ページを次に示します。

![前払いのランディング ページ](images/mb-fig2-landing-page-prepaid.png)

## <a name="span-idopmsgspanspan-idopmsgspanoperator-messages--show-an-overview-or-link"></a><span id="opmsg"></span><span id="OPMSG"></span>演算子メッセージ – 概要またはリンクを表示します。


ランディング ページは、テキスト メッセージの演算子の一覧を強調できます。 演算子のメッセージ数は、優先度の高いであるために、ユーザーはこれらを簡単にアクセスすることを選びます。 テキスト メッセージを組み込む必要がある機能の詳細については、次を参照してください。[モバイル ブロード バンド アプリでのメッセージを設計](design-messages-in-a-mobile-broadband-app.md)します。

## <a name="span-idkeylinksspanspan-idkeylinksspanlinks-to-other-key-pages"></a><span id="keylinks"></span><span id="KEYLINKS"></span>その他のキーのページへのリンク


ランディング ページは、その他のキーのページへのリンクを行うことができます。 たとえばのタイルを含めることができます**ヘルプし、サポート**のタイルと**サービス**。

## <a name="span-idappnavspanspan-idappnavspanapp-navigation"></a><span id="appnav"></span><span id="APPNAV"></span>アプリのナビゲーション


ランディング ページを記述する場合は、アプリ内のナビゲーションに注意してください。 アプリは、複数のページをさまざまな目的を持つ必要があります。 Windows 10 には、ナビゲーションに使用できる次のツールが用意されています。

-   **[戻る] ボタン**アプリでは、前のページに戻るには、[戻る] ボタンを使用できます。 戻るボタンのスタイル設定の詳細については、次を参照してください。[クイック スタート: コントロールのスタイル](https://docs.microsoft.com/previous-versions/windows/apps/hh465498(v=win.10))します。

-   **ヘッダー テキストを含むドロップダウン アフォー ダンス**ヘッダー テキストは、アプリの複数のページ間のナビゲーションのドロップ ダウン アフォー ダンスとして使用できます。 クリックすると、前の図で**アカウントの概要**次の図に示すように移動できるアプリ内のページのドロップダウン リストになります。

    ![アプリ間を移動します。](images/mb-fig3-nav-between-apps.png)

    アプリのナビゲーションを設計する方法の詳細については、次を参照してください。[クイック スタート。単一ページ ナビゲーションを使用して](https://docs.microsoft.com/previous-versions/windows/apps/hh452768(v=win.10))と[**要素の選択 | オブジェクトを選択**](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select)します。

## <a name="span-idopbrandspanspan-idopbrandspanoperator-branding"></a><span id="opbrand"></span><span id="OPBRAND"></span>ブランド化演算子


個々 のブランド化スタイルに合ったモバイル ブロード バンド アプリをカスタマイズできます。 さまざまなカスタマイズを使用すると、一意でわかりやすいにアプリを行うことができます。 アプリをブランド化する方法の詳細については、次を参照してください。[モバイル ブロード バンド アプリでのブランド化の設計](design-branding-in-a-mobile-broadband-app.md)します。

## <a name="span-idsumspanspan-idsumspanquick-summary"></a><span id="sum"></span><span id="SUM"></span>簡単な概要


### <a name="span-idappropriatedesignforthelandingpagespanspan-idappropriatedesignforthelandingpagespanspan-idappropriatedesignforthelandingpagespanappropriate-design-for-the-landing-page"></a><span id="Appropriate_design_for_the_landing_page"></span><span id="appropriate_design_for_the_landing_page"></span><span id="APPROPRIATE_DESIGN_FOR_THE_LANDING_PAGE"></span>ランディング ページの適切な設計

-   ユーザーがアプリで探しては主に概要情報を表示します。

-   読みやすさを向上させるためにシンプルなレイアウトを使用します。

-   UWP アプリのガイドラインに従ってください。

-   無効にする、**戻る**場合は、ユーザーがアプリへのアクセスを最初にボタンをクリックします。

### <a name="span-idinappropriatedesignforthelandingpagespanspan-idinappropriatedesignforthelandingpagespanspan-idinappropriatedesignforthelandingpagespaninappropriate-design-for-the-landing-page"></a><span id="Inappropriate_design_for_the_landing_page"></span><span id="inappropriate_design_for_the_landing_page"></span><span id="INAPPROPRIATE_DESIGN_FOR_THE_LANDING_PAGE"></span>不適切なデザインのランディング ページ

-   ランディング ページ上のスクロールを必要はありません。 1 つのページへのすべてのコンテンツを制限しようとしてください。

-   ランディング ページは、管理機能を必要はありません。

## <a name="span-idresspanspan-idresspanadditional-resources"></a><span id="res"></span><span id="RES"></span>その他のリソース


-   [UWP アプリ用のインデックスの UX のガイドライン](https://developer.microsoft.com/windows/apps/design)

-   [コントロールとコンテンツの追加](https://docs.microsoft.com/previous-versions/windows/apps/hh465393(v=win.10))

-   [すばらしい UWP アプリを作成します。](https://msdn.microsoft.com/library/windows/apps/hh464920)

-   [UI のレイアウト](https://docs.microsoft.com/previous-versions/windows/apps/hh465304(v=win.10))

-   [その他の Windows コンポーネントと統合して、モバイル ブロード バンド アプリ](integrate-a-mobile-broadband-app-with-other-windows-components.md#splash)

-   [その他の Windows コンポーネントと統合して、モバイル ブロード バンド アプリ](integrate-a-mobile-broadband-app-with-other-windows-components.md#tileandtoast)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイル ブロード バンドのアプリのユーザー エクスペリエンスの設計](designing-the-user-experience-of-a-mobile-broadband-app.md)

 

 






