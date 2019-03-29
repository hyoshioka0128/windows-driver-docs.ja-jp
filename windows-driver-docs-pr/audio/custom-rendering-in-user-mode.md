---
title: ユーザー モードでのカスタム レンダリング
description: ユーザー モードでのカスタム レンダリング
ms.assetid: a30c9eae-c3a9-4ff8-8e6c-d98c83f8596e
keywords:
- DirectMusic カスタム レンダリング WDK オーディオ
- DirectMusic カスタム レンダリング WDK オーディオ、ユーザー モードのカスタム レンダリングについて
- Microsoft ソフトウェアのシンセサイザー WDK オーディオ
- カスタムのシンセサイザー WDK オーディオ
- ユーザー モード シンセサイザー WDK オーディオ、カスタム
- ユーザー モードの WDK オーディオのレンダリングをカスタマイズします。
- wave シンク WDK オーディオ、ユーザー モードのカスタム表示
- DirectMusic WDK のオーディオ、カスタムのシンセサイザー
- ユーザー モードの WDK オーディオでは、カスタムの表示
- カスタム レンダリングについて、ユーザー モードの WDK オーディオでは、カスタムの表示
- DirectMusic WDK オーディオ、ユーザー モード
- 既定のシンセサイザー
- シンセサイザー WDK オーディオ、ユーザー モード カスタム レンダリング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31dee4bd93f88200ae1c5ccb23cefdc318f647b6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582384"
---
# <a name="custom-rendering-in-user-mode"></a>ユーザー モードでのカスタム レンダリング


## <span id="custom_rendering_in_user_mode"></span><span id="CUSTOM_RENDERING_IN_USER_MODE"></span>


シンセサイザーの Microsoft ソフトウェア DirectMusic インストールのユーザー モード コンポーネントは、ほとんどのシンセサイザー目的に適している必要があります。 DirectMusic は、その既定のシンセサイザーとしてこのコンポーネントを使用します。

さらに、DirectMusic を使用すると、独自のシンセサイザーのユーザー モード ソフトウェアを実装できます。 シンセサイザーは MIDI イベントから成る入力ストリームを受け取り、波形データを含む、出力ストリームを生成します。 通常、カスタム シンセサイザーでは、Microsoft DirectSound でストリームを再生する DirectMusic の組み込み wave シンクに、生成された wave ストリームをフィードします。 ただし、ユーザー モードの波は DirectSound 以外のデバイスに表示されるリダイレクト wave 出力する Microsoft DirectX 6.1 と 7、DirectMusic で使用できるように、カスタム シンクします。 ただし、カスタム wave シンクでは、必要なことはほとんどありません。 DirectX 8 以降では、DirectMusic はサポートされませんカスタム wave シンク。

DirectMusic シンセサイザーの最も重要なヘッダー ファイルは、dmusics.h (ユーザー モードのみ)、dmusicks.h (カーネル モードのみ)、dmusbuff.h、dmusprop.h です。

このセクションの残りの部分では、レンダリング プロセスのカスタマイズのさまざまな側面について説明します。 このセクションの例では、特記それ以外の場合を除くユーザーとカーネル モードの両方にある概念適用が、ユーザー モードの実装を想定しています。 次のトピックについて説明します。

[シンセサイザーと Wave シンク](synthesizers-and-wave-sinks.md)

[IDirectMusicSynth と IDirectMusicSynthSink](idirectmusicsynth-and-idirectmusicsynthsink.md)

[MIDI Wave は](midi-to-wave.md)

[シンセサイザーのタイミング](synthesizer-timing.md)

[DLS ダウンロードのサポート](dls-download-support.md)

[シンセサイザーの登録](registering-your-synthesizer.md)

 

 




