---
title: MIDI ポート ドライバー
description: MIDI ポート ドライバー
ms.assetid: 4b403569-75c8-4cf4-bda1-efa9e004b529
keywords:
- MIDI ポートドライバー WDK オーディオ
- PortCls WDK オーディオ、ポートドライバー
- オーディオミニポートドライバー WDK、ポートドライバー
- ミニポートドライバー WDK オーディオ、ポートドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b804b06ef394e2d78bcb28c80b633c2fb78dbde
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830363"
---
# <a name="midi-port-driver"></a>MIDI ポート ドライバー


## <span id="midi_port_driver"></span><span id="MIDI_PORT_DRIVER"></span>


Midi ポートドライバーは、MIDI シンセサイザーまたはキャプチャデバイスを管理します。 アダプタードライバーは、midi ポートドライバーオブジェクトにバインドして midi フィルター (midi フィルター[と DirectMusic フィルター](midi-and-directmusic-filters.md)を参照) を形成し、midi ストリームをキャプチャまたはレンダリングできる、対応する[midi ミニポートドライバー](midi-miniport-driver.md)を提供します。

MIDI ポートドライバーは、ミニポートドライバーに[Iportmidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportmidi)インターフェイスを公開します。 **Iportmidi**は、基本インターフェイス[IPort](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iport)のメソッドを継承します。 **Iportmidi**には、次の追加のメソッドが用意されています。

[**IPortMidi:: Notify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportmidi-notify)

MIDI シンセサイザーまたはキャプチャデバイスが MIDI ストリーム内の新しい位置に進んでいることをポートドライバーに通知します。
[**IPortMidi:: RegisterServiceGroup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportmidi-registerservicegroup)

サービスグループオブジェクトをポートドライバーに登録します。
サービスグループには、ミニポートドライバーが**通知**を呼び出すときに呼び出される1つ以上のサービスルーチンの一覧が含まれています。詳細については、「[サービスシンクおよびサービスグループオブジェクト](service-sink-and-service-group-objects.md)」を参照してください。

MIDI ポートとミニポートドライバーオブジェクトは、それぞれの**Iportmidi**および[IMiniportMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportmidi)インターフェイスを介して相互に通信します。 ミニポートドライバーは、ポートドライバーの**Iportmidi**インターフェイスを使用して、ハードウェア割り込みのポートドライバーに通知します。 さらに、ポートドライバーは、 [IMiniportMidiStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportmidistream)インターフェイスを介してミニポートドライバーのストリームオブジェクトと通信します。

Windows XP 以降では、 **Iportmidi**インターフェイスと[Iportdmus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iportdmus)インターフェイスの両方が1つの内部ドライバーモジュールに実装されています。 この統合は、この2つのインターフェイスの類似性によって促進されます。 たとえば、同じメソッドが両方のインターフェイスに対して定義されているとします。 以前のバージョンの Windows 用に作成されたアプリケーションでは、MIDI および DMus ポートドライバーを統合した結果として得られる**Iportmidi**および**Iportdmus**インターフェイスの動作が変更されていないことを確認できます。

 

 




