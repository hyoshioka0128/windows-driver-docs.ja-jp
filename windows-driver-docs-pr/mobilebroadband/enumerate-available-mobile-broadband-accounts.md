---
title: 利用可能なモバイル ブロード バンド アカウントを列挙します。
description: 利用可能なモバイル ブロード バンド アカウントを列挙します。
ms.assetid: 6dcf4789-09e8-43d2-9617-a026cbe0dfbb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7821be8edbb6231e7dd1301daa95ffcc9fc2301
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559277"
---
# <a name="enumerate-available-mobile-broadband-accounts"></a>利用可能なモバイル ブロード バンド アカウントを列挙します。


ネットワーク アカウントを列挙するために使用できる 2 つの方法があります: ポーリングやイベント ベースします。

-   **ポーリング**モバイル ブロード バンド アプリを静的なを使用して、使用可能なネットワーク アカウントのポーリング[ **MobileBroadbandAccount.AvailableNetworkAccountIds** ](https://msdn.microsoft.com/library/windows/apps/hh770608)メソッド。 これは、単に、アプリケーションは、アカウントのスナップショットを必要し、されているアカウントに、実行時に応答する必要はない場合に最適な追加または削除します。

-   **イベント ベース**を使用することができます、 [ **MobileBroadbandAccountWatcher** ](https://msdn.microsoft.com/library/windows/apps/hh770597)クラスを列挙し、モバイル ブロード バンド アカウントへの変更を監視します。 イベント ベースのメソッドは、アプリケーションが変更に応答する必要がある場合に最適です (つまり、戻るアカウントの選択 ページに、現在選択されているアカウントが削除されたときに)。 このクラスを使用する手順は次のとおりです。

    1.  インスタンスを作成、 [ **MobileBroadbandAccountWatcher** ](https://msdn.microsoft.com/library/windows/apps/hh770597)オブジェクト。

    2.  イベント ハンドラーを追加、 [ **AccountAdded**](https://msdn.microsoft.com/library/windows/apps/hh770599)、 [ **AccountRemoved**](https://msdn.microsoft.com/library/windows/apps/hh770600)、および[ **EnumerationCompleted** ](https://msdn.microsoft.com/library/windows/apps/hh770602)イベント。

    3.  ウォッチャーに Start() を呼び出します。

    [ **AccountAdded** ](https://msdn.microsoft.com/library/windows/apps/hh770599)既存のネットワーク アカウントごとにイベント ハンドラーが呼び出されます。 すべての既存のネットワーク アカウントが列挙されるとき、 [ **EnumerationCompleted** ](https://msdn.microsoft.com/library/windows/apps/hh770602)イベントが発生します。

    追加[ **AccountAdded** ](https://msdn.microsoft.com/library/windows/apps/hh770599)と[ **AccountRemoved** ](https://msdn.microsoft.com/library/windows/apps/hh770600)アカウントとしてのイベントの可用性と変更されます (つまり、モバイルブロード バンド ハードウェアまたは SIM は削除されます)。

**重要な**  アカウントの監視オブジェクトは自動的に、Windows によって、アプリが中断されたときに停止し、アプリケーションが再開されたときを再開します。 これは、大量のディスク アクティビティにイベントを処理するアプリの中断された再開および中断状態にすることにつながるために、バッテリの寿命を保持するために実行されます。 Stopped イベントは、監視を停止したときに発生します (これに当たります右側か前に、または、アプリの中断イベントの取得後に右)。 アプリの再開時、アプリが自動的に中断される前に実行されていたすべての監視を再起動、一連がトリガーされました[ **AccountAdded** ](https://msdn.microsoft.com/library/windows/apps/hh770599)が続くイベント、 [**EnumerationCompleted** ](https://msdn.microsoft.com/library/windows/apps/hh770602)イベント (同様に、まるで、 [**開始**](https://msdn.microsoft.com/library/windows/apps/hh770604)メソッドが呼び出された)。 これにより、中断された時間中に発生した何か重大な最新の状態を取得するアプリです。

[**MobileBroadbandAccountWatcher** ](https://msdn.microsoft.com/library/windows/apps/hh770597)オブジェクトは互いに依存しません。 つまり、すべてのイベントを報告する、イベントの – グループとしては、同じセットを報告するすべての監視に依存することはできません。 ただし、そのイベントがもう 1 つの監視によって使用されたため、特定の監視は、特定のイベントを報告しない場合があります。 相応の理由がある場合を除き、アプリごとの 1 つだけのアカウント監視オブジェクトを使用する必要があります。

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイル ブロード バンドの Windows ランタイム Api の一般的なタスク](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 






