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
ms.openlocfilehash: f11d78e2ea06e7b6455fa52031819a47209dd326
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332316"
---
# <a name="midi-port-driver"></a>MIDI ポート ドライバー


## <span id="midi_port_driver"></span><span id="MIDI_PORT_DRIVER"></span>


MIDI ポート ドライバーでは、MIDI シンセサイザーまたはキャプチャ デバイスを管理します。 アダプターのドライバーは、対応する[MIDI ミニポート ドライバー](midi-miniport-driver.md) MIDI フィルターを形成する、MIDI ポート ドライバー オブジェクトをバインドする (を参照してください[MIDI と DirectMusic フィルター](midi-and-directmusic-filters.md)) キャプチャまたは MIDI をレンダリングすることができますストリーム。

MIDI ポート ドライバーを公開、 [IPortMidi](https://msdn.microsoft.com/library/windows/hardware/ff536891)ミニポート ドライバーへのインターフェイス。 **IPortMidi**基底インターフェイスでメソッドを継承[IPort](https://msdn.microsoft.com/library/windows/hardware/ff536842)します。 **IPortMidi**次の追加のメソッドを提供します。

[**IPortMidi::Notify**](https://msdn.microsoft.com/library/windows/hardware/ff536893)

MIDI ストリーム内の新しい位置に、MIDI シンセサイザーまたはキャプチャ デバイスに高度なポート ドライバーに通知します。
[**IPortMidi::RegisterServiceGroup**](https://msdn.microsoft.com/library/windows/hardware/ff536895)

ポート ドライバーとサービスのグループ オブジェクトを登録します。
サービス グループは、ミニポート ドライバーを呼び出すときに呼び出されるは 1 つまたは複数のサービスのルーチンの一覧を含む**通知**; 詳細についてを参照してください[サービスがシンク オブジェクトとサービスのグループ オブジェクト](service-sink-and-service-group-objects.md)します。

MIDI ポートおよびミニポート ドライバー オブジェクトが、それぞれを互い通信**IPortMidi**と[IMiniportMidi](https://msdn.microsoft.com/library/windows/hardware/ff536703)インターフェイス。 ミニポート ドライバーは、ポート ドライバーの**IPortMidi**インターフェイスのハードウェアの割り込みポート ドライバーに通知します。 さらに、ポート ドライバーと通信を介して、ミニポート ドライバーのストリーム オブジェクト、 [IMiniportMidiStream](https://msdn.microsoft.com/library/windows/hardware/ff536704)インターフェイス。

Windows XP 以降では、 **IPortMidi**と[IPortDMus](https://msdn.microsoft.com/library/windows/hardware/ff536879)インターフェイスはいずれも 1 つの内部ドライバー モジュールに実装します。 この統合は、これら 2 つのインターフェイスの類似性によって促進されます。 たとえば、同じメソッドは、両方のインターフェイスに対して定義されます。 Windows の以前のバージョンが表示されないの動作の変更用に記述されたアプリケーション、 **IPortMidi**と**IPortDMus**インターフェイス MIDI と Dmu ポート ドライバーの統合に起因します。

 

 




