---
title: モバイル ブロード バンド アプリ内購入フローをデザイン
description: モバイル ブロード バンド アプリ内購入フローをデザイン
ms.assetid: 1243b255-aac6-4d75-826a-e42482f5ac1b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c0d5793433efe779b06f72c59ac7b6079704f3f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528117"
---
# <a name="design-purchase-flows-in-a-mobile-broadband-app"></a>モバイル ブロード バンド アプリ内購入フローをデザイン


モバイル ブロード バンド アプリでは、使用してプランを購入するユーザーの購入のフローを含めることができます。 初めての購入を web 経由で購入フローをサポートします。 購入のフローの標準的な推奨事項を次に示します。

**注**  アプリでこれらのフローをホストする iframe を使用しないでください。

 

1.  ユーザー プランの詳細を表示して、完全な購入フローに転送する前に、プランを選択できるようにします。

    ![プランの詳細](images/mb-fig1-purchaseflow-plandetails.png)

2.  必要に応じてこれらが必要になるデータを評価するユーザーのデータのブレーク ダウンを行うことができます。 これにより、最適なプランを購入するユーザーの選択は役立ちます。

    ![プランの詳細を確認してください。](images/mb-fig2-reviewplandetails.png)

3.  購入フローにフォームが含まれている場合は、次のガイドラインに従います。

    -   垂直方向のフォーム ページのスクロールを許可します。

    -   すべてのフォーム フィールドは左揃えを確認します。

    -   アプリは、複数のフォーム ファクターと互換性のあるである必要があります、ために、タッチ操作に適したフォーム フィールドの間隔を指定することをお勧めします。

    -   わかりやすくするために昇格する空白のままにします。

    -   フォームのサポートのベスト プラクティスに従ってください。 これは、が含まれているがされておらず、アドレス、番号、およびクレジット カードのフィールドの適切なサポートを提供します。

    -   フォーム フィールドのフィールドの適切なタッチ キーボードが表示されるように、入力のスコープが定義されていることを確認、数値、テキスト、およびなど。

    -   フォームがすべてのコントロールのあるし、フィールドが正しく調整してください。

    -   数回のクリックとフィールドの数を最小限に抑えます。

4.  ユーザーの情報を入力すると、購入を完了する前に、注文を確認することを許可します。 注文、アクティブ化が簡単な場合は、アクティブ化を続行し、アプリのランディング ページにリダイレクトします。 アクティブ化の時間がかかるが予想される場合は、アクティブ化の進行状況のプレース ホルダー ページが含まれますをアクティブ化が行われていることを表示する進行状況コントロールを使用することができます。 プログレス コントロールの概要の詳細については、次を参照してください。[クイック スタート: 進行状況コントロールを追加する](https://msdn.microsoft.com/library/windows/apps/hh465487)します。

## <a name="span-idquicksummaryspanspan-idquicksummaryspanspan-idquicksummaryspanquick-summary"></a><span id="Quick_summary"></span><span id="quick_summary"></span><span id="QUICK_SUMMARY"></span>簡単な概要


購入のページの適切なデザイン:

-   左揃え、空白、適切なグリッド配置、および使いやすさをタッチするフォームのガイドラインに従ってください。

-   読みやすさを向上させるためにシンプルなレイアウトを使用します。

-   タブに容易にできるように、スクリーン キーボードを使用して、長い形式の垂直方向のスクロールを使用します。

-   Let のユーザーの確認と購入のフローを開始する前にプランを選択します。

-   初めて購入する、web 経由で購入をサポートします。

購入、再充電、補充および課金のページの不適切なデザイン:

-   長い形式の水平方向のスクロールを使用しないでください。

-   すべての空白文字を入力しません。

-   フローをホストするのに iframe を使用しないでください。

-   視覚的なフィードバックを提供することがなく待機時間が長く、ユーザーを作成しません。

-   アプリの外部での web サイトにリンクしないようにします。

## <a name="span-idadditionalresourcesspanspan-idadditionalresourcesspanspan-idadditionalresourcesspanadditional-resources"></a><span id="Additional_resources"></span><span id="additional_resources"></span><span id="ADDITIONAL_RESOURCES"></span>その他のリソース


-   ビューとレイアウトの詳細については: を参照してください[レイアウトの選択](https://msdn.microsoft.com/library/windows/apps/hh465327)します。

-   Listview の詳細については、次を参照してください。[クイック スタート。ListView を追加する](https://msdn.microsoft.com/library/windows/apps/hh465496)します。

-   エラー処理の設計ガイダンスについては、次を参照してください。 [、UI レイアウト](https://msdn.microsoft.com/library/windows/apps/hh465304)します。

-   ユーザー補助のガイダンスについては、次を参照してください。 [、C++ を使用して UWP アプリのユーザー補助機能C#、または Visual Basic](https://msdn.microsoft.com/library/windows/apps/hh452680)します。

-   組み込みのコントロールを使用する方法の詳細については、次を参照してください。[コントロールやコンテンツを追加する](https://msdn.microsoft.com/library/windows/apps/hh465393)します。

-   タッチ入力のガイドラインについては、次を参照してください。[クイック スタート。タッチ入力](https://msdn.microsoft.com/library/windows/apps/xaml/hh465387)します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイル ブロード バンドのアプリのユーザー エクスペリエンスの設計](designing-the-user-experience-of-a-mobile-broadband-app.md)

 

 






