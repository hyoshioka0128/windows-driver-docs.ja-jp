---
title: MIDI ミニポート ドライバー
description: MIDI ミニポート ドライバー
ms.assetid: 38aeba40-35da-4bfd-a8fe-cf8f7e96f286
keywords:
- オーディオミニポートドライバー WDK、MIDI
- ミニポートドライバー WDK オーディオ、MIDI
- MIDI ミニポートドライバー WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c87dec9b878ec5cf74abd4ca2d1aea9be055881
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830365"
---
# <a name="midi-miniport-driver"></a>MIDI ミニポート ドライバー


## <span id="midi_miniport_driver"></span><span id="MIDI_MINIPORT_DRIVER"></span>


MIDI ミニポートドライバーは、ハードウェアシーケンスやダウンロード可能なサウンド (DLS) などの高度な機能がないシンプルな MIDI デバイスのハードウェアに依存する機能を管理します。 MIDI ポートドライバーは、シンセサイザーへの MIDI メッセージ配信のタイミングを処理します。 MIDI ミニポートドライバーは、ポートドライバーからの要求に応答して、シンセサイザーへの MIDI メッセージの転送のみを行います。 高度な MIDI 機能を搭載したデバイスでは、代わりに[Dmus ミニポートドライバー](dmus-miniport-driver.md)を使用する必要があります。

MIDI ミニポートドライバーは、次の2つのインターフェイスを実装する必要があります。

-   *ミニポートインターフェイス*は、ミニポートオブジェクトを初期化し、MIDI ストリームを作成します。

-   *ストリームインターフェイス*は、MIDI ストリームを管理し、ほとんどのミニポートドライバーの機能を公開します。

ミニポートインターフェイス[IMiniportMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportmidi)は、 [IMiniport](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiport)インターフェイスのメソッドを継承します。 **IMiniportMidi**には、次の追加のメソッドが用意されています。

[**IMiniportMidi:: Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportmidi-init)

ミニポートオブジェクトを初期化します。

[**IMiniportMidi:: NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportmidi-newstream)

新しいストリームオブジェクトを作成します。

[**IMiniportMidi:: Service**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportmidi-service)

サービスの要求をミニポートドライバーに通知します。

ストリームインターフェイス[IMiniportMidiStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportmidistream)は、 **IUnknown**インターフェイスのメソッドを継承します。 **IMiniportMidiStream**には、次の追加のメソッドが用意されています。

[**IMiniportMidiStream:: Read**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportmidistream-read)

MIDI キャプチャデバイスから入力データを読み取ります。

[**IMiniportMidiStream:: SetFormat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportmidistream-setformat)

MIDI ストリームのデータ形式を設定します。

[**IMiniportMidiStream:: SetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportmidistream-setstate)

MIDI ストリームの状態を設定します。

[**IMiniportMidiStream:: Write**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportmidistream-write)

出力データを MIDI シンセサイザーに書き込みます。

MIDI ポートドライバーは、双方向のすべてのタイミングの問題を処理します。また、ポートドライバーによる**IMiniportMidiStream**の読み取りおよび書き込みメソッドの呼び出しに応答して、アダプターとの間でデータを迅速に移動するために、ミニポートドライバーに依存します。

PortCls には、FM シンセサイザーと UART の機能を備えた MIDI デバイス用の組み込みの MIDI ミニポートドライバーが含まれています。 詳細については、「 [**Pcnewminiport ポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewminiport)」を参照してください。

 

 




