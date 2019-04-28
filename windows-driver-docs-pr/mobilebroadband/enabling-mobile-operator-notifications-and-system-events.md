---
title: 通信事業者の通知とシステム イベントを有効にする
description: 通信事業者の通知とシステム イベントを有効にする
ms.assetid: 988bafcc-ad8e-446d-9336-85c19cf05577
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e16f59242649b95b7eb19ca129babf43569b7bd4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380225"
---
# <a name="enabling-mobile-operator-notifications-and-system-events"></a>通信事業者の通知とシステム イベントを有効にする


このトピックでは、Mobile Operator Notification システム イベントに関する情報を提供します。 SMS、USSD ベースの受信の mobile operator notifications と関連するモバイル ブロード バンドのシステム イベントを処理する UWP モバイル ブロード バンド アプリを開発するためのガイドラインを示します。

## <a name="span-idintroductionspanspan-idintroductionspanspan-idintroductionspanintroduction"></a><span id="Introduction"></span><span id="introduction"></span><span id="INTRODUCTION"></span>概要


モバイル ブロード バンド ネットワーク ブランドの顧客の主な操作は、モバイル ブロード バンド アプリです。 このアプリは、プライマリ接続、管理機能を提供する必要はありませんが、代わりにアカウントの管理やサービス エクスペリエンスを提供します。 アカウントの状態に関する情報を通知するユーザーが引き続き、ユーザーはこれと対話していない場合でも、アプリがいくつかのアクティビティを実行する必要があります。 これらのアクティビティを以下に示します。

-   演算子の SMS またはネットワークが開始した USSD メッセージへの応答

-   データ制限に近づいていることをユーザーに通知します。

-   データ プランの有効期限が切れたことを通知します。

-   ローミングの状態のユーザーに通知します。

-   テザリングがユーザーのデータ プランでサポートされているかどうか確認

### <a name="span-idbackgroundbrokeredworkitemsspanspan-idbackgroundbrokeredworkitemsspanspan-idbackgroundbrokeredworkitemsspanbackground-brokered-work-items"></a><span id="Background_brokered_work_items"></span><span id="background_brokered_work_items"></span><span id="BACKGROUND_BROKERED_WORK_ITEMS"></span>仲介型バック グラウンド作業項目

UWP モバイル ブロード バンド アプリは、全画面表示で実行が、ユーザーは、フォア グラウンドでは、アプリケーションの対話にのみ必要です。 フォア グラウンド アプリは、このアプリは、システムのすべてのリソースを受け取るように、ユーザーに最も重要なと見なされます。 アプリがフォア グラウンドにない場合が中断され、任意のコードを実行することはできません。 ユーザーがフォア グラウンドにアプリを導入することで再開するまで、中断されているアプリが中断されたままです。 このモデルのアプリの動作では、遅延または重要でないバック グラウンド アプリの実行によって遅延が発生して、ユーザー エクスペリエンスは影響を受けることはありません。 さらに、レジューサーの不要なバック グラウンド アクティビティには、さまざまなフォーム ファクターのバッテリの寿命が最適化されます。 中断されているアプリの再開にかかった時間はごくわずかと、ほとんどのユーザーにほとんど重要ではなくになります。

Windows 10 では、アプリ タイル最新の状態も時に保持する、アプリが中断した Windows プッシュ通知を提供します。 可能であれば、Windows プッシュ通知を使用することをお勧めしているために、システムのパフォーマンスとデバイスのバッテリ寿命の延長のプッシュ通知が最適化されています。 中断されているアプリでは、その他の作業を行う独自のコードを実行する必要があります、バック グラウンド タスクを作成することができます。

フォア グラウンドで実行されていない場合、UWP アプリですべてのコードを実行することはできませんをシステム イベント ブローカーでは、アプリがバック グラウンドでは、イベントに応答コードを実行することができます。 アプリは、特定のバック グラウンドの仲介型イベントに応答するシステムのイベント ブローカーを作業項目を登録できます。 Windows は、仲介型バック グラウンド イベントは、アプリの現在の状態 (アクティブまたは保留) に関係なく、トリガーされたときに、アプリの作業項目を実行します。

一般に、バック グラウンド イベントは、簡単なトリガー ポイントとしてし、大量の処理を通知するものではありません。 そのため、アプリごとのクォータは、バック グラウンド イベントを許可されている処理時間に配置されます。 ネットワーク オペレーター API によって提供されるバック グラウンド イベントを含む、 [MobileOperatorNotification](mobile-operator-notification-event-technical-details.md)イベントと[HotspotAuthentication](handling-the-hotspot-authentication-event.md)イベント、重大なイベントとして Windows によって扱われます。 関連付けられている作業項目イベントの一般的な情報と比較して、バック グラウンド**MobileOperatorNotification**と**HotspotAuthentication**イベントの実行に関係なく、イベントのすべてのインスタンス、バック グラウンドの作業項目の各インスタンスは、処理時間のクォータの対象は、時間のクォータを処理します。 バック グラウンドのイベント ハンドラーで処理を制限し、モバイル ブロード バンド アプリへの大規模な処理を延期する必要があります。

## <a name="span-idinthissectionspanspan-idinthissectionspanspan-idinthissectionspanin-this-section"></a><span id="In_this_section"></span><span id="in_this_section"></span><span id="IN_THIS_SECTION"></span>このセクションの内容


-   [MobileOperatorNotification イベントを処理するアプリを開発します。](develop-an-app-to-handle-the-mobileoperatornotification-event.md)

-   [通信事業者通知イベントの技術的な詳細](mobile-operator-notification-event-technical-details.md)

-   [通信事業者の通知のシナリオ](mobile-operator-notification-scenarios.md)

 

 





