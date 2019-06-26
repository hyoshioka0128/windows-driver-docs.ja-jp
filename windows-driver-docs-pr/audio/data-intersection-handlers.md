---
title: データ交差ハンドラー
description: データ交差ハンドラー
ms.assetid: 7206afdb-8a34-4b5a-8cea-87119f426161
keywords:
- WDM オーディオ ドライバー WDK、積集合のデータ ハンドラー
- オーディオ ドライバー WDK、積集合のデータ ハンドラー
- 交差部分のデータ ハンドラーの WDK オーディオ
- ハンドラーの WDK オーディオ
- WDK 仮想オーディオ デバイス
- オーディオは、データ交差ハンドラーのオーディオ、WDK をフィルター処理します。
- 交差部分のデータ ハンドラーのオーディオ、WDK をフィルター処理します。
- 交差部分のデータ ハンドラーのオーディオ、WDK を書式設定します。
- 交差部分のデータ ハンドラーのオーディオ、WDK をピン留め
- グラフの WDK オーディオ
- 範囲の交差部分を WDK オーディオ
- データの範囲は、オーディオの交差部分を WDK
- オーディオ データ形式 WDK
- WDK のオーディオ データ範囲
- ポート ドライバー WDK オーディオ、積集合のデータ ハンドラー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc0b8c35dc0eff3c941ce1665f1240148aa54613
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359093"
---
# <a name="data-intersection-handlers"></a>データ交差ハンドラー


## <span id="data_intersection_handlers"></span><span id="DATA_INTERSECTION_HANDLERS"></span>


このセクションでは、Microsoft Windows Driver Model (WDM) オーディオ ドライバーの交差部分のデータ ハンドラーについて説明します。 データ交差 KS の処理に関する幅広い議論については、一般にフィルターを参照してください[AVStream の交差部分を DataRange](https://docs.microsoft.com/windows-hardware/drivers/stream/data-range-intersections-in-avstream)します。

Windows XP などの Windows の旧バージョンで、 [SysAudio システム ドライバー](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)を構築します、[仮想のオーディオ デバイス](virtual-audio-devices.md)オーディオ フィルター ピンのペアをフォームに組み合わせることで、[オーディオ フィルターグラフ](audio-filter-graphs.md)します。 1 つのフィルターでソース pin は、別のシンクのピンに接続する、前に、SysAudio は 2 つの pin を使用してデータを交換する一般的な形式をネゴシエートする必要があります。 このネゴシエーションの詳細については、個別のフィルターで実装されているデータ交差ハンドラーに委任されます大きくします。

同様に、Windows Vista 以降で、オーディオ エンジンは、オーディオのレンダリング デバイスを表す wave フィルターの積集合のデータ ハンドラーを持つ共通ストリーム形式をネゴシエートする必要があります。

アダプターのドライバーでは、Portcls.sys からポートに対応するドライバーをミニポート ドライバーのいずれかのバインドによって、オーディオ デバイスの WaveRT フィルターを作成します。 ポート ドライバーには、既定の交差部分のデータ ハンドラーが含まれています。 既定のハンドラーが共通の形式を決定する最初のチャンス常に、ミニポート ドライバーの独自のデータの積集合のハンドラーに用意されています。 独自のハンドラーがこの機会を拒否する場合、ポート ドライバーの既定のハンドラーには、形式が決定します。

ポート ドライバーの既定の交差部分のデータ ハンドラーは、最も一般的なハードウェア機能を扱う設計されています。 オーディオ デバイスの単純な場合は、既定のハンドラーは、アダプターのドライバーで独自のハンドラーを実装する代わりに使用するを提供します。 ただしより高度な機能を持つアダプターが、ハードウェアのすべての機能を公開するために、独自のハンドラーが必要があります。

このセクションの残りの部分では、ポート ドライバーの既定の交差部分のデータ ハンドラーの制限事項について説明し、アダプター ドライバーが、独自のデータの積集合のハンドラーをデザインするために必要なテクニックが紹介します。 次のトピックについて説明します。

[データの積集合](data-intersection.md)

[既定の交差部分のデータ ハンドラー](default-data-intersection-handlers.md)

[独自のデータの積集合のハンドラー](proprietary-data-intersection-handlers.md)

[頻度のサンプルでハードウェアの制約](hardware-constraints-on-sample-frequency.md)

[出力バッファーのサイズ](output-buffer-size.md)

[離散値を含むデータ範囲](data-ranges-with-discrete-values.md)

[ワイルドカード](wild-cards.md)

[データ範囲のプロパティ](data-range-properties.md)



 

 




