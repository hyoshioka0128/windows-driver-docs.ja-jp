---
title: メディアとカテゴリ
description: メディアとカテゴリ
ms.assetid: 2bc83ce6-7f79-44e7-a0fb-7b9f56771730
keywords:
- ビデオ キャプチャ WDK AVStream、メディア
- ビデオの WDK AVStream、メディアのキャプチャ
- ビデオ キャプチャ WDK AVStream、ストリームのカテゴリ
- ビデオの WDK AVStream、ストリームのカテゴリのキャプチャ
- 暗証番号 (pin) の主な目的を識別します。
- ストリーム カテゴリ WDK ビデオのキャプチャします。
- メディアの WDK ビデオのキャプチャ
- 暗証番号 (pin) の接続の WDK ビデオ キャプチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1d88fb8020a0acfacd71709ac20d2e3f7c967e9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578496"
---
# <a name="mediums-and-categories"></a>メディアとカテゴリ


Microsoft DirectShow のストリームをによって識別されたがこれまでは、その[メディアの種類](https://go.microsoft.com/fwlink/p/?linkid=51458)します。 これは、単純なフィルター グラフを表示するための十分なより複雑なグラフとグラフ ハードウェア トポロジを反映する追加情報が必要グラフが正しく構築するため。 フィルター グラフの構築を正しく特定し、ピンを接続を有効にするのには、ビデオ キャプチャ ミニドライバーは、メディアと同様に、自分の pin が属するカテゴリをストリームを指定します。

Stream のカテゴリは、pin の主な目的を特定する方法です。 たとえば、キャプチャ フィルター各ピンでサポートされている同じ MediaTypes で 2 つの出力ピンことができます。 ピンの 1 つに、フィルターが優先順位を与える場合は、優先順位の高い暗証番号 (pin) をキャプチャのストリーム カテゴリに割り当てる可能性があります (PINNAME\_ビデオ\_キャプチャ)、およびプレビュー ストリーム カテゴリ (PINNAMEに優先順位の低いピン留め\_ビデオ\_プレビュー)。

メディアは、アナログのオーディオ出力ピン (サポートするテレビ オーディオ)、テレビ チューナー フィルターで、テレビのオーディオ入力ピン テレビ オーディオ フィルターでの個別のフィルターに 2 つの pin の間の接続を確立する方法です。 中規模の 1 つの方法は、1 つのフィルターの出力ピンと別のフィルターの入力ピンの間のネットワークを識別します。

DirectShow のグラフ ビルダー インターフェイス**IFilterMapper2**と**ICaptureGraphBuilder**メディアとストリームのカテゴリの両方に基づくフィルター グラフを作成するこれらのメソッドを使用します。

 

 




