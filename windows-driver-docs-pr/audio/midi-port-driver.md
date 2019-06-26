---
title: MIDI ポート ドライバー
description: MIDI ポート ドライバー
ms.assetid: 4b403569-75c8-4cf4-bda1-efa9e004b529
keywords:
- MIDI ポート ドライバー WDK オーディオ
- PortCls WDK のオーディオ、ポートのドライバー
- オーディオのミニポート ドライバー WDK、ポート ドライバー
- ミニポート ドライバー WDK のオーディオ、ポートのドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b0ffa0ef538ca8e018427cfc2dd9125dc934cb6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363244"
---
# <a name="midi-port-driver"></a>MIDI ポート ドライバー


## <span id="midi_port_driver"></span><span id="MIDI_PORT_DRIVER"></span>


MIDI ポート ドライバーでは、MIDI シンセサイザーまたはキャプチャ デバイスを管理します。 アダプターのドライバーは、対応する[MIDI ミニポート ドライバー](midi-miniport-driver.md) MIDI フィルターを形成する、MIDI ポート ドライバー オブジェクトをバインドする (を参照してください[MIDI と DirectMusic フィルター](midi-and-directmusic-filters.md)) キャプチャまたは MIDI をレンダリングすることができますストリーム。

MIDI ポート ドライバーを公開、 [IPortMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportmidi)ミニポート ドライバーへのインターフェイス。 **IPortMidi**基底インターフェイスでメソッドを継承[IPort](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iport)します。 **IPortMidi**次の追加のメソッドを提供します。

[**IPortMidi::Notify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportmidi-notify)

MIDI ストリーム内の新しい位置に、MIDI シンセサイザーまたはキャプチャ デバイスに高度なポート ドライバーに通知します。
[**IPortMidi::RegisterServiceGroup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportmidi-registerservicegroup)

ポート ドライバーとサービスのグループ オブジェクトを登録します。
サービス グループは、ミニポート ドライバーを呼び出すときに呼び出されるは 1 つまたは複数のサービスのルーチンの一覧を含む**通知**; 詳細についてを参照してください[サービスがシンク オブジェクトとサービスのグループ オブジェクト](service-sink-and-service-group-objects.md)します。

MIDI ポートおよびミニポート ドライバー オブジェクトが、それぞれを互い通信**IPortMidi**と[IMiniportMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportmidi)インターフェイス。 ミニポート ドライバーは、ポート ドライバーの**IPortMidi**インターフェイスのハードウェアの割り込みポート ドライバーに通知します。 さらに、ポート ドライバーと通信を介して、ミニポート ドライバーのストリーム オブジェクト、 [IMiniportMidiStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportmidistream)インターフェイス。

Windows XP 以降では、 **IPortMidi**と[IPortDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-iportdmus)インターフェイスはいずれも 1 つの内部ドライバー モジュールに実装します。 この統合は、これら 2 つのインターフェイスの類似性によって促進されます。 たとえば、同じメソッドは、両方のインターフェイスに対して定義されます。 Windows の以前のバージョンが表示されないの動作の変更用に記述されたアプリケーション、 **IPortMidi**と**IPortDMus**インターフェイス MIDI と Dmu ポート ドライバーの統合に起因します。

 

 




