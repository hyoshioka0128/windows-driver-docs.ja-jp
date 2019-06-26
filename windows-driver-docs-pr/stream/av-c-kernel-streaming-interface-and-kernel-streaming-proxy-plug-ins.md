---
title: AV/C カーネル インターフェイスとプロキシのプラグインのストリーミング
description: AV/C カーネル ストリーミングに関する情報を提供インターフェイスとカーネル ストリーミング プロキシ プラグイン
ms.assetid: 0831d917-5afc-4c0c-832a-c2b2669b8c22
keywords:
- カーネル ストリーミング インターフェイス WDK AV/C
- プロキシのカーネル ストリーミング プラグインを WDK AV/C
- AV/C WDK、カーネル ストリーミング プロキシ プラグイン
- AV/C WDK、カーネル ストリーミング インターフェイス
- プロキシ プラグイン WDK AV/C
- カーネル ストリーミング プロキシ WDK AVStream
- KS プロキシ WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3bc02eef75431bd795800b7e95c4b4c0384d839d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386761"
---
# <a name="avc-kernel-streaming-interface-and-kernel-streaming-proxy-plug-ins"></a>AV/C カーネル ストリーミング インターフェイスとカーネル ストリーミング プロキシ プラグイン



ベンダーは Stream クラス インターフェイスを使用している WDM ドライバーとしてピアまたは仮想のサブユニット ドライバーを記述する必要があります (ファイルに実装されているカーネル ストリーミング 1.0、 *Stream.sys*) または (カーネル Streaming 2.0、AVStream インターフェイスファイルに実装されている*Ks.sys*)。 ストリーム クラスのインターフェイスは廃止され、Microsoft はこれでさらに、開発を廃止 AVStream 好みのインターフェイスです。

いずれかのインターフェイスを使用するサブユニット ドライバーは、同じ AV/C 単位内であっても共存できます。 たとえば、サブユニット ドライバー AVStream を使用する場合、サブユニット ドライバーは、サブユニットの暗証番号 (pin) とフィルター記述子に対応する静的構造体をレイアウトします。 サブユニット ドライバーし登録 AVStream 呼び出すことによって、 [ **KsInitializeDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksinitializedriver) AVStream 関数。 両方のインターフェイスで使用される概念の詳細については、次を参照してください。[カーネル ストリーミング](kernel-streaming.md)します。 AVStream の詳細については、次を参照してください。 [AVStream の概要](avstream-overview.md)します。 Stream クラスの詳細については、次を参照してください。[ストリーミング ミニドライバー](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_stream/index)します。

カーネル ストリーミングのいずれかのインターフェイスは、アプリケーション制御のサブユニット ドライバーと対話に使用する同じ標準メカニズムを提供します。 アプリケーション レベルのサブユニットの AV/C を制御するための推奨される方法は Microsoft DirectShow フィルターとグラフをフィルターします。 DirectShow の (KS) プロキシ機能をストリーミングするカーネルが汎用フィルターを提供します (*ksproxy.ax*) できるように、サブユニットのプロパティを表す標準的な方法と、サブユニットがイベントを表す標準的な方法トリガーです。 AV/C サブユニットは、ドライバー、関連する KS プロパティとイベントをサポートするために必要なコードを実装します。 詳細については、サブユニット プロパティを表す、次を参照してください。[カーネル ストリーミング プロパティ セット](https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-property-sets)します。 詳細については、サブユニットのイベントを表す、次を参照してください。[ストリーミング イベントのセットのカーネル](https://docs.microsoft.com/windows-hardware/drivers/stream/kernel-streaming-event-sets)します。

プロキシ プラグイン、ベンダーまたは Microsoft によって提供されると、KS プロキシのフィルターを拡張できます。 KS プロキシのフィルターを拡張するには、KS プロパティとイベントのセットの低レベルの詳細を非表示にする COM インターフェイスが使用できます。 デバイスの INF ファイルで、サブユニットのドライバー プラグイン関連付けます。

プロパティとイベントに直接アクセスする一般的な方法では、使用可能なままを設定します。 **IAMExtTransport**インターフェイス (テープのサブユニットに使用)、プロキシ プラグインで実装されるインターフェイスの例に示します。 プラグインは、デバイスを制御ユーザー インターフェイスを提供するプロパティ ページとも含まれます。 エンドユーザーのデバイスの操作ではなく、テスト目的で、これらのプロパティ ページが通常使用されます。 GraphEdit または AMCap ユーティリティを使用して、KS、プラグインのプロパティをテストできます。 これらのユーティリティは、WDK と Windows SDK の両方に含まれます。

 





