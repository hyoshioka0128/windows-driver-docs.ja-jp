---
title: Storport イベント ログ拡張
description: Storport イベント ログ拡張
ms.assetid: 03b0bdef-cefa-4ad8-b9bf-a5f6b5f64cc6
ms.date: 06/13/2019
ms.localizationpriority: medium
ms.openlocfilehash: f76a6a314679a3bd06f1fb41218b9894f669104f
ms.sourcegitcommit: e8b8c40d00a452793582f2729207b7d51bd89952
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/14/2019
ms.locfileid: "67133890"
---
# <a name="storport-event-log-extensions"></a>Storport イベント ログ拡張

などの他の多くの種類のドライバーでは、Storport ミニポート ドライバーでは、管理者が接続された記憶域デバイスの状態の情報を保持するシステム イベント ログにエントリを作成する必要があります。 これらのイベント ログ エントリは、デバイス関連の障害への応答で多くの場合、作成されます。 イベントは、製品利用統計情報、デバッグ、および最適化にも記録されます。

Windows カーネル自体は、イベント ログ エントリを作成するための柔軟なインターフェイスを提供します、Storport ミニポート モデル ミニポート ドライバーにそのインターフェイスに直接アクセスを許可しません。 代わりに、Storport、カーネルのシステム イベント ログの機能、ラッパーを提供して、ミニポート ドライバーでは、ラッパーを使用して、イベント ログ エントリを作成します。

具体的には、Storport は、次のイベント ログのルーチンを提供します。

* [**StorPortLogTelemetryEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportlogtelemetryex)ミニポート、tracelogging 測定ログまたはミニポートにカスタマイズされたデータ (Windows 10 バージョンが 1903 以降) のテレメトリ イベントを使用します。
* [**StorPortEtwChannelEvent2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportetwevent2)、 [ **StorPortEtwChannelEvent4**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportetwevent4)、および[ **StorPortEtwChannelEvent8** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportetwevent8)ミニポート ストレージ トレース チャネル (Windows 10 は 1809 以降のバージョン) に ETW イベントを発行できるようにします。
* [**StorPortLogSystemEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportlogsystemevent) miniports (Windows 7 以降) イベント ログ エントリを作成できます。

Storport の下のイベントを記録する、"**Microsoft Windows 記憶域 Storport**"プロバイダーの名前。 エラーがログ記録、 **Operational**チャネル、およびデバッグ/分析をログイン**診断**(**分析**と**デバッグ**)。 使用する場合、*イベント ビューアー*アプリケーション、する必要がありますまず有効にする、**診断**表示するためのチャネル (を有効にする] をクリックして*ビューでは、[分析およびデバッグ ログ]-> [* )。

 上記の関数は、Storport の機能を拡張として実装され、既存の拡張機能インターフェイスを使用して、ミニポート ドライバーを利用できます。 拡張機能インターフェイスの使用は、新しい関数への直接の動的リンク参照を回避できます。 その直接の参照を回避するには、新しい関数を使用するミニポート ドライバーはサポートされていない場合、STOR_STATUS_NOT_IMPLEMENTED を返す関数で、関数をサポートしないオペレーティング システムで正しく読み込ま。 この方法で、ベンダーは、特定の活用新しいイベントのログ記録機能がサポートされている複数の OS のリリースで実行されている 1 つのミニポート ドライバーを作成できます。

**注:** バージョンの Windows 7、Storport のシステム イベント ログのインターフェイスよりも前の Storport [ **StorPortLogError**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportlogerror)カーネルのシステム イベントの機能のごくわずかであるにミニポート ドライバーへのアクセスを付与ログ機能: ミニポート イベント ログ エントリの有用性に影響を与えます。

Windows イベントの詳細については、次を参照してください。 [Windows イベント](https://docs.microsoft.com/windows/desktop/Events/windows-events)します。
