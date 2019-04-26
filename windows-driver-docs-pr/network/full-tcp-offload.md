---
title: 完全な TCP オフロード
description: 完全な TCP オフロード
ms.assetid: a940617a-b848-430d-8da1-acd946feba1b
keywords:
- TCP オフロード WDK ネットワーク
- chimney オフロード WDK ネットワーク完全
- WDK ネットワークの処理をオフロードします。
- 完全な TCP オフロード WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a588b090ccadb36e2adca78c4124a38ead0d7b5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349995"
---
# <a name="full-tcp-offload"></a>完全な TCP オフロード





NDIS 6.0 には、完全な TCP オフロードするためのアーキテクチャが導入されました。 このアーキテクチャと呼ばれる「chimney オフロード」アーキテクチャ"chimney"と呼ばれる、直接接続を提供するためのアプリケーションとオフロード対応の NIC 間 Chimney は、TCP プロトコルの状態を維持するなど、オフロードされた接続の処理を実行する NIC を使用できます。

Chimney オフロードのアーキテクチャでは、ネットワーク集中型アプリケーションのホスト ネットワークの処理を軽減します。 これにより、ネットワークのアプリケーションをエンド ツー エンドの待機時間を軽減しながらより効率的にスケールできます。 少数のサーバーは、アプリケーションをホストするために必要なし、サーバーは、完全なイーサネット帯域幅を使用することができます。

TCP chimney は、すべての TCP が 1 つまたは複数の TCP 接続の処理をオフロードします。 プライマリのパフォーマンスの向上は、セグメント化と再編成 (行政区) オフロードにより、信頼性の高い接続 (たとえば、確認の処理および TCP 再転送タイマー) 処理と削減の割り込みの読み込みをオフロードから取得されます。

**注**  Windows Vista オペレーティング システムは引き続き以前のバージョンのオペレーティング システムで使用できる個々 の TCP タスク オフロードをサポートします。 を通じて、chimney オフロードされがない接続では、これらのタスクをオフロードすることができます。 オフロード対応の NIC が両方 chimney オフロードをサポートする必要があり、タスクの負荷を軽減します。 このような NIC は、最高レベルのオフロードの最適化を提供します。

 

TCP chimney オフロード NDIS 6.0 以降では、次を参照してください。 [NDIS TCP Chimney オフロード](https://docs.microsoft.com/previous-versions/windows/hardware/network/ndis-tcp-chimney-offload)します。

 

 





