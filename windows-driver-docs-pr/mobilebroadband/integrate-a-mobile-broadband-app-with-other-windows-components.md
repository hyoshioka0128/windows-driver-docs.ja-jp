---
title: その他の Windows コンポーネントと統合して、モバイル ブロード バンド アプリ
description: その他の Windows コンポーネントと統合して、モバイル ブロード バンド アプリ
ms.assetid: 70469f6b-70a8-4ebc-b315-08ddeffbdc0f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c08f251204697d34a24ac41650c92fc168af22a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557602"
---
# <a name="integrate-a-mobile-broadband-app-with-other-windows-components"></a>その他の Windows コンポーネントと統合して、モバイル ブロード バンド アプリ


Windows 10 のユーザー インターフェイス (UI) のサーフェスを使用すると、モバイル ブロード バンド アプリの全体的なエクスペリエンスを向上します。

基礎、やクラウドへのローミング アプリの UI コントロールのレイアウト、ナビゲーション、コマンドの実行、アニメーション、タッチ操作、スナップしスケーリング、コントラクトと機能、タイルおよび通知の追加のユーザー エクスペリエンス デザイン ガイドライン、を参照してください。[UWP アプリ用のインデックスの UX ガイドライン](https://msdn.microsoft.com/library/windows/apps/hh465424)します。

このトピックには、次のセクションが含まれています。

-   [アプリの設定](#app-settings)

-   [エラーのユーザー エクスペリエンス](#errorux)

-   [アプリのビュー](#appviews)

-   [起動ポイント](#launchpts)

-   [タイルとトースト通知](#tileandtoast)

-   [スプラッシュ スクリーン](#splash)

-   [簡単な概要](#qusum)

-   [その他のリソース](#resources)

## <a name="app-settings"></a>アプリの設定


使用することができます[アプリ設定](https://msdn.microsoft.com/library/windows/apps/hh770544)アプリ構成設定を含めます。 これらのいくつかの例は次のとおりです。

-   サインインおよびサインアウト

-   表示して、ユーザー プロファイルの編集

-   請求先住所を変更します。

-   お支払い方法を表示および編集

-   表示およびマーケティングの環境設定を設定します。

## <a name="span-iderroruxspanspan-iderroruxspanerror-user-experience"></a><span id="errorux"></span><span id="ERRORUX"></span>エラーのユーザー エクスペリエンス


### <a name="span-idgeneralspanspan-idgeneralspanspan-idgeneralspangeneral"></a><span id="General"></span><span id="general"></span><span id="GENERAL"></span>[全般]

モバイル ブロード バンド アプリで適切に処理する必要がありますエラー ケースの数を持つことができます。 一般的な例は次のとおりです。

-   **デバイスが見つからないか、接続されていない**SIM やドングルなどのデバイスが見つからないか、接続されていない場合に表示されます。

-   **ロックされたデバイス**をユーザーに、接続されたデバイスがロックされている場合に表示されます。

-   **インターネット接続が失われる**ネットワーク接続が検出されない場合に表示されます。

-   **複数のデバイスが接続されている**組み込みのアダプターと外部のドングルが接続されている場合に表示されます。 このような場合に、通知バーのエラーを使用することをお勧めします。

-   **フォーム フィールドの検証エラー**をフォームに誤った情報が入力されたときに表示されます。 検証エラーはインライン表示するか、ユーザーが、エラーが関連付けられているフィールドを認識できるようにします。

エラーが存在する方法のガイダンスについては、[、UI レイアウト](https://msdn.microsoft.com/library/windows/apps/hh465304)を参照してください。 次の例では、ページの上部にある通知バーが表示されます。

![通知バーは、エラーを示しています。](images/mb-fig1-notificationbarerrors.png)

### <a name="span-iderrorsindatausagespanspan-iderrorsindatausagespanspan-iderrorsindatausagespanerrors-in-data-usage"></a><span id="Errors_in_data_usage"></span><span id="errors_in_data_usage"></span><span id="ERRORS_IN_DATA_USAGE"></span>データの使用状況のエラー

次のエラーの場合は、次の方法で、[概要] ページに表示するか。

-   **ユーザーの場合は、プランの有効期限が近い**:ユーザーのプランの有効期限の近くにあることを示すには、画面の上部にバーを使用します。

-   **使用状況の場合は、データの上限を**データ バーがいっぱいになるし、問題について説明し、それについての対処方法をユーザーに通知するインライン メッセージあります。 または、over には、データ上限の使用状況のメッセージは、ページ上部にある通知バーであることができます。

-   **プランが有効期限が切れて**:概要 ボックスの上部にあるバーを使用して、問題と、ユーザーが実行できるアクションについて説明します。 この場合、請求サイクル、および情報のローミング データの使用状況は表示されません。

-   **海外ローミング**:[概要] セクションの下部にあるローミングを示します。

## <a name="span-idappviewsspanspan-idappviewsspanapp-views"></a><span id="appviews"></span><span id="APPVIEWS"></span>アプリのビュー


アプリはアダプティブや数などのレイアウトに合わせてできる必要があります。

-   横向き

-   縦向き

-   別のアプリと共に

-   入力

-   キーボード

    **注**  タッチ キーボードが、フォームのフィールドなどの要素を適切にスクロールできるようにします。

     

次の例では、別のアプリと並行一部のページを検索する方法を示します。

![別のアプリと並行ランディング ページ](images/mb-fig2-snappedview-landingpage.png)

![別のアプリとサービス ページ](images/mb-fig3-snappedview-servicespage.png)

アプリがアプリ ビュー、ハイ コントラスト モードとスクリーン リーダーの準備などからアクセスできることを確認します。 アプリにアクセスできるようにする方法の詳細については、[JavaScript を使用して UWP アプリのユーザー補助機能](https://msdn.microsoft.com/library/windows/apps/hh452681)を参照してください。

## <a name="span-idlaunchptsspanspan-idlaunchptsspanlaunch-points"></a><span id="launchpts"></span><span id="LAUNCHPTS"></span>起動ポイント


モバイル ブロード バンド アプリでユーザーには、**すべてのアプリ**表示、Windows 接続マネージャーで、または、トースト通知を通じてします。

![アプリを起動するエントリ ポイント](images/mb-fig4-entrypoints.png)

### <a name="span-idlaunchfromwindowsconnectionmanagerspanspan-idlaunchfromwindowsconnectionmanagerspanspan-idlaunchfromwindowsconnectionmanagerspanlaunch-from-windows-connection-manager"></a><span id="Launch_from_Windows_Connection_Manager"></span><span id="launch_from_windows_connection_manager"></span><span id="LAUNCH_FROM_WINDOWS_CONNECTION_MANAGER"></span>Windows 接続マネージャーからの起動

![windows 接続マネージャーを使用してアプリを起動します。](images/mb-fig5-startfromwcm.png)

Windows 接続マネージャーを使用して、モバイル ブロード バンド アプリに接続することができます。 アプリは、アカウントとデータの使用状況情報のランディング ページを開く必要があります。 接続したら、Windows 接続マネージャーは、現在のアカウントとデータの使用状況を示します。

![windows 接続マネージャーのアカウント情報](images/mb-fig6-wcmaccountinfo.png)

**Captive portal 購入フロー中に、接続マネージャーからの自動起動**

ユーザーが web トラフィックがリダイレクトされる場所 captive portal ネットワークに接続されているときに Windows にインストールされている場合、そのアプリを自動的に起動するオプションが提供します。 アプリは、インターネットへのアクセスを購入する方法の情報を提供するプランのページを開く必要があります。

### <a name="span-idlaunchappfromtileinallappsviewspanspan-idlaunchappfromtileinallappsviewspanspan-idlaunchappfromtileinallappsviewspanlaunch-app-from-tile-in-all-apps-view"></a><span id="Launch_app_from_tile_in_All_Apps_view"></span><span id="launch_app_from_tile_in_all_apps_view"></span><span id="LAUNCH_APP_FROM_TILE_IN_ALL_APPS_VIEW"></span>すべてのアプリ ビューでタイルからアプリを起動します。

アプリでは、(たとえば、2 つ外部 USB モバイル ブロード バンドのアダプターを使用して) 複数の同時アカウントを持つユーザーをサポートする必要があります。 タイルからアプリを起動すると、アプリは、ユーザーに使用するアカウントを選択できるようにする必要があります。

アプリが中断または既に実行中である場合は、使用される最後のページが表示されます。 アプリが既に実行されているまたは中断された場合は、情報が利用できない、ランディング ページにアプリを開く必要があります。

### <a name="span-idtileandtoastspanspan-idtileandtoastspantile-and-toast-notifications"></a><span id="tileandtoast"></span><span id="TILEANDTOAST"></span>タイルとトースト通知

**開始** メニューのタイルをアプリのプライマリの表現。 ユーザーは、通知によって新しい、関連する、カスタマイズされたコンテンツを表示できるこれらのタイルをアプリを起動します。 これにより、**開始**メニュー活気のあると考えるし、新機能の概要を参照できます。 アプリを通信することも、トースト通知を通じてユーザーに時間が重要なイベント、ユーザーが別のアプリであるかどうか、**開始** 画面で、またはデスクトップ。 設計し、トーストを密接に配信するための方法と対応のタイル、習得に要する時間が減少します。

![最初の画面のタイル](images/mb-fig7-startscreentile.png)

トースト通知では、テキストとイメージに含めることができますが、ボタンなどのセカンダリのアクションをサポートしていません。 タスク バーの通知領域から Windows バルーン通知に類似するとしてトーストと考えてください。 バルーン通知などは、画面の右下隅にトーストが表示されます。 ユーザーをタップまたはクリックして、トースト、通知に関連するビューに関連付けられているアプリが起動されます。 これは、別のアプリ内のユーザーを 1 つのアプリから中断できる唯一のメカニズムです。 トーストのアクティブ化、閉じる、またはユーザーによって無視されます。 ユーザーは、アプリのすべてのトースト通知を無効にできます。

![トースト通知](images/mb-fig8-toastonpage.png)

トースト通知をユーザーに高い関心のある情報だけに使用する必要があり、通常、何らかの形式のユーザーのオプトインが必要です。 着信電子メールのアラート、IM チャット要求、およびニュース速報のことをお勧めします。 ただし、トースト通知の使用を検討するときにことを認識すること、一時的な性質のため、ユーザーことはありませんが見ることが非常に重要です。 トースト通知のデータ使用量の超過分またはアラートのローミングを使用する場合は、エンドユーザー トースト通知に失敗した場合、タイルでは、アプリ ビュー内で情報を示すことを検討します。

### <a name="span-idsplashspanspan-idsplashspansplash-screen"></a><span id="splash"></span><span id="SPLASH"></span>スプラッシュ スクリーン

スプラッシュ スクリーンを使用すると、ブランド化を促進します。 スプラッシュ スクリーンの詳細については、[スプラッシュ画面の追加](https://msdn.microsoft.com/library/windows/apps/hh465332)を参照してください。

![スプラッシュ スクリーン](images/mb-fig4-splash-screen.png)

### <a name="span-idqusumspanspan-idqusumspanquick-summary"></a><span id="qusum"></span><span id="QUSUM"></span>簡単な概要

オペレーターへの通知を適切なデザイン:

-   トーストの両方を使用し、タイルのサブスクライバーのアカウントとサービス プランに関連する重要かつ高利のメッセージをユーザーに警告通知します。

-   トーストをカスタマイズし、タイルの背景色とロゴをブランドのガイドラインに基づいてください。

-   重要なのか、SMS、USSD operator notifications とランディング ページに直接、サブスクライバーのアカウントとサービス プランに関連したアラートが含まれます。

オペレーターへの通知の不適切なデザイン:

-   (キャンペーン広告) などのリアルタイムではない情報のトースト通知を表示しません。

-   エンドユーザーは、重要な演算子の通知を受信できないことができますので、ユーザーにチャット メッセージとの上位変換と混合 operator notifications と、アラートと共に提供情報を表示しません。

### <a name="span-idresourcesspanspan-idresourcesspanadditional-resources"></a><span id="resources"></span><span id="RESOURCES"></span>その他のリソース

-   [タイル、バッジ、およびトースト通知の使用](https://msdn.microsoft.com/library/windows/apps/xaml/hh868259)

-   [トースト通知のガイドラインとチェックリスト](https://msdn.microsoft.com/library/windows/apps/hh465391)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイル ブロード バンドのアプリのユーザー エクスペリエンスの設計](designing-the-user-experience-of-a-mobile-broadband-app.md)

 

 






