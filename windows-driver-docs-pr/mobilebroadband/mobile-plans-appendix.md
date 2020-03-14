---
title: モバイルプランの概要 (付録)
description: このトピックでは、モバイルプランプログラムの付録情報について説明します。
ms.assetid: B3B478DB-78F4-4031-B041-DCBAACC15D6F
keywords:
- Windows Mobile プラン付録、モバイルプラン付録モバイルオペレーター
ms.date: 07/05/2019
ms.localizationpriority: medium
ms.openlocfilehash: 0a1af5c5101a1493efedce5339a32495e632aa50
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242745"
---
# <a name="mobile-plans-general-appendix"></a>モバイルプランの概要 (付録)

## <a name="web-portal-flow-and-reference-design"></a>Web ポータルのフローと参照のデザイン

この参照設計は、お客様のブランドと製品を最適に表すために変更できるテンプレートです。 この参照設計は、ナビゲーション要素、ブランド化の場所、および web サイトの機能を備えた、推奨される UX 設計を示しています。

### <a name="mo-direct-reference-site-walkthrough"></a>MO ダイレクトリファレンスサイトのチュートリアル

1. ユーザーは、[続行] ボタンをクリックします。

    <img src="images/dynamo_appendix_mo_direct_1_continue.png" alt="MO Direct walkthrough: user clicks on the continue button" title="MO ダイレクトチュートリアル: ユーザーが [続行] ボタンをクリックする" width="600" />

    - このダイアログは、モバイルプランアプリによって求められます。

2. ユーザーが MO Direct ポータルに入り、MO アカウントを使用してサインインします。

    <img src="images/dynamo_appendix_mo_direct_2_sign_in.png" alt="MO Direct walkthrough: user enters MO Direct portal and signs in with their MO account" title="MO ダイレクトチュートリアル: ユーザーが MO Direct ポータルに入り、MO アカウントでサインインする" width="600" />

    - ページレイアウトは、すべてのページにわたって一貫しています。 たとえば、ロゴ要素とブランド要素は左上にあり、ナビゲーション要素は下部にあります。
    - サインインページをリンクして、新しいアカウントにサインアップすることができます。
    - "パスワードを忘れた" は省略可能です。 ユーザーは Walled 庭園にあり、モバイルプランアプリのみがインターネットにアクセスできることに注意してください。 MO ダイレクトポータルでのパスワードのリセットをサポートする場合は、ユーザーがデバイスでブラウザーまたは電子メールアプリを起動せずに、2 ~ 3 つの手順でリセットできることを確認してください。

3. ユーザーは、次のオプションを選択します。

    <img src="images/dynamo_appendix_mo_direct_3_options.png" alt="MO Direct walkthrough: user picks an option" title="MO Direct チュートリアル: ユーザーがオプションを選択する" width="600" />

    - ページの中央に、最も重要なコンテンツ (利用可能なサービス) を提示します。
    - ロゴとブランド化の要素は、左上隅にあります。
    - ナビゲーションボタンは右下隅にあります。
    - 使用可能なオプションには大きなタイルを使用し、サービスカテゴリのタイトルと短い説明を使用します。
    - [次へ] と [キャンセル] の両方のボタンを使用して、ユーザーが前方または exit を参照できます。 MO Direct の予期されるデータサービスカテゴリには、前払いプラン、定期的な月単位のプラン、および既存のプランへの新しいデバイスの接続が含まれている場合があります。

4. ユーザーが注文を送信します。

    <img src="images/dynamo_appendix_mo_direct_4_submit_order.png" alt="MO Direct walkthrough: user submits an order" title="MO ダイレクトチュートリアル: ユーザーが注文を送信する" width="600" />

    - ページレイアウトは、すべてのページにわたって一貫しています。 たとえば、ロゴ要素とブランド要素は左上にあり、ナビゲーション要素は下部にあります。
    - サービスの利用規約リンクは、web ページに表示される必要があります。
    - 注文の確認ページには、データサービスの詳細、支払い方法、支払い額など、注文を送信する前にユーザーが確認する重要な情報が表示されます。

5. ユーザーがいつでも MO ダイレクトフローをキャンセルした場合は、次のようになります。

    <img src="images/dynamo_appendix_mo_direct_5_cancel.png" alt="MO Direct walkthrough: user cancels MO Direct flow" title="MO Direct チュートリアル: ユーザーが MO ダイレクトフローをキャンセルする" width="600" />

    - MO Direct エクスペリエンスを終了するための確認ダイアログには、Mobile plan アプリによってメッセージが表示されます。

6. 注文が完了しました:

    <img src="images/dynamo_appendix_mo_direct_6_order_complete.png" alt="MO Direct walkthrough: order complete" title="MO ダイレクトチュートリアル: 注文完了" width="600" />

    - これは、モバイルオペレーターポータルの一部であるトランザクション確認の例を示しています。
    - 注文が正常に処理され、この場合、[Continue (続行)] をクリックした後、通知は、購入結果、eSIM ライセンス認証コード、API で必要なその他の情報を使用して、モバイルプランアプリに投稿されます。 ユーザーは、モバイルプランアプリの PDP (製品の詳細ページ) に自動的にリダイレクトされます。
    - トランザクションが物理的な SIM カード用であるか、アクティブな eSIM プロファイルが配置されている場合は、バックエンドでプランをアクティブ化する必要があります。
    - トランザクションで新しいプロファイルをダウンロードする必要がある場合は、次の手順に進みます。

7. ESIM プロファイルをダウンロードしています (該当する場合):

    <img src="images/dynamo_appendix_mo_direct_7_downloading_esim_profile.png" alt="MO Direct walkthrough: downloading an eSIM profile (if applicable)" title="MO ダイレクトチュートリアル: eSIM プロファイルのダウンロード (該当する場合)" width="600" />

    - ESIM プロファイルをダウンロードしています。

8. MO Direct プランがアクティブ化されます。

    <img src="images/dynamo_appendix_mo_direct_8_activated.png" alt="MO Direct walkthrough: MO Direct plan is activated" title="MO Direct チュートリアル: MO Direct プランがアクティブ化されている" width="600" />

    - デバイスは接続されています。
    - ユーザーは、アクティブな MO ダイレクトアカウントを持っています。

### <a name="hyperlink-experience"></a>ハイパーリンクエクスペリエンス

MO ダイレクトポータルで新しいページを指すハイパーリンクがあり、ユーザーがそれをクリックすると、web ビューコントロールによってそのページが同じウィンドウに表示されます。 ユーザーは、モバイルプランアプリの [戻る] ボタンをクリックして、前のページに戻る必要があります。

または、ハイパーリンクを使用して、WebView コントロールのコンテキスト内でダイアログを起動することもできます。

### <a name="back-button-experience"></a>戻るボタンの操作

Mobile plan アプリのメニューバーの [戻る] ボタンをクリックすると、web ブラウザーの場合と同じように、ユーザーが前のページに移動します。 

> [!IMPORTANT]
> ユーザーが入力したデータを失うことなく前の状態に戻るようにする場合は、ショッピングカートのエクスペリエンスを構築する場合と同様に、MO ダイレクトポータルを構築します。

<img src="images/dynamo_appendix_mo_direct_9_back_button.png" alt="MO Direct walkthrough: back button example" title="MO ダイレクトチュートリアル: [戻る] ボタンの例" width="600" />

### <a name="error-while-loading-the-mo-direct-experience"></a>MO Direct エクスペリエンスの読み込み中にエラーが発生しました

MO ダイレクトポータルで未処理のエラーまたは例外が発生し、モバイルプランアプリが MO Direct エクスペリエンスの読み込みに失敗すると、次のエラーが表示されます。

<img src="images/dynamo_appendix_mo_direct_10_error.png" alt="MO Direct walkthrough: error example" title="MO ダイレクトチュートリアル: エラーの例" width="600" />

## <a name="high-level-integration-schedule"></a>高レベルの統合スケジュール

次の表に、*モバイルプラン*プロジェクトの統合スケジュールの概要を示します。

| フェーズ | 活動 | 所有者 | 推定時間 |
| --- | --- | --- | --- |
| 実装 | Windows デバイスにインストール可能な eSIM プロファイル。 SMDP + を使用してテストし、ステージング環境と運用環境に使用します。 | 月 |  |
|                | ステージング環境のサービス構成を含むオンボードのチェックリストドキュメントを提供する | 月 |  |
|                | モバイル*プラン*ステージング環境でモバイルオペレーターステージング環境を有効にする | MF | 毎月第1および第3金曜日に構成の更新が行われます。 |
|                | COSA データベース更新の送信 | 月 | 約3か月 |
|                | MO ダイレクトポータル開発の開始 |  |
|                | `GetBalance` API 開発の開始 |  |
| Integration | Walled 庭園を有効にする | 月 |  |
|             | COSA 更新プログラムの検証 | 月 |  |
|             | MO ダイレクトポータルの開発完了 | 月 |  |
|             | `GetBalance` API 開発の完了 | 月 |  |
|             | MO 開発完了-コード完了 (チェックポイント) | 月 |  |
|             | `GetBalance` API 機能の検証 | 月 |  |
|             | エンドツーエンドのエクスペリエンスは、MO ステージング環境 (チェックポイント) で機能します。 | 月 |  |
|             | 運用環境の設定を反映するようにサービス構成ドキュメントを更新する (以前に提供されていない場合) | 月 |  |
|             | `GetBalance` ロードテストに使用する ICCIDs を指定する | 月 |  |
|             | モバイル*プラン*ステージング環境でモバイルオペレーターの運用環境環境を有効にする | MF | 毎月第1および第3金曜日に構成の更新が行われます。 |
|             | エンドツーエンドのエクスペリエンスは、MO 運用環境 (チェックポイント) で機能します。 | 月 |  |
| 検証 | 終了条件のテストケース完了 | 月 |  |
|           | テストケースの結果の確認 | MF |  |
|           | サインオフのテスト (チェックポイント) | MF |  |
| 段階的 | `GetBalance` API のロードテスト | MSFT と MO | 1 週間 |
|         | 監視とエスカレーションのパス | MF | 1 週間 |
|         | カスタマーサポートが実施される | MSFT と MO |  |
|         | コマーシャル契約が完了しました | 月 |  |
|         | Windows で使用可能な COSA 更新プログラム | MF |  |
|         | ゴー/いいえ (最終的なチェックポイント) | MSFT と MO |  |
|         | *モバイルプラン*運用環境での MO 運用環境環境の構成 | MF |  |
|         | Launch | MSFT と MO | ローカル検証が確実に行われるようにするには、起動日時に同意する必要があります |