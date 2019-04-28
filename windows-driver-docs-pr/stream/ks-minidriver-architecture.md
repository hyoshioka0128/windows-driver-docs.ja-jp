---
title: KS のミニドライバー アーキテクチャ
description: KS のミニドライバー アーキテクチャ
ms.assetid: a9c17040-72a8-4290-831b-7fb46b00f532
keywords:
- カーネルのアーキテクチャ、WDK のストリーミング
- KS WDK、アーキテクチャ
- ストリーミング フィルター グラフ WDK カーネル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87a7e23238e8591b73542fba72108da94d028667
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380111"
---
# <a name="ks-minidriver-architecture"></a>KS のミニドライバー アーキテクチャ





カーネルのストリーミング サービスでは、ストリーミングされたデータのカーネル モードの処理をサポートします。 このモデルでフィルターと呼ばれる一連のブロックにグループ化されているノードをデータ フローのストリーミングします。 各フィルターは、データに実行するには、いくつか処理タスクをカプセル化します。 A [KS フィルター](ks-filters.md)はカーネル モードとして実装[**ドライバー\_オブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff544174)します。

ユーザー モードで DirectShow フィルターとして、プロキシを介して KS フィルターが表示されます。 そのため、グラフ ビルダーとユーザー モード アプリケーションは、KS フィルターと対話できます。 アクティブなグラフでは、カーネル モード コンポーネントも通信を直接ユーザー モードとカーネル モードの間の遷移のリソースを消費しているを排除します。

接続ポイントでフィルターとの間のデータ フローと呼ばれる[ピン](ks-pins.md)します。 暗証番号 (pin) のインスタンスは、レンダリングまたはデジタル オーディオなどのデータ ストリームをキャプチャします。

フィルターのグラフは、接続されているフィルターのグループです。 フィルターのグラフでは、ストリームに対して実行する複数の処理タスクをリンクします。 さまざまな操作をテストすることができます[グラフ構成をフィルター処理](filter-graph-examples.md)GraphEdit ツールを Microsoft Windows Driver Kit (WDK) を使用しています。 (GraphEdit の詳細については、次を参照してください、[フィルター グラフ エディター ツール](https://go.microsoft.com/fwlink/p/?linkid=9230)web サイトです。)。

サポートするドライバー[内蔵クロック](ks-clocks.md)ファイル オブジェクトとしてクロックを公開します。 ミニドライバーは[クロック時間を照会](https://msdn.microsoft.com/library/windows/hardware/ff566564)、または[**に通知を受け取る要求**](https://msdn.microsoft.com/library/windows/hardware/ff561764)時計が一定の時間に達したとき。

カスタムのメモリ管理インターフェイスをサポートするミニドライバーでは、このインターフェイスを公開と呼ばれるファイル オブジェクトとして、[アロケーター](ks-allocators.md)します。 たとえば、オンボード メモリを処理するデバイス マネージャーは、このようなインターフェイスを公開する可能性があります。 ミニドライバーは、割り当てし、メモリの割り当て解除に関連するファイル オブジェクトを使用できます。

このセクションには、次のトピックに関する追加情報が含まれています。

[KS フィルター](ks-filters.md)

[KS ピン](ks-pins.md)

[KS データ形式とデータの範囲](ks-data-formats-and-data-ranges.md)

[KS メディア](ks-mediums.md)

[KS インターフェイス](ks-interfaces.md)

[品質管理](quality-management.md)

 

 




