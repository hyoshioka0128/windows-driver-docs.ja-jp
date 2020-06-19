---
title: メディアとカテゴリ
description: メディアとカテゴリ
ms.assetid: 2bc83ce6-7f79-44e7-a0fb-7b9f56771730
keywords:
- ビデオキャプチャ WDK AVStream、メディア
- ビデオのキャプチャ WDK AVStream、メディア
- ビデオキャプチャ WDK AVStream、ストリームカテゴリ
- ビデオのキャプチャ WDK AVStream、ストリームカテゴリ
- pin の主な目的を特定する
- ストリームカテゴリ WDK ビデオキャプチャ
- メディア WDK ビデオキャプチャ
- ピン接続の WDK ビデオキャプチャ
ms.date: 06/18/2020
ms.localizationpriority: medium
ms.openlocfilehash: 52bd0fa781a9cea025f5384253641053d4eeb8c5
ms.sourcegitcommit: 31fa7dbbcd051d7ec1ea3e05a4c0340af9d3b8a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2020
ms.locfileid: "85073433"
---
# <a name="mediums-and-categories"></a>メディアとカテゴリ

従来、Microsoft DirectShow ストリームは、[メディアの種類](https://docs.microsoft.com/previous-versions//ms787271(v=vs.85))によってのみ識別されていました。 単純なフィルターグラフのレンダリングには十分ですが、ハードウェアトポロジを反映する複雑なグラフやグラフでは、適切なグラフの作成に関する追加情報が必要です。 ピンを正しく識別して接続するためにフィルターグラフの作成を有効にするには、ビデオキャプチャミニドライバーは、そのピンが属するストリームカテゴリおよびメディアを指定します。

ストリームカテゴリは、pin の主要な目的を識別するためのメソッドです。 たとえば、キャプチャフィルターには、各ピンで同一の MediaTypes がサポートされている2つの出力ピンが存在する場合があります。 フィルターがいずれかのピンに優先順位を与える場合は、優先度の高い pin をキャプチャストリームカテゴリ (PINNAME \_ video capture) に割り当て、 \_ 優先度の低い pin をプレビューストリームカテゴリ (pinname \_ video preview) に割り当てることができ \_ ます。

メディアは、テレビチューナーフィルターのアナログオーディオ出力ピン (TV オーディオをサポートするため) や tv オーディオ入力ピン (テレビオーディオフィルター) の2つのピン間の接続を確保するための方法です。 メディアとは、1つのフィルターの出力ピンと別のフィルターの入力ピンの間のネットワークを識別する方法の1つです。

DirectShow graph builder のインターフェイスである**IFilterMapper2**および**Icap graphbuilder**では、これらのメソッドを使用して、メディアとストリームカテゴリの両方に基づいてフィルターグラフを作成します。
