---
title: Wave と MIDI
description: Wave と MIDI
ms.assetid: 0c69ce48-ded0-44b8-9d34-20decb75058e
keywords:
- シンセサイザー WDK のオーディオ、MIDI ・ ウェーブの変換
- MIDI ・ ウェーブ変換 WDK オーディオ
- wave ストリーム WDK オーディオ
- カスタムのシンセサイザー WDK のオーディオ、MIDI ・ ウェーブの変換
- ユーザー モード シンセサイザー WDK のオーディオ、MIDI ・ ウェーブの変換
- wave MIDI に変換します。
- DirectMusic WDK のオーディオ、MIDI ・ ウェーブの変換
- ユーザー モードの WDK オーディオ、MIDI ・ ウェーブ変換でカスタムの表示
- DirectMusic カスタム レンダリング WDK のオーディオ、MIDI ・ ウェーブの変換
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b861dd4ac2c7ad1cd3c6c316d92b9d62415a6b60
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355351"
---
# <a name="midi-to-wave"></a>Wave と MIDI


## <span id="midi_to_wave"></span><span id="MIDI_TO_WAVE"></span>


シンセサイザーの主な作業は、2 つの手順で行われます。

-   MIDI メッセージを取得します。

-   Wave オーディオ ストリームにレンダリングされたノートの混在

このセクションは、一般的にこれを行う方法、ユーザー モードで、概念は、カーネル モードで同じでは基本的に詳細です。 参照してください[カーネル モードのハードウェアの高速化 DDI](kernel-mode-hardware-acceleration-ddi.md)カーネル モードのミニポート ドライバーを使用した同じ処理を実行する方法の詳細について。

ユーザー モードで呼び出して[ **IDirectMusicSynth::PlayBuffer** ](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-playbuffer) MIDI メッセージに再生できる状態がある場合。 呼び出し元のアプリケーションは、 **PlayBuffer**適切なタイミングで、タイムスタンプ、バッファー正しくと取得、[シンセサイザーの待機時間](synthesizer-latency.md)アカウントにします。 このメソッドの実装では、待機中のメッセージを取得し、内部形式には、バッファーが渡される参照時間に基づいている時間の設定に格納します。

Wave シンク呼び出し[ **IDirectMusicSynth::Render** ](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-render)たびにデータを受信する準備ができます。 たとえば、表示されたデータの保存先がセカンダリ DirectSound 場合バッファーの実装[ **IDirectMusicSynthSink::Activate** ](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-activate) DirectSound を待機するスレッドがセットアップする場合があります**PlayBuffer**通知します。 DirectSound DirectSound バッファーは、データを必要とする通知を呼び出し、スレッドの**レンダリング**へのポインターで渡し、 **IDirectSoundBuffer**オブジェクト (Microsoft Windows SDK で説明します。ドキュメント) および数とレンダリングされるサンプルの位置。

DirectSound バッファーが循環します。 バッファーの末尾に折り返しが発生したため、2 つの部分に分割されている、実質的に連続した領域の可能性が考慮する必要があります。 Wave シンクは、呼び出すことで、分割を処理する通常**レンダリング**2 回、1 回、DirectSound のロックされている部分の各部分をバッファーするように、**レンダリング**の連続したブロックを処理するメソッドがしかメモリ。 Wave シンク呼び出し**IDirectSoundBuffer::Lock** DirectSound バッファー、バッファー内のリージョンへの書き込みアクセス許可を要求するのです。 たとえば、次のシンクの呼び出しを wave**ロック**データ バッファーの末尾から 1 キロバイトの開始の 2 キロバイトにし、呼び出しをロック、バッファーとバッファーの先頭から別の 1 キロバイトの最後までの最後の 1 キロバイトです。 この場合、**ロック**実際には 2 つのポインターと対応する長さは、ロックされているバッファーの地域をまとめて説明を返します。 各ポインター連続メモリ ブロックをポイントすることが保証されます。

実装、**レンダリング**メソッドが必要な作業で取得される MIDI メッセージに応答を判断する**PlayBuffer**します。 *DwLength*への連続呼び出しのパラメーター値**レンダリング**メソッドは、サンプリング時間の追跡し、現在の表示期間の有効なメッセージで動作します。 注にメッセージが処理されるときに、メモは内部的に保存され、再度表示各パスでメソッドを対応するノート オフ メッセージが受信されるまでです。

 

 




