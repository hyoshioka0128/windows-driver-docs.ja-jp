---
title: モバイル ブロード バンド アプリ内課金のページをデザインします。
description: モバイル ブロード バンド アプリ内課金のページをデザインします。
ms.assetid: 44c5a273-1dd4-4ff5-90aa-9d1f4f855439
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2abd40354ef9dd74f550d750593324007ca59070
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551972"
---
# <a name="design-billing-pages-in-a-mobile-broadband-app"></a>モバイル ブロード バンド アプリ内課金のページをデザインします。


ユーザーは、請求履歴、請求の概要を表示、料金を支払う、またはプランを再チャージする機能に提供する必要があります。

![請求書ページの表示](images/mb-fig1-viewbillpage.png)

**支払い**フォームが記載されているフォームのガイドラインに従う必要があります[モバイル ブロード バンド アプリ内購入フローをデザイン](design-purchase-flows-in-a-mobile-broadband-app.md)します。 このページにリンクできる、**課金**ページの後に有料のプランと、**今すぐ再充電**前払いプランのランディング ページ ボタンをします。

![フォームの支払い](images/mb-fig2-makepaymentform.png)

## <a name="span-idquicksummaryspanspan-idquicksummaryspanspan-idquicksummaryspanquick-summary"></a><span id="Quick_summary"></span><span id="quick_summary"></span><span id="QUICK_SUMMARY"></span>簡単な概要


課金情報ページの適切なデザイン:

-   左揃え、空白、適切なグリッドの配置など、フォームのガイドラインに従うし、使いやすさをタッチします。

-   読みやすさを向上させるためにシンプルなレイアウトを使用します。

-   簡単にタブをオンラインのキーボードを使用するため、長い形式の垂直スクロールを使用します。

-   単純なエクスペリエンスを処理する支払を行います。

課金情報ページの不適切なデザイン:

-   空白文字を入力しないでください。

-   フローをホストするのに iframe を使用しないでください。 代わりに、アプリのエクスペリエンスに直接フローを構築します。

-   ユーザーを待たせない視覚的なフィードバックを提供することがなく時間の長い時刻します。

-   アプリの外部で外部のサイトにリンクしないようにします。

## <a name="span-idadditionalresourcesspanspan-idadditionalresourcesspanspan-idadditionalresourcesspanadditional-resources"></a><span id="Additional_resources"></span><span id="additional_resources"></span><span id="ADDITIONAL_RESOURCES"></span>その他のリソース


-   ビューとレイアウトの詳細については: を参照してください[レイアウトの選択](https://msdn.microsoft.com/library/windows/apps/hh465327)します。

-   Listview の詳細については、次を参照してください。[クイック スタート。ListView を追加する](https://msdn.microsoft.com/library/windows/apps/hh465496)します。

-   エラー処理の設計ガイダンスについては、[、UI レイアウト](https://msdn.microsoft.com/library/windows/apps/hh465304)を参照してください。

-   ユーザー補助のガイダンスについては、[、C++ を使用して UWP アプリのユーザー補助機能C#、または Visual Basic](https://msdn.microsoft.com/library/windows/apps/hh452680)を参照してください。

-   組み込みのコントロールを使用する方法の詳細については、[コントロールやコンテンツを追加する](https://msdn.microsoft.com/library/windows/apps/hh465393)を参照してください。

-   タッチ入力のガイドラインについては、次を参照してください。[クイック スタート。タッチ入力](https://msdn.microsoft.com/library/windows/apps/xaml/hh465387)します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイル ブロード バンドのアプリのユーザー エクスペリエンスの設計](designing-the-user-experience-of-a-mobile-broadband-app.md)

 

 






