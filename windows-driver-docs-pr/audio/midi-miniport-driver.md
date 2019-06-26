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
ms.openlocfilehash: a018ddb93f1af9cd817067d2bc924bf8b3fec3f3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363239"
---
# <a name="midi-miniport-driver"></a>MIDI ミニポート ドライバー


## <span id="midi_miniport_driver"></span><span id="MIDI_MINIPORT_DRIVER"></span>


MIDI ミニポート ドライバーでは、ハードウェアのシーケンス処理とダウンロード可能なサウンド (DL) などの高度な機能のない単純な MIDI デバイスのハードウェアに依存する機能を管理します。 MIDI ポート ドライバーでは、シンセサイザーへ MIDI メッセージの配信のタイミングを処理します。 シンセサイザー ポート ドライバーからの要求に応答する MIDI メッセージの転送にのみ、MIDI ミニポート ドライバーが担当します。 MIDI の高度な機能を持つデバイスを使用する必要があります、 [Dmu ミニポート ドライバー](dmus-miniport-driver.md)代わりにします。

MIDI ミニポート ドライバーでは、2 つのインターフェイスを実装する必要があります。

-   *ミニポート インターフェイス*ミニポート オブジェクトを初期化し、MIDI ストリームを作成します。

-   *ストリーム インターフェイス*MIDI ストリームを管理し、ミニポート ドライバーの機能のほとんどを公開します。

ミニポート インターフェイス[IMiniportMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportmidi)でメソッドを継承、 [IMiniport](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiport)インターフェイス。 **IMiniportMidi**次の追加のメソッドを提供します。

[**IMiniportMidi::Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportmidi-init)

ミニポート オブジェクトを初期化します。

[**IMiniportMidi::NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportmidi-newstream)

新しいストリーム オブジェクトを作成します。

[**IMiniportMidi::Service**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportmidi-service)

サービスに対する要求のミニポート ドライバーに通知します。

ストリーム インターフェイス、 [IMiniportMidiStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportmidistream)でメソッドを継承、 **IUnknown**インターフェイス。 **IMiniportMidiStream**次の追加のメソッドを提供します。

[**IMiniportMidiStream::Read**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportmidistream-read)

読み取りは、MIDI キャプチャ デバイスからデータを入力します。

[**IMiniportMidiStream::SetFormat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportmidistream-setformat)

MIDI ストリームのデータ形式を設定します。

[**IMiniportMidiStream::SetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportmidistream-setstate)

MIDI ストリームの状態を設定します。

[**IMiniportMidiStream::Write**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportmidistream-write)

MIDI シンセサイザーへのデータを出力します。

MIDI ポート ドライバーは、双方向ですべてのタイミングの問題を処理し、オンとオフ、アダプターにポート ドライバーの呼び出しに応答を迅速にデータを移動するミニポート ドライバーに依存しています、 **IMiniportMidiStream**読み取りおよび書き込みメソッド。

PortCls には、FM シンセサイザーと UART 関数を持つ MIDI デバイス用の組み込みの MIDI ミニポート ドライバーが含まれています。 詳細については、次を参照してください。 [ **PcNewMiniport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcnewminiport)します。

 

 




