---
title: IMXF インターフェイス
description: IMXF インターフェイス
ms.assetid: 3782f812-bb95-4735-9635-e721ccda92b5
keywords:
- IMXF
- MIDI トランスポート WDK オーディオ
- wave オーディオ、MIDI トランスポートの WDK をシンクします。
- シンセサイザー WDK オーディオ、MIDI トランスポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7989fe5ac93cde4b31742e467ab0c63b31cdc64d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359905"
---
# <a name="imxf-interfaces"></a>IMXF インターフェイス


## <span id="imxf_interfaces"></span><span id="IMXF_INTERFACES"></span>


MIDI トランスポート DirectMusic ポートおよびミニポート ドライバーではすべては、同じインターフェイスを使用して実行されます。[IMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-imxf)します。

**IMXF** DirectMusic MIDI 変換のフィルターの COM インターフェイスです。 ミニポート ドライバー、シーケンサー、およびポート ドライバー MIDI データの使用を処理する他のエンティティ**IMXF**の一般的な COM インターフェイスとして。 ミニポート ドライバーは、このインターフェイスを実装すると、MIDI トランスポートに参加できます。 [IPortDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-iportdmus)、管理、PortCls に存在する**IMXF**します。 シンクをキャプチャするキャプチャ デバイスからのインターフェイスも、 **IMXF**インターフェイス。

MIDI データはユーザー モードとカーネル モード パックされたタイムスタンプ付きのデータのバッファーの間で転送されます。 カーネル ポート ドライバーは、個々 のイベントにこれらのバッファーを分割 (を参照してください[ **DMU\_カーネル\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/ns-dmusicks-_dmus_kernel_event))。 高解像度、MIDI sequencer では、トリガーの時間が発生した場合、これらのイベントをミニポート ドライバーに渡します。

入力側では、カーネル ポート ドライバーは、ミニポート ドライバーから個々 の入力メッセージを抽出し、ユーザー モードに渡すようにするパックされたバッファーを構築します。 したがって、DirectMusic ミニポート ドライバーのデータ モデルはトランスポートから成る[ **IMXF::PutMessage** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-imxf-putmessage)と[ **IAllocatorMXF::GetMessage** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iallocatormxf-getmessage).

**IMXF**インターフェイスは、次のメソッドをサポートしています。

[**IMXF::ConnectOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-imxf-connectoutput)

[**IMXF::DisconnectOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-imxf-disconnectoutput)

[**IMXF::PutMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-imxf-putmessage)

[**IMXF::SetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-imxf-setstate)

[IAllocatorMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-iallocatormxf)インターフェイスは、拡張**IMXF**次のメソッドを追加します。

[**IAllocatorMXF::GetMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iallocatormxf-getmessage)

[**IAllocatorMXF::GetBufferSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iallocatormxf-getbuffersize)

[**IAllocatorMXF::GetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iallocatormxf-getbuffer)

[**IAllocatorMXF::PutBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iallocatormxf-putbuffer)

これらのインターフェイスの使用に関する詳細については、次を参照してください。[アロケーター](allocator.md)します。

 

 




