---
title: MIDI ミニポート ドライバー
description: MIDI ミニポート ドライバー
ms.assetid: 38aeba40-35da-4bfd-a8fe-cf8f7e96f286
keywords:
- オーディオのミニポート ドライバー WDK、MIDI
- ミニポート ドライバー WDK オーディオ、MIDI
- MIDI ミニポート ドライバー WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8fb8fc53526cdfa404ae409321301ee2fde5b0bb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332327"
---
# <a name="midi-miniport-driver"></a>MIDI ミニポート ドライバー


## <span id="midi_miniport_driver"></span><span id="MIDI_MINIPORT_DRIVER"></span>


MIDI ミニポート ドライバーでは、ハードウェアのシーケンス処理とダウンロード可能なサウンド (DL) などの高度な機能のない単純な MIDI デバイスのハードウェアに依存する機能を管理します。 MIDI ポート ドライバーでは、シンセサイザーへ MIDI メッセージの配信のタイミングを処理します。 シンセサイザー ポート ドライバーからの要求に応答する MIDI メッセージの転送にのみ、MIDI ミニポート ドライバーが担当します。 MIDI の高度な機能を持つデバイスを使用する必要があります、 [Dmu ミニポート ドライバー](dmus-miniport-driver.md)代わりにします。

MIDI ミニポート ドライバーでは、2 つのインターフェイスを実装する必要があります。

-   *ミニポート インターフェイス*ミニポート オブジェクトを初期化し、MIDI ストリームを作成します。

-   *ストリーム インターフェイス*MIDI ストリームを管理し、ミニポート ドライバーの機能のほとんどを公開します。

ミニポート インターフェイス[IMiniportMidi](https://msdn.microsoft.com/library/windows/hardware/ff536703)でメソッドを継承、 [IMiniport](https://msdn.microsoft.com/library/windows/hardware/ff536698)インターフェイス。 **IMiniportMidi**次の追加のメソッドを提供します。

[**IMiniportMidi::Init**](https://msdn.microsoft.com/library/windows/hardware/ff536709)

ミニポート オブジェクトを初期化します。

[**IMiniportMidi::NewStream**](https://msdn.microsoft.com/library/windows/hardware/ff536710)

新しいストリーム オブジェクトを作成します。

[**IMiniportMidi::Service**](https://msdn.microsoft.com/library/windows/hardware/ff536711)

サービスに対する要求のミニポート ドライバーに通知します。

ストリーム インターフェイス、 [IMiniportMidiStream](https://msdn.microsoft.com/library/windows/hardware/ff536704)でメソッドを継承、 **IUnknown**インターフェイス。 **IMiniportMidiStream**次の追加のメソッドを提供します。

[**IMiniportMidiStream::Read**](https://msdn.microsoft.com/library/windows/hardware/ff536705)

読み取りは、MIDI キャプチャ デバイスからデータを入力します。

[**IMiniportMidiStream::SetFormat**](https://msdn.microsoft.com/library/windows/hardware/ff536706)

MIDI ストリームのデータ形式を設定します。

[**IMiniportMidiStream::SetState**](https://msdn.microsoft.com/library/windows/hardware/ff536707)

MIDI ストリームの状態を設定します。

[**IMiniportMidiStream::Write**](https://msdn.microsoft.com/library/windows/hardware/ff536708)

MIDI シンセサイザーへのデータを出力します。

MIDI ポート ドライバーは、双方向ですべてのタイミングの問題を処理し、オンとオフ、アダプターにポート ドライバーの呼び出しに応答を迅速にデータを移動するミニポート ドライバーに依存しています、 **IMiniportMidiStream**読み取りおよび書き込みメソッド。

PortCls には、FM シンセサイザーと UART 関数を持つ MIDI デバイス用の組み込みの MIDI ミニポート ドライバーが含まれています。 詳細については、次を参照してください。 [ **PcNewMiniport**](https://msdn.microsoft.com/library/windows/hardware/ff537714)します。

 

 




