---
title: DMus ポート ドライバー
description: DMus ポート ドライバー
ms.assetid: 19828364-1b0d-4fc0-b142-9d776cbf1ada
keywords:
- DirectMusic WDK のオーディオ、ポートのドライバー
- Dmu ポート ドライバー WDK オーディオ
- PortCls WDK のオーディオ、ポートのドライバー
- オーディオのミニポート ドライバー WDK、ポート ドライバー
- ミニポート ドライバー WDK のオーディオ、ポートのドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8953a0132ad1c8acd0e20002d6b9623731798c3e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360113"
---
# <a name="dmus-port-driver"></a>DMus ポート ドライバー


## <span id="dmus_port_driver"></span><span id="DMUS_PORT_DRIVER"></span>


Dmu ポート ドライバーでは、Microsoft DirectMusic シンセサイザーまたはキャプチャ デバイスを管理します。 単純な MIDI デバイスのみをサポートしている、MIDI ポート ドライバーとは異なりは、Dmu のポート ドライバーは、有効桁数 sequencer のタイミング、ダウンロード可能なサウンド (DL) チャネル グループなどの高度な MIDI 機能を備えたデバイスをサポートします。 アダプター ドライバーでは、対応する[Dmu ミニポート ドライバー](dmus-miniport-driver.md) DirectMusic フィルターを形成する Dmu ポート ドライバーをバインドする (を参照してください[MIDI と DirectMusic フィルター](midi-and-directmusic-filters.md)) レンダリングまたは MIDI をキャプチャすることができますストリーム。

Dmu ポート ドライバーが公開、 [IPortDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-iportdmus)ミニポート ドライバーへのインターフェイス。 **IPortDMus**基底インターフェイスでメソッドを継承[IPort](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iport)します。 **IPortDMus**次の追加のメソッドを提供します。

[**IPortDMus::Notify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iportdmus-notify)

MIDI ストリーム内の新しい位置に、MIDI シンセサイザーまたはキャプチャ デバイスに高度なポート ドライバーに通知します。

[**IPortDMus::RegisterServiceGroup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iportdmus-registerservicegroup)

ポート ドライバーとサービスのグループ オブジェクトを登録します。
登録されているサービス グループは、ミニポート ドライバーを呼び出すときに、ポート ドライバーによって呼び出される 1 つまたは複数のサービス ルーチンの一覧を含む**通知**; 詳細についてを参照してください[サービスがシンク オブジェクトとサービスのグループ オブジェクト](service-sink-and-service-group-objects.md).

Dmu ポート ドライバーは、メモリも作成[アロケーター](allocator.md)各ストリームし、公開、アロケーターの[IAllocatorMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-iallocatormxf)ミニポート ドライバーのストリーム オブジェクトへのインターフェイス。 **IAllocatorMXF**基底インターフェイスでメソッドを継承[IMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-imxf)します。 **IAllocatorMXF**次の追加のメソッドを提供します。

[**IAllocatorMXF::GetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iallocatormxf-getbuffer)

MIDI イベントまたは大きすぎる内に収まるイベントの一覧のバッファーを取得、 [ **DMU\_カーネル\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/ns-dmusicks-_dmus_kernel_event)構造体。

[**IAllocatorMXF::GetBufferSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iallocatormxf-getbuffersize)

によって取得されたバッファーのバイト サイズを取得、 **GetBuffer**メソッド。

[**IAllocatorMXF::GetMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iallocatormxf-getmessage)

DMU の種類の 1 つの構造の記憶域を含むメッセージ バッファーを取得\_カーネル\_イベント。

[**IAllocatorMXF::PutBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iallocatormxf-putbuffer)

使用されていません。
Dmu のポートおよびミニポート ドライバー オブジェクトが、それぞれを互い通信**IPortDMus**と[IMiniportMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportmidi)インターフェイス。 さらに、ポート ドライバーと通信を介して、ミニポート ドライバーのストリーム オブジェクト、 [IMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-imxf)インターフェイス、およびストリーム オブジェクトのミニポート ドライバーの通信ポート ドライバーのアロケーターをその**IAllocatorMXF**インターフェイス。

DirectMusic のドライバー サポートについての詳細については、次を参照してください。[シンセサイザー ミニポート ドライバーの概要](synthesizer-miniport-driver-overview.md)します。

Windows XP 以降では、 **IPortDMus**と[IPortMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportmidi)インターフェイスはいずれも 1 つの内部ドライバー モジュールに実装します。 この統合は、これら 2 つのインターフェイスの類似性によって促進されます。 たとえば、同じメソッドは、両方のインターフェイスに対して定義されます。 Windows の以前のバージョンが表示されないの動作の変更用に記述されたアプリケーション、 **IPortMidi**と**IPortDMus**インターフェイス MIDI と Dmu ポート ドライバーの統合に起因します。

 

 




