---
title: AV/C カーネルインターフェイスとストリーミングプロキシプラグイン
description: AV/C カーネルストリームインターフェイスとカーネルストリーミングプロキシプラグインに関する情報を提供します。
ms.assetid: 0831d917-5afc-4c0c-832a-c2b2669b8c22
keywords:
- カーネルストリーミングインターフェイス WDK AV/C
- カーネルストリーミングプロキシプラグイン (WDK AV/C)
- AV/C WDK、カーネルストリーミングプロキシプラグイン
- AV/C WDK、カーネルストリーミングインターフェイス
- プロキシプラグイン WDK AV/C
- カーネルストリーミングプロキシ WDK AVStream
- KS プロキシ WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5cc33372dfec78326972d926dd7b19d7d119b617
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843359"
---
# <a name="avc-kernel-streaming-interface-and-kernel-streaming-proxy-plug-ins"></a>AV/C カーネルストリームインターフェイスとカーネルストリーミングプロキシプラグイン



ベンダーは、ストリームクラスインターフェイス (ファイルの .sys で実装されている Kernel Streaming 1.0) または AVStream インターフェイス (カーネルストリーミング 2.0) を使用する WDM ドライバー (または、実装されている) を使用する WDM ドライバーとして、ピアまたは仮想サブユニットドライバーを書き込む必要があります *。* ファイルを*Ks*) にします。 ストリームクラスのインターフェイスは互換性のために残されているため、AVStream は推奨インターフェイスです。

いずれかのインターフェイスを使用するサブユニットドライバーは、同じ AV/C ユニット内であっても共存できます。 たとえば、サブユニットドライバーが AVStream を使用している場合、サブユニットドライバーは、サブユニットのピンとフィルター記述子に対応する静的構造をレイアウトします。 次に、サブユニットドライバーは、 [**Ksinitializedriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksinitializedriver) avstream 関数を呼び出して avstream に登録します。 両方のインターフェイスで使用される概念の詳細については、「[カーネルストリーミング](kernel-streaming.md)」を参照してください。 AVStream の詳細については、「 [Avstream の概要](avstream-overview.md)」を参照してください。 Stream クラスの詳細については、「 [Streaming ミニドライバー](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)」を参照してください。

カーネルストリーミングインターフェイスには、アプリケーションがサブユニットドライバーを操作および制御するために使用するのと同じ標準メカニズムが用意されています。 アプリケーションレベルで AV/C サブユニットを制御するために推奨される方法は、Microsoft DirectShow フィルターとフィルターグラフを使用することです。 DirectShow の kernel streaming (KS) プロキシメカニズムには汎用的なフィルター (*ksproxy.ax*) が用意されています。これを使用すると、サブユニットのプロパティを標準の方法で表すことができ、サブユニットがトリガーする可能性のあるイベントを表すことができます。 AV/C サブユニットドライバーで、関連する KS プロパティとイベントをサポートするために必要なコードを実装します。 サブユニットのプロパティの表現の詳細については、「[カーネルストリーミングのプロパティセット](https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-property-sets)」を参照してください。 サブユニットイベントの表現の詳細については、「[カーネルストリーミングイベントセット](https://docs.microsoft.com/windows-hardware/drivers/stream/kernel-streaming-event-sets)」を参照してください。

KS プロキシフィルターは、Microsoft またはベンダーによって提供されるプロキシプラグインを使用して拡張できます。 KS プロキシフィルターを拡張すると、COM インターフェイスは、KS プロパティとイベントセットの下位レベルの詳細を非表示にすることができます。 プラグインは、デバイスの INF ファイルのサブユニットドライバーに関連付けられています。

プロパティとイベントセットに直接アクセスする一般的な方法は、引き続き使用できます。 (Tape サブユニットに使用される) **Iamexttransport**インターフェイスは、プロキシプラグインで実装されるインターフェイスの一例です。 プラグインには、デバイスを制御するためのユーザーインターフェイスを提供するプロパティページを含めることもできます。 これらのプロパティページは、通常、エンドユーザーのデバイスの操作ではなく、テスト目的で使用されます。 GraphEdit または AMCap ユーティリティを使用して、プラグインの KS プロパティをテストできます。 これらのユーティリティは、WDK と Windows SDK の両方に含まれています。

 





