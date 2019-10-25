---
title: Storport イベント ログ拡張
description: Storport イベント ログ拡張
ms.assetid: 03b0bdef-cefa-4ad8-b9bf-a5f6b5f64cc6
ms.date: 06/13/2019
ms.localizationpriority: medium
ms.openlocfilehash: 71fdff09578d4c456f9f95e95e6051d64a0c1e98
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844475"
---
# <a name="storport-event-log-extensions"></a>Storport イベント ログ拡張

他の多くの種類のドライバーと同様に、Storport ミニポートドライバーは、接続された記憶装置の状態を管理者に通知するために、システムイベントログにエントリを作成する必要があります。 これらのイベントログエントリは、デバイスに関連するエラーに応答して作成されることがよくあります。 イベントは、テレメトリ、デバッグ、および最適化のためにログに記録することもできます。

Windows カーネル自体には、イベントログエントリを作成するための柔軟なインターフェイスが用意されていますが、Storport ミニポートモデルでは、ミニポートドライバーがこのインターフェイスに直接アクセスすることはできません。 代わりに、Storport はカーネルのシステムイベントログ機能のラッパーを提供し、ミニポートドライバーはラッパーを使用してイベントログエントリを作成します。

具体的には、Storport は次のイベントログルーチンを提供します。

* [**StorPortLogTelemetryEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportlogtelemetryex)を使用すると、ミニポートでカスタマイズされたデータを使用して、tracelogging メジャーまたはテレメトリイベントをログに記録できます (Windows 10 バージョン1903以降)。
* [**StorPortEtwChannelEvent2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportetwevent2)、 [**StorPortEtwChannelEvent4**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportetwevent4)、および[**StorPortEtwChannelEvent8**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportetwevent8)を使用すると、ミニポートでストレージトレースチャネル (Windows 10 バージョン1809以降) に ETW イベントを発行できます。
* [**Storportlogsystemevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportlogsystemevent)を使用すると、ミニポートでイベントログエントリ (Windows 7 以降) を作成できます。

Storport は、"**Microsoft-Windows-Storage-Storport**" プロバイダー名でイベントをログに記録します。 エラーは**運用**チャネルに記録され、デバッグ/分析は**診断**(**分析**および**デバッグ**) でログに記録されます。 *イベントビューアー*アプリケーションを使用する場合は、まず、**診断**チャネルを表示するように有効にする必要があります (有効にするには、[表示] をクリックし、[*分析ログとデバッグログの表示] >* をクリックします)。

 上記の関数は、Storport 拡張関数として実装されており、既存の拡張関数インターフェイスを使用してミニポートドライバーで使用できます。 拡張関数インターフェイスを使用すると、新しい関数への直接動的リンク参照が回避されます。 この直接参照を回避することで、新しい関数を使用するミニポートドライバーは、その関数をサポートしていないオペレーティングシステムで適切に読み込まれます。サポートされていない場合は、STOR_STATUS_NOT_IMPLEMENTED を返します。 このようにして、ベンダーは、サポートされている新しいイベントログ機能を利用して、複数の OS リリースで動作する単一のミニポートドライバーを作成できます。

**注:** Windows 7 より前のバージョンの Storport では、Storport のシステムイベントログインターフェイスである[**Storportlogerror**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportlogerror)を使用して、ミニポートドライバーが、ミニポートの有用性に影響を与えるカーネルのシステムイベントログ機能のごく一部にアクセスできるようにしました。イベントログエントリ。

Windows イベントに関する一般的な情報については、「 [Windows イベント](https://docs.microsoft.com/windows/desktop/Events/windows-events)」を参照してください。
