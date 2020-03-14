---
title: モバイル ブロードバンド アプリと他の Windows コンポーネントを統合する
description: モバイル ブロードバンド アプリと他の Windows コンポーネントを統合する
ms.assetid: 70469f6b-70a8-4ebc-b315-08ddeffbdc0f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cad659cb3c38a81b3134cc539e278305dc1c9dc0
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242749"
---
# <a name="integrate-a-mobile-broadband-app-with-other-windows-components"></a>モバイル ブロードバンド アプリと他の Windows コンポーネントを統合する


Windows 10 のユーザーインターフェイス (UI) サーフェイスを使用して、モバイルブロードバンドアプリの全体的なエクスペリエンスを向上させることができます。

レイアウト、ナビゲーション、コマンド処理、アニメーション、タッチ操作、スナップとスケーリング、コントラクトと機能、タイルと通知、UI コントロール、クラウドへのアプリのローミング、および基礎に関するユーザーエクスペリエンスデザインガイドラインの詳細については、「 [UWP アプリの UX ガイドラインのインデックス](https://developer.microsoft.com/windows/apps/design)」を参照してください。

このトピックには、次のセクションが含まれています。

-   [アプリの設定](#app-settings)

-   [ユーザーエクスペリエンスのエラー](#errorux)

-   [アプリ ビュー](#appviews)

-   [起動ポイント](#launchpts)

-   [タイルとトースト通知](#tileandtoast)

-   [スプラッシュスクリーン](#splash)

-   [概要](#qusum)

-   [その他のリソース](#resources)

## <a name="app-settings"></a>アプリの設定


アプリの[設定](https://docs.microsoft.com/windows/uwp/app-settings/guidelines-for-app-settings)を使用して、アプリの構成の設定を含めることができます。 これらの例を次に示します。

-   サインインとサインアウト

-   ユーザープロファイルの表示と編集

-   請求先住所の変更

-   支払いオプションを表示および編集する

-   マーケティング設定の表示と設定

## <a name="span-iderroruxspanspan-iderroruxspanerror-user-experience"></a><span id="errorux"></span><span id="ERRORUX"></span>ユーザーエクスペリエンスのエラー


### <a name="span-idgeneralspanspan-idgeneralspanspan-idgeneralspangeneral"></a><span id="General"></span><span id="general"></span><span id="GENERAL"></span>総

モバイルブロードバンドアプリには、適切に対処する必要があるさまざまなエラーケースがあります。 一般的な例を次に示します。

-   **デバイスが見つからないか、または取り外されてい**ますSIM やドングルなどのデバイスが見つからないか、または取り外された場合に表示されます。

-   **ロック**されたデバイス接続されているデバイスがユーザーにロックされているときに表示されます。

-   **インターネット接続が失わ**れましたネットワーク接続が検出されなかった場合に表示されます。

-   **複数のデバイスが接続されてい**ます組み込みアダプターと外部ドングルが接続されている場合に表示されます。 このような場合は、通知バーエラーを使用することをお勧めします。

-   **フォームフィールドの検証エラー**ユーザーが正しくない情報をフォームに入力したときに表示されます。 エラーが関連付けられているフィールドをユーザーが認識できるように、検証エラーをインラインで表示する必要があります。

エラーを表示する方法については、「 [UI のレイアウト](https://docs.microsoft.com/previous-versions/windows/apps/hh465304(v=win.10))」を参照してください。 次の例では、ページの上部に通知バーが表示されます。

![通知バーにエラーが表示される](images/mb-fig1-notificationbarerrors.png)

### <a name="span-iderrors_in_data_usagespanspan-iderrors_in_data_usagespanspan-iderrors_in_data_usagespanerrors-in-data-usage"></a><span id="Errors_in_data_usage"></span><span id="errors_in_data_usage"></span><span id="ERRORS_IN_DATA_USAGE"></span>データ使用状況のエラー

次のエラーケースは、次の方法で [概要] ページに表示されます。

-   **ユーザーのプランの有効期限が近づい**ている場合: 画面の上部にあるバーを使用して、ユーザーのプランが有効期限切れに近いことを示します。

-   **使用量がデータキャップを超えている場合**データバーがいっぱいになり、問題を説明するインラインメッセージも表示され、ユーザーに対して何を実行するかが示されます。 または、ページの上部にある通知バーに、[over data cap usage] \ (データキャップの使用 \) メッセージが表示されます。

-   **プランの有効期限が切れた場合**: 概要ボックスの上部にあるバーを使用して、ユーザーが実行できる問題とアクションを説明します。 この場合、データの使用状況、請求サイクル、およびローミング情報は表示されません。

-   **国際ローミング**: [概要] セクションの下部にある [ローミング] を指定します。

## <a name="span-idappviewsspanspan-idappviewsspanapp-views"></a><span id="appviews"></span><span id="APPVIEWS"></span>アプリビュー


アプリはアダプティブで、次のようなさまざまなレイアウトに適合できる必要があります。

-   [横]

-   [縦]

-   別のアプリとサイドバイサイドで

-   ら

-   キーボード上

    **メモ**   タッチキーボードが起動している場合は、フォームフィールドなどの要素が適切にスクロールすることを確認してください。

     

次の例では、一部のページが他のアプリと並べて表示されています。

![別のアプリとサイドバイサイドでランディングページ](images/mb-fig2-snappedview-landingpage.png)

![[サービス] ページと別のアプリのサイドバイサイド](images/mb-fig3-snappedview-servicespage.png)

ハイコントラストモードやスクリーンリーダーの準備など、アプリビューからアプリにアクセスできることを確認します。 アプリにアクセスできるようにする方法の詳細については、「 [JavaScript を使用した UWP アプリのユーザー補助](https://docs.microsoft.com/previous-versions/windows/apps/hh452681(v=win.10))」を参照してください。

## <a name="span-idlaunchptsspanspan-idlaunchptsspanlaunch-points"></a><span id="launchpts"></span><span id="LAUNCHPTS"></span>起動ポイント


モバイルブロードバンドアプリは、ユーザーが [すべての**アプリ**] ビュー、Windows 接続マネージャー、またはトースト通知を使用して利用できます。

![アプリを開始するためのエントリポイント](images/mb-fig4-entrypoints.png)

### <a name="span-idlaunch_from_windows_connection_managerspanspan-idlaunch_from_windows_connection_managerspanspan-idlaunch_from_windows_connection_managerspanlaunch-from-windows-connection-manager"></a><span id="Launch_from_Windows_Connection_Manager"></span><span id="launch_from_windows_connection_manager"></span><span id="LAUNCH_FROM_WINDOWS_CONNECTION_MANAGER"></span>Windows 接続マネージャーから起動する

![windows 接続マネージャーを使用してアプリを起動する](images/mb-fig5-startfromwcm.png)

Windows 接続マネージャーを使用して、モバイルブロードバンドアプリに接続できます。 アプリは、アカウントとデータの使用状況に関する情報を含むランディングページを開く必要があります。 接続すると、現在のアカウントとデータの使用状況が Windows 接続マネージャーに表示されます。

![windows 接続マネージャーのアカウント情報](images/mb-fig6-wcmaccountinfo.png)

**専用ポータルの購入フロー中の接続マネージャーからの自動起動**

Web トラフィックがリダイレクトされる専用のポータルネットワークにユーザーが接続されている場合、Windows には、アプリがインストールされている場合に自動的に起動するオプションが用意されています。 アプリは、インターネットアクセスを購入する方法に関する情報を提供する [プラン] ページを開く必要があります。

### <a name="span-idlaunch_app_from_tile_in_all_apps_viewspanspan-idlaunch_app_from_tile_in_all_apps_viewspanspan-idlaunch_app_from_tile_in_all_apps_viewspanlaunch-app-from-tile-in-all-apps-view"></a><span id="Launch_app_from_tile_in_All_Apps_view"></span><span id="launch_app_from_tile_in_all_apps_view"></span><span id="LAUNCH_APP_FROM_TILE_IN_ALL_APPS_VIEW"></span>すべてのアプリビューでタイルからアプリを起動する

アプリでは、複数の同時アカウントを持つユーザーをサポートする必要があります (たとえば、2つの外部 USB モバイルブロードバンドアダプターを使用します)。 アプリをタイルから起動する場合は、使用するアカウントをユーザーが選択できるようにする必要があります。

アプリが中断されているか、既に実行されている場合は、最後に使用されたページが表示されます。 アプリがまだ実行されていない場合、または中断情報を使用できない場合は、アプリがランディングページを開く必要があります。

### <a name="span-idtileandtoastspanspan-idtileandtoastspantile-and-toast-notifications"></a><span id="tileandtoast"></span><span id="TILEANDTOAST"></span>タイルとトースト通知

**[スタート]** メニューには、アプリの主要な表現がタイルとして表示されます。 ユーザーは、これらのタイルを使用してアプリを起動します。これにより、通知によって、新規、関連、および調整されたコンテンツを表示できます。 これにより、 **[スタート]** メニューが鮮やかになり、ユーザーがひとめで最新情報を確認できるようになります。 アプリでは、トースト通知、ユーザーが別のアプリにあるか、**スタート**画面、デスクトップであるかにかかわらず、時間のかかる重要なイベントをユーザーに伝えることもできます。 トーストを設計および配信する方法はタイルのものとよく似ているため、学習曲線が減少します。

![スタート画面のタイル](images/mb-fig7-startscreentile.png)

トースト通知にはテキストとイメージを含めることができますが、ボタンなどの二次的な操作はサポートされていません。 トーストは、タスクバーの通知領域からの Windows バルーン通知に似ていると考えてください。 バルーン通知と同様に、トーストは画面の右下隅に表示されます。 ユーザーがトーストをタップまたはクリックすると、関連付けられているアプリが、通知に関連するビューで起動されます。 これは、あるアプリが別のアプリでユーザーを中断できる唯一のメカニズムです。 Toasts は、ユーザーによるアクティブ化、破棄、または無視を行うことができます。 ユーザーは、アプリのすべてのトーストを無効にすることができます。

![トースト通知](images/mb-fig8-toastonpage.png)

トースト通知は、ユーザーにとって重要な情報に対してのみ使用してください。通常は、何らかの形式のユーザーオプトインが関係します。 これは、受信電子メールアラート、IM チャット要求、およびニュース速報に適しています。 ただし、トースト通知の使用を検討する際には、一時的な性質上、ユーザーに表示されない場合があることに注意してください。 データ使用量の超過またはローミングアラートにトースト通知を使用する場合は、エンドユーザーがトースト通知を受信しなかった場合に備えて、タイルとアプリビュー内の情報を表示することを検討してください。

### <a name="span-idsplashspanspan-idsplashspansplash-screen"></a><span id="splash"></span><span id="SPLASH"></span>スプラッシュスクリーン

スプラッシュスクリーンを使用して、ブランド化を促進することができます。 スプラッシュスクリーンの詳細については、「[スプラッシュスクリーンの追加](https://docs.microsoft.com/previous-versions/windows/apps/hh465332(v=win.10))」を参照してください。

![スプラッシュ スクリーン](images/mb-fig4-splash-screen.png)

### <a name="span-idqusumspanspan-idqusumspanquick-summary"></a><span id="qusum"></span><span id="QUSUM"></span>概要

オペレーターへの通知に適した設計:

-   トースト通知とタイル通知の両方を使用して、サブスクライバーのアカウントとサービスプランに関連する重要なメッセージと重要度の高いメッセージをユーザーに警告します。

-   自分のブランドガイドラインに基づいて、トーストおよびタイルの背景色とロゴをカスタマイズします。

-   重要な SMS または USSD オペレーターの通知と、サブスクライバーのアカウントとサービスプランに直接対応するアラートを、ランディングページに追加します。

オペレーター通知の不適切な設計:

-   リアルタイムではない情報 (プロモーション広告など) のトースト通知を表示しません。

-   エンドユーザーが重要なオペレーター通知を見逃してしまう可能性があるため、ユーザーからユーザーへのチャットメッセージやプロモーションや広告をオペレーターの通知とアラートと一緒に表示しないようにしてください。

### <a name="span-idresourcesspanspan-idresourcesspanadditional-resources"></a><span id="resources"></span><span id="RESOURCES"></span>その他のリソース

-   [タイル、バッジ、およびトースト通知の操作](https://docs.microsoft.com/previous-versions/windows/apps/hh868259(v=win.10))

-   [トースト通知のガイドラインとチェックリスト](https://docs.microsoft.com/windows/uwp/controls-and-patterns/tiles-badges-notifications)

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイルブロードバンドアプリのユーザーエクスペリエンスの設計](designing-the-user-experience-of-a-mobile-broadband-app.md)

 

 






