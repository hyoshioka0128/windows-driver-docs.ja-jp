---
title: DMus ポート ドライバー
description: DMus ポート ドライバー
ms.assetid: 19828364-1b0d-4fc0-b142-9d776cbf1ada
keywords:
- DirectMusic WDK オーディオ、ポートドライバー
- DMus ポートドライバー WDK オーディオ
- PortCls WDK オーディオ、ポートドライバー
- オーディオミニポートドライバー WDK、ポートドライバー
- ミニポートドライバー WDK オーディオ、ポートドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40ec3ee54d3bf7c80013f7f25d7e60000411f9c2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833444"
---
# <a name="dmus-port-driver"></a>DMus ポート ドライバー


## <span id="dmus_port_driver"></span><span id="DMUS_PORT_DRIVER"></span>


DMus ポートドライバーは、Microsoft DirectMusic シンセサイザーまたはキャプチャデバイスを管理します。 MIDI ポートドライバーは、単純な MIDI デバイスのみをサポートしていますが、DMus ポートドライバーは、精度のあるシーケンサーのタイミング、ダウンロード可能なサウンド (DLS)、チャネルグループなどの高度な MIDI 機能を搭載したデバイスをサポートしています。 アダプタードライバーは、対応する[dmus ミニポートドライバー](dmus-miniport-driver.md)を実装します。これは、dmus ポートドライバーにバインドして、midi ストリームをレンダリングまたはキャプチャできる directmusic フィルター ( [Midi フィルターと directmusic フィルター](midi-and-directmusic-filters.md)を参照) を形成します。

DMus ポートドライバーは、ミニポートドライバーに[Iportdmus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iportdmus)インターフェイスを公開します。 **Iportdmus**は、基本インターフェイス[IPort](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iport)のメソッドを継承します。 **Iportdmus**には、次の追加のメソッドが用意されています。

[**IPortDMus:: Notify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iportdmus-notify)

MIDI シンセサイザーまたはキャプチャデバイスが MIDI ストリーム内の新しい位置に進んでいることをポートドライバーに通知します。

[**IPortDMus:: RegisterServiceGroup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iportdmus-registerservicegroup)

サービスグループオブジェクトをポートドライバーに登録します。
登録済みサービスグループには、ミニポートドライバーが**通知**を呼び出すときにポートドライバーによって呼び出される1つ以上のサービスルーチンの一覧が含まれています。詳細については、「[サービスシンクおよびサービスグループオブジェクト](service-sink-and-service-group-objects.md)」を参照してください。

また、DMus ポートドライバーは、各ストリームのメモリ[アロケーター](allocator.md)を作成し、アロケーターの[IAllocatorMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iallocatormxf)インターフェイスをミニポートドライバーのストリームオブジェクトに公開します。 **IAllocatorMXF**は、基本インターフェイス[imxf](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imxf)のメソッドを継承します。 **IAllocatorMXF**には、次の追加のメソッドが用意されています。

[**IAllocatorMXF:: GetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iallocatormxf-getbuffer)

[**Dmus\_カーネル\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/ns-dmusicks-_dmus_kernel_event)構造内に収まりきらない、MIDI イベントまたはイベントのリストのバッファーを取得します。

[**IAllocatorMXF:: GetBufferSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iallocatormxf-getbuffersize)

**GetBuffer**メソッドによって取得されるバッファーのサイズ (バイト単位) を取得します。

[**IAllocatorMXF:: GetMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iallocatormxf-getmessage)

種類が DMUS\_カーネル\_イベントの1つの構造体のストレージを格納するメッセージバッファーを取得します。

[**IAllocatorMXF::P utBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iallocatormxf-putbuffer)

使用しません。
DMus ポートとミニポートドライバーオブジェクトは、それぞれの**Iportdmus**インターフェイスと[IMiniportMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportmidi)インターフェイスを介して相互に通信します。 さらに、ポートドライバーは、 [Imxf](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imxf)インターフェイスを介してミニポートドライバーのストリームオブジェクトと通信します。また、ミニポートドライバーのストリームオブジェクトは、 **IAllocatorMXF**インターフェイスを介してポートドライバーのアロケーターと通信します。

DirectMusic のドライバーサポートの詳細については、「[シンセサイザーミニポートドライバーの概要](synthesizer-miniport-driver-overview.md)」を参照してください。

Windows XP 以降では、 **Iportdmus**インターフェイスと[iportmidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportmidi)インターフェイスの両方が1つの内部ドライバーモジュールに実装されています。 この統合は、この2つのインターフェイスの類似性によって促進されます。 たとえば、同じメソッドが両方のインターフェイスに対して定義されているとします。 以前のバージョンの Windows 用に作成されたアプリケーションでは、MIDI および DMus ポートドライバーを統合した結果として得られる**Iportmidi**および**Iportdmus**インターフェイスの動作が変更されていないことを確認できます。

 

 




