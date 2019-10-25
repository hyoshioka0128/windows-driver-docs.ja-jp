---
title: IMXF インターフェイス
description: IMXF インターフェイス
ms.assetid: 3782f812-bb95-4735-9635-e721ccda92b5
keywords:
- IMXF
- MIDI トランスポート WDK オーディオ
- wave シンク WDK オーディオ、MIDI トランスポート
- シンセサイザー WDK オーディオ、MIDI トランスポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2baafb72144c9d32c858ca4cf8f420506a72bb91
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833227"
---
# <a name="imxf-interfaces"></a>IMXF インターフェイス


## <span id="imxf_interfaces"></span><span id="IMXF_INTERFACES"></span>


DirectMusic ポートとミニポートドライバーのすべての MIDI トランスポートは、 [Imxf](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imxf)と同じインターフェイスを使用して実行されます。

**Imxf**は、DirectMusic MIDI 変換フィルターの COM インターフェイスです。 MIDI データを処理するポートドライバーのミニポートドライバー、sequencer、およびその他のエンティティは、共通の COM インターフェイスとして**Imxf**を使用します。 ミニポートドライバーは、このインターフェイスを実装するときに、MIDI トランスポートに参加できます。 PortCls に存在する[Iportdmus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iportdmus)は、 **imxf**を管理します。 キャプチャデバイスからキャプチャシンクへのインターフェイスは、 **Imxf**インターフェイスでもあります。

MIDI データは、パックされたタイムスタンプ付きデータのバッファーで、ユーザーモードとカーネルモードの間で転送されます。 カーネルポートドライバーは、これらのバッファーを個々のイベントに分割します (「 [**Dmus\_カーネル\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/ns-dmusicks-_dmus_kernel_event)」を参照してください)。 高解像度の MIDI sequencer は、トリガー時間が発生したときに、これらのイベントをミニポートドライバーに渡します。

入力側では、カーネルポートドライバーはミニポートドライバーから個々の入力メッセージを抽出し、ユーザーモードに渡すために、パックされたバッファーを構築します。 したがって、DirectMusic ミニポートドライバーのデータトランスポートモデルは、 [**Imxf::P utMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-imxf-putmessage)と[**IAllocatorMXF:: GetMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iallocatormxf-getmessage)で構成されます。

**Imxf**インターフェイスは、次のメソッドをサポートしています。

[**IMXF:: ConnectOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-imxf-connectoutput)

[**IMXF::D isconnectOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-imxf-disconnectoutput)

[**IMXF::P utMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-imxf-putmessage)

[**IMXF:: SetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-imxf-setstate)

[IAllocatorMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iallocatormxf)インターフェイスは、次のメソッドを追加することで、 **imxf**を拡張します。

[**IAllocatorMXF:: GetMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iallocatormxf-getmessage)

[**IAllocatorMXF:: GetBufferSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iallocatormxf-getbuffersize)

[**IAllocatorMXF:: GetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iallocatormxf-getbuffer)

[**IAllocatorMXF::P utBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iallocatormxf-putbuffer)

これらのインターフェイスの使用方法の詳細については、「[アロケーター](allocator.md)」を参照してください。

 

 




