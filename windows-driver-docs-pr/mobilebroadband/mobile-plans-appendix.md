---
title: Mobile のプランの付録
description: このトピックでは、Mobile プラン プログラムの付録の情報について説明します。
ms.assetid: B3B478DB-78F4-4031-B041-DCBAACC15D6F
keywords:
- Windows Mobile プラン付録、Mobile のプランの付録モバイル演算子
ms.date: 03/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: 0451a6ad8243ed59e7209edfcdf09d8c5d042471
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357825"
---
# <a name="mobile-plans-appendix"></a>Mobile のプランの付録

## <a name="web-portal-flow-and-reference-design"></a>Web ポータルのフローと参照設計

この参照設計は、独自のブランドと製品を最適に表すには変更可能なテンプレートです。 この参照設計では、場所、および機能の web サイトをブランド化のナビゲーション要素を持つことをお勧めの UX デザインを示します。

### <a name="mo-direct-reference-site-walkthrough"></a>月の直接参照サイトのチュートリアル

1. [続行] ボタンをクリックしたユーザー。

    <img src="images/dynamo_appendix_mo_direct_1_continue.png" alt="MO Direct walkthrough: user clicks on the continue button" title="MO 直接チュートリアル: ユーザーが [続行] ボタンをクリックして" width="600" />

    - このダイアログ ボックスは、プランのモバイル アプリによって求められます。

2. ユーザーは、MO 直接ポータルを入力し、その月のアカウントでサインインします。

    <img src="images/dynamo_appendix_mo_direct_2_sign_in.png" alt="MO Direct walkthrough: user enters MO Direct portal and signs in with their MO account" title="MO 直接チュートリアル: ユーザーが直接 MO ポータルと、MO アカウントを使ってサインイン入力" width="600" />

    - ページ レイアウトは、すべてのページ全体で一貫性のあります。 たとえば、ロゴおよびブランド要素は左、上であり、ナビゲーション要素が下部にあります。
    - サインイン ページは、新しいアカウントのサインアップをリンクできます。
    - 「パスワードを忘れた場合」は省略可能です。 Walled Garden に、ユーザーが、プランのモバイル アプリのみがインターネットにアクセスできることに注意してください。 MO 直接ポータルから、パスワード リセットをサポートする場合は、ことユーザー リセットできます 2 つまたは 3 つの手順で、ブラウザーまたはデバイスの電子メール アプリを起動しなくてもを確認します。

3. ユーザーは、オプションを取得します。

    <img src="images/dynamo_appendix_mo_direct_3_options.png" alt="MO Direct walkthrough: user picks an option" title="MO 直接チュートリアル: ユーザーは、オプションを取得" width="600" />

    - 最も重要なコンテンツ、使用可能なサービス、ページの中心を紹介します。
    - ロゴおよびブランド要素は左上隅です。
    - ナビゲーション ボタンは、右下隅には。
    - タイトルと、サービス カテゴリの簡単な説明と、使用可能なオプションには、大規模なタイルを使用します。
    - [次へ]、[キャンセル] ボタンの両方を前方に移動または終了するユーザーを利用できます。 MO 直接想定データ サービスのカテゴリは、プリペイド プランを含めることができます月間プランは、定期的な既存のプランに新しいデバイスをアタッチします。

4. ユーザーは、注文を送信します。

    <img src="images/dynamo_appendix_mo_direct_4_submit_order.png" alt="MO Direct walkthrough: user submits an order" title="MO 直接チュートリアル: ユーザーが注文を送信します。" width="600" />

    - ページ レイアウトは、すべてのページ全体で一貫性のあります。 たとえば、ロゴおよびブランド要素は左、上であり、ナビゲーション要素が下部にあります。
    - サービス利用規約のリンクは、web ページに表示である必要があります。
    - 注文の確認 ページには、ユーザーは、データ サービス、支払い方法、支払いなどの量の詳細を含む、注文を送信する前に確認する重要な情報が一覧表示します。

5. 場合は、ユーザーは、いつでも、MO を直接フローをキャンセルします。

    <img src="images/dynamo_appendix_mo_direct_5_cancel.png" alt="MO Direct walkthrough: user cancels MO Direct flow" title="MO 直接チュートリアル: ユーザーが月を直接フローをキャンセル" width="600" />

    - 月の直接のエクスペリエンスのままにする確認のダイアログ ボックスは、プランのモバイル アプリで求められます。

6. 注文を完了するとします。

    <img src="images/dynamo_appendix_mo_direct_6_order_complete.png" alt="MO Direct walkthrough: order complete" title="MO 直接チュートリアル: 注文完了" width="600" />

    - これは、携帯電話会社ポータルの一部であるトランザクションの確認の例を示します。
    - 注文が処理されると正常にし、この場合、[続行] をクリックした後、購入の結果、esim 状のライセンス認証コード、および API で必要なその他の情報を使用してアプリを Mobile プランに通知を投稿する必要があります。 ユーザーは、プランのモバイル アプリ PDP (製品の詳細 ページ) に自動的にリダイレクトされます。
    - 作業中の eSIM プロファイルが物理 SIM カード用では、トランザクション、または、バックエンドでプランがアクティブ化する必要があります。
    - トランザクションでは、新しいプロファイルをダウンロードする必要がある場合は、次の手順に移動します。

7. (該当する) 場合、eSIM プロファイルのダウンロード。

    <img src="images/dynamo_appendix_mo_direct_7_downloading_esim_profile.png" alt="MO Direct walkthrough: downloading an eSIM profile (if applicable)" title="MO 直接チュートリアル: (該当する) 場合、eSIM プロファイルのダウンロード" width="600" />

    - Esim 状のプロファイルをダウンロードしています。

8. MO Direct のプランがアクティブ化されます。

    <img src="images/dynamo_appendix_mo_direct_8_activated.png" alt="MO Direct walkthrough: MO Direct plan is activated" title="MO 直接チュートリアル:MO Direct プランをアクティブ化します。" width="600" />

    - デバイスが接続されています。
    - ユーザーは、アクティブな月ダイレクト アカウントです。

### <a name="hyperlink-experience"></a>ハイパーリンクのエクスペリエンス

MO 直接ポータルと、ユーザーがクリックで新しいページを指すハイパーリンクにする場合は、web ビューのコントロールは、同じウィンドウで、そのページに表示されます。 ユーザーは、前のページに戻るにプランのモバイル アプリで [戻る] ボタンをクリックする必要があります。

また、WebView コントロールのコンテキスト内でのダイアログを起動するのにハイパーリンクを使用する可能性があります。

### <a name="back-button-experience"></a>戻るボタンのエクスペリエンス

プランのモバイル アプリのメニュー バーで [戻る] ボタンは、web ブラウザーで前のページにユーザーと同じように移動されます。 

> [!IMPORTANT]
> 場合は、ユーザーが入力したすべてのデータを失うことがなく、以前の状態に戻るには、ショッピング カートの操作を構築している場合に、MO 直接ポータルを構築します。

<img src="images/dynamo_appendix_mo_direct_9_back_button.png" alt="MO Direct walkthrough: back button example" title="MO 直接チュートリアル: [戻る] ボタンの例" width="600" />

### <a name="error-while-loading-the-mo-direct-experience"></a>月の直接のエクスペリエンスの読み込み中にエラー

ハンドルされないエラーがあるかまたは MO 直接読み込みに失敗するプランのモバイル アプリを原因となる、MO 直接ポータルでの例外が発生したときに、次のエラーが表示されます。

<img src="images/dynamo_appendix_mo_direct_10_error.png" alt="MO Direct walkthrough: error example" title="MO 直接チュートリアル: エラーの例" width="600" />

## <a name="high-level-integration-schedule"></a>高レベルの統合のスケジュール

次の表の大まかな概要、 *Mobile プラン*プロジェクト スケジュールの統合。

| フェーズ | アクティビティ | 所有者 | 推定所要時間 |
| --- | --- | --- | --- |
| 実装 | esim 状のプロファイルが Windows デバイスにインストール可能です。 使用して SMDP + ステージング環境と運用環境の使用をテストします。 | 月 |  |
|                | ステージング環境のサービス構成を含め、オンボード チェックリスト ドキュメントを提供します。 | 月 |  |
|                | 通信事業者のステージング環境を有効にするのに、 *Mobile プラン*ステージング環境 | MSFT | 構成の更新がすべての月の 1 番目と 3 番目の金曜日に発生します。 |
|                | COSA データベースの更新を送信します。 | 月 | 約 3 か月 |
|                | MO 直接ポータル開発の開始 |  |
|                | `GetBalance` API の開発の開始 |  |
| 統合 | 高い庭を有効にします。 | 月 |  |
|             | 更新プログラムを COSA 検証します。 | 月 |  |
|             | MO 直接ポータル開発の完了 | 月 |  |
|             | `GetBalance` 完全な API の開発 | 月 |  |
|             | 月の開発が完了 - コードの完了 (チェックポイント) | 月 |  |
|             | 検証`GetBalance`API の機能 | 月 |  |
|             | エンド ツー エンドのエクスペリエンスがステージング環境の月 (チェックポイント) の機能 | 月 |  |
|             | 更新サービスの構成ドキュメントの運用環境の設定を反映するように (指定されていない場合以前) | 月 |  |
|             | 提供するためにいる Iccid`GetBalance`ロード テスト | 月 |  |
|             | 通信事業者で環境を運用環境を有効にする*Mobile プラン*ステージング環境 | MSFT | 構成の更新がすべての月の 1 番目と 3 番目の金曜日に発生します。 |
|             | エンド ツー エンドのエクスペリエンスが運用環境の月 (チェックポイント) で機能 | 月 |  |
| 検証 | 終了条件のテスト_ケースを完了します。 | 月 |  |
|           | テスト_ケースの結果を確認します。 | MSFT |  |
|           | サインオフ (チェックポイント) のテストします。 | MSFT |  |
| ロールアウト | `GetBalance` API のロード テスト | MSFT と MO | 1 週間 |
|         | 場所で監視とエスカレーション パス | MSFT | 1 週間 |
|         | インプレース カスタマー サポート | MSFT と MO |  |
|         | 商用の契約が完了しました | 月 |  |
|         | Windows で利用可能な COSA 更新 | MSFT |  |
|         | 続行/中止 (最後のチェックポイント) | MSFT と MO |  |
|         | 月の実稼働環境環境構成*Mobile プラン*実稼働環境 | MSFT |  |
|         | Launch | MSFT と MO | 起動の日付と時刻はローカル検証の動作を確実に合意する必要があります。 |