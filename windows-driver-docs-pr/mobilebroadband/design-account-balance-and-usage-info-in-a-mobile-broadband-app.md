---
title: モバイル ブロードバンド アプリで残高と利用状況の情報を設計する
description: モバイル ブロードバンド アプリで残高と利用状況の情報を設計する
ms.assetid: aec4e4b3-d207-4319-a134-29b4a773c3a6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b637f489d35a4e62032a6150fcffe358fac2cc2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572466"
---
# <a name="design-account-balance-and-usage-info-in-a-mobile-broadband-app"></a>モバイル ブロードバンド アプリで残高と利用状況の情報を設計する


主に、ユーザーは、アカウントの残高と使用状況の情報を表示するのにモバイル ブロード バンド アプリを使用します。 このデータがアプリのホーム画面で明確に表示されます。

![後の有料プランの概要](images/mb-fig1-postpaidplansummary.png)

後に有料アカウントの関連するアカウント情報の次のとおりです。

-   アカウントの携帯電話番号

-   アカウントの残高

-   ローミング データを使用すると、使用すると、データと残りの使用状況

-   請求期間またはプランの有効期限日

ユーザーは、ひとめで、(月単位のアカウント) の場合、使用したデータ、左があるデータの量、その場合、課金サイクル終了を明確に理解します。

![前払いプランの概要](images/mb-fig2-prepaidplansummary.png)

前払いアカウントの関連するアカウント情報の次のとおりです。

-   アカウントの携帯電話番号

-   アカウントの残高

-   今すぐ ボタン、支払いページへのリンクを再チャージします。

-   使用されるデータと残り

-   計画 (存在する) 場合の有効期限日

## <a name="span-idquicksummaryspanspan-idquicksummaryspanspan-idquicksummaryspanquick-summary"></a><span id="Quick_summary"></span><span id="quick_summary"></span><span id="QUICK_SUMMARY"></span>簡単な概要


アカウント情報を表示するための適切なデザイン:

-   該当するアカウント情報を表示します。

-   データが最後に更新されたときに表示します。

-   図は、チャートやグラフなどを使用してデータを視覚化するには

    **ヒント:**   で説明したように、確定した進行状況バー コントロールを使用して横棒グラフを実装することができます[進行状況コントロールを追加する](https://msdn.microsoft.com/library/windows/apps/hh465428)します。

     

-   残りの使用率が低いときに、プランをアップグレードするプランのページへのリンクを表示します。

アカウント情報を表示するための不適切なデザイン:

-   データの使用状況の横にある免責事項の長い段落は表示されません。 アカウントの使用」の中心からユーザーがあいまいになることができます。 代わりに、完全な法的免責事項を持つアプリの別のセクションへのリンクを表示します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイル ブロード バンドのアプリのユーザー エクスペリエンスの設計](designing-the-user-experience-of-a-mobile-broadband-app.md)

 

 






