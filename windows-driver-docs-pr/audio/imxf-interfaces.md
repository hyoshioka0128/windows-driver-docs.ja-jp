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
ms.openlocfilehash: fa026692d15c9f50be0fc14929a4298326781444
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553103"
---
# <a name="imxf-interfaces"></a>IMXF インターフェイス


## <span id="imxf_interfaces"></span><span id="IMXF_INTERFACES"></span>


MIDI トランスポート DirectMusic ポートおよびミニポート ドライバーではすべては、同じインターフェイスを使用して実行されます。[IMXF](https://msdn.microsoft.com/library/windows/hardware/ff536782)します。

**IMXF** DirectMusic MIDI 変換のフィルターの COM インターフェイスです。 ミニポート ドライバー、シーケンサー、およびポート ドライバー MIDI データの使用を処理する他のエンティティ**IMXF**の一般的な COM インターフェイスとして。 ミニポート ドライバーは、このインターフェイスを実装すると、MIDI トランスポートに参加できます。 [IPortDMus](https://msdn.microsoft.com/library/windows/hardware/ff536879)、管理、PortCls に存在する**IMXF**します。 シンクをキャプチャするキャプチャ デバイスからのインターフェイスも、 **IMXF**インターフェイス。

MIDI データはユーザー モードとカーネル モード パックされたタイムスタンプ付きのデータのバッファーの間で転送されます。 カーネル ポート ドライバーは、個々 のイベントにこれらのバッファーを分割 (を参照してください[ **DMU\_カーネル\_イベント**](https://msdn.microsoft.com/library/windows/hardware/ff536340))。 高解像度、MIDI sequencer では、トリガーの時間が発生した場合、これらのイベントをミニポート ドライバーに渡します。

入力側では、カーネル ポート ドライバーは、ミニポート ドライバーから個々 の入力メッセージを抽出し、ユーザー モードに渡すようにするパックされたバッファーを構築します。 したがって、DirectMusic ミニポート ドライバーのデータ モデルはトランスポートから成る[ **IMXF::PutMessage** ](https://msdn.microsoft.com/library/windows/hardware/ff536791)と[ **IAllocatorMXF::GetMessage** ](https://msdn.microsoft.com/library/windows/hardware/ff536494).

**IMXF**インターフェイスは、次のメソッドをサポートしています。

[**IMXF::ConnectOutput**](https://msdn.microsoft.com/library/windows/hardware/ff536785)

[**IMXF::DisconnectOutput**](https://msdn.microsoft.com/library/windows/hardware/ff536787)

[**IMXF::PutMessage**](https://msdn.microsoft.com/library/windows/hardware/ff536791)

[**IMXF::SetState**](https://msdn.microsoft.com/library/windows/hardware/ff536792)

[IAllocatorMXF](https://msdn.microsoft.com/library/windows/hardware/ff536491)インターフェイスは、拡張**IMXF**次のメソッドを追加します。

[**IAllocatorMXF::GetMessage**](https://msdn.microsoft.com/library/windows/hardware/ff536494)

[**IAllocatorMXF::GetBufferSize**](https://msdn.microsoft.com/library/windows/hardware/ff536493)

[**IAllocatorMXF::GetBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536492)

[**IAllocatorMXF::PutBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536495)

これらのインターフェイスの使用に関する詳細については、次を参照してください。[アロケーター](allocator.md)します。

 

 




