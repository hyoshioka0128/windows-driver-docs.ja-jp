---
title: Mobile のプランの付録
description: このトピックでは、Mobile プラン プログラムの付録の情報について説明します。
ms.assetid: B3B478DB-78F4-4031-B041-DCBAACC15D6F
keywords:
- Windows Mobile プラン付録、Mobile のプランの付録モバイル演算子
ms.date: 09/17/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: f6a2edbb0ed48e11383401b0e35249263a49276f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530377"
---
# <a name="mobile-plans-appendix"></a>Mobile のプランの付録

[!include[Mobile Plans Beta Prerelease](../mobile-plans-beta-prerelease.md)]

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

## <a name="mobile-plans-user-journey"></a>ユーザー体験のモバイルの計画

次の図は、ユーザーがモバイル プラン プログラムに参加している携帯電話会社に eSIM 対応の Windows に接続されているデバイスをアタッチするときに、体験を示します。

<img src="images/dynamo_appendix_user_journey.png" alt="Mobile Plans user journey" title="ユーザー体験のモバイルの計画" width="400" />

## <a name="high-level-integration-schedule"></a>高レベルの統合のスケジュール

次の表では、プロジェクトの統合の Mobile 計画スケジュールの概要を示します。

| フェーズ | アクティビティ | 所有者 | 推定所要時間 |
| --- | --- | --- | --- |
| 構成 | ICCID の範囲を定義します。 | 月 | なし |
| 構成 | COSA データベースの更新を送信します。 <p>これは、Windows 上の APN 構成は、自動があり、ハード期限 Windows ビルドに含めることのことです。 これより前に、設定を構成および検証してする必要があります。</p> | 月 | 約 2 か月間 |
| 構成 | デベロッパー センター アカウントを作成し、アプリの送信 | 月 | なし |
| 構成 | 月のホワイト リストのアプリとアカウント | MS | 2 日間 |
| 構成 | サービス構成のメールを入力します。 | 月 | なし |
| 構成 | デベロッパー センターでメタデータ パッケージを発行します。 | 月 | なし |
| 実装 | 通信事業者の Api を実装します。 | 月 | なし |
| 実装 | 高い庭を有効にします。 | 月 | なし |
| 実装 | 月の直接の web エクスペリエンスを構築します。 | 月 | なし |
| ［確認］ | MO Api コードの完了 | 月 | なし |
| ［確認］ | 月の API の実装を検証します。 | 月 | なし |
| 統合 | 統合フェーズ中に使用するには、SIM と Esim の一覧を提供します。 | 月 | 1 day |
| 統合 | 構成を検証するには、SIM と Esim | MS | 最大 1 週間 |
| 統合 | DM PPE 環境で MO API ステージング エンドポイントを構成します。 | MS | 最大 1 週間 |
| 統合 | アクティブな SIM (チェックポイント) のテストが完了したら、MO API | MS | 2 週間 |
| 統合 | 月の API は、運用環境 (チェックポイント) | MO (&AMP; M) | なし |
| Launch | DM に MO API エンドポイントを運用環境を送信します。 | 月 | なし |
| Launch | DM PPE 環境で MO API 実稼働エンドポイントを構成します。 | MS | 最大 1 週間 |
| Launch | ロード テスト | MO (&AMP; M) | 1 週間 |
| Launch | 場所で監視とエスカレーション パス | MS | 1 週間 |
| Launch | DM 運用環境で MO API 実稼働エンドポイントを持つ SIM 範囲を小さくするテストを構成します。 | MS | 最大 1 週間 |
| Launch | エンド ツー エンドの検証 (チェックポイント) | 月 | なし |
| Launch | 移動/いいえ (最後のチェックポイント) を参照してください。 | MO (&AMP; M) | なし |
| Launch | DM 実稼働環境で実稼働エンドポイントを MO API と完全 SIM 範囲を構成します。 | MS | 最大 1 週間 |
| Launch | リリースの対応準備の確認の起動 | MS | 2 日間 |
| Launch | Launch | MO (&AMP; M) | なし |