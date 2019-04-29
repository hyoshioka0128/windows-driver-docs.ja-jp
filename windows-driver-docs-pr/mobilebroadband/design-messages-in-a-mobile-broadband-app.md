---
title: モバイル ブロードバンド アプリでメッセージを設計する
description: モバイル ブロードバンド アプリでメッセージを設計する
ms.assetid: 314fd479-7dcf-4559-a195-26e4c020446c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3704008076dd6468d5f95adf4194ddca58f1a26e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383772"
---
# <a name="design-messages-in-a-mobile-broadband-app"></a>モバイル ブロードバンド アプリでメッセージを設計する


モバイル ブロード バンド アプリは、重要なアカウント情報について、お客様との通信に便利な方法です。 アプリは、エンドユーザーが重要なアカウント メッセージを表示できる、ホーム画面上のセクションまたはリンクが必要です。 While 演算子メッセージとして表示されるタイルとトースト通知では、それらも表示するかアプリ ビューでトースト通知とタイル通知を表示するテキストの限られた量の一時的な性質のために重要です。

お客様は、重要な演算子の通知を見逃す可能性があるため、オペレーターの通知とアラートと共に混合 messages セクションにユーザーにチャット テキスト メッセージング、プロモーション、および提供情報を表示する必要があります。 アプリのレイアウトのプロモーションと広告を表示し、ユーザー インターフェイスの別のセクションでユーザーにチャット テキスト メッセージを表示できます。

![メッセージ](images/message.png)

次の表は、いくつかの例の演算子のメッセージと警告を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>型</th>
<th>メッセージの例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>国際対応のローミング</p></td>
<td><p>英国へようこそ。 1 日につき 5 ドルの 25 MB のデータであり、1 MB あたり 1 ドルになります。 SMS は、メッセージごとに $0.49 です。詳細については、www.contoso.com/rates/uk について説明します。</p></td>
</tr>
<tr class="even">
<td><p>データ使用量の超過料金</p></td>
<td><p>4 GB のデータ プラン全体を使用しました。 $10 GB/@ 超過分は課金されます。 今日、プランのページで、プランをアップグレードすることでより多くのデータを保存します。</p></td>
</tr>
<tr class="odd">
<td><p>データ使用状況</p></td>
<td><p>40 GB データ プランの 65% を使用しました。 $5 GB/@ 超過分請求書。 ヒント:Wi-fi 経由でデータを制限することはありません。 プランのページで詳しく説明します。</p></td>
</tr>
<tr class="even">
<td><p>プランの有効期限</p></td>
<td><p>ご利用のプランは、2013 年 7 月 1 日に有効期限が切れました。 プランのページに移動して、プランを更新します。</p></td>
</tr>
<tr class="odd">
<td><p>アカウントの更新</p></td>
<td><p>お知らせ: 有効なすぐに、Contoso が増加している 4 GB に 2 GB から DataPro テザリング計画に含まれるデータの量。 プランの月額料金は変更されませんし、ユーザー操作は必要ありません。 優れたまこといただきありがとうございます。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idquicksummaryspanspan-idquicksummaryspanspan-idquicksummaryspanquick-summary"></a><span id="Quick_summary"></span><span id="quick_summary"></span><span id="QUICK_SUMMARY"></span>簡単な概要


演算子のメッセージを表示するための適切なデザイン:

-   受信したすべてのメッセージの一覧を表示する機能が含まれて、メッセージの完全な詳細情報を表示し、メッセージを削除します。

-   または、アプリで、独自のページで、アプリのホーム画面のセクションでは、重要な演算子のメッセージを表示します。

演算子のメッセージを表示するための不適切なデザイン:

-   テキスト メッセージをユーザーにチャットとプロモーションとオペレーターの通知とアラートと共に混合の提供情報を表示しません。

## <a name="span-idadditionalresourcesspanspan-idadditionalresourcesspanspan-idadditionalresourcesspanadditional-resources"></a><span id="Additional_resources"></span><span id="additional_resources"></span><span id="ADDITIONAL_RESOURCES"></span>その他のリソース


-   使用[ **ListView** ](https://msdn.microsoft.com/library/windows/apps/br211837)メッセージを表示します。 詳細については、次を参照してください。[リスト ビューの追加、セマンティック ズーム、およびその他のデータ コントロール](https://msdn.microsoft.com/library/windows/apps/hh465409)します。

-   表示し、メッセージを削除するには、アプリ バーのコントロールを使用します。 詳細については、次を参照してください。[アプリ バーのガイドライン](https://msdn.microsoft.com/library/windows/apps/hh465302)します。

-   [その他の Windows コンポーネントと統合して、モバイル ブロード バンド アプリ](integrate-a-mobile-broadband-app-with-other-windows-components.md#tileandtoast)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイル ブロード バンドのアプリのユーザー エクスペリエンスの設計](designing-the-user-experience-of-a-mobile-broadband-app.md)

 

 






