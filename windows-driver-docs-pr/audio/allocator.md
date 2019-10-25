---
title: アロケーター
description: アロケーター
ms.assetid: 8f263288-2f79-4f1d-b740-d78d40f47b32
keywords:
- MIDI トランスポート WDK オーディオ
- wave シンク WDK オーディオ、MIDI トランスポート
- シンセサイザー WDK オーディオ、MIDI トランスポート
- アロケーター WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9536af14fea3622e2852197ed6391ab53c9b8800
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831583"
---
# <a name="allocator"></a>アロケーター


## <span id="allocator"></span><span id="ALLOCATOR"></span>


アロケーターとの間のインターフェイスは、 [Imxf](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imxf)と[IAllocatorMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iallocatormxf)です。 これらのインターフェイスを使用すると、メモリの割り当てと解放を行わずに、 [**Dmus\_カーネル\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/ns-dmusicks-_dmus_kernel_event)構造体を再利用できます。 [**Imxf::P utMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-imxf-putmessage)はアロケーターに構造を与え、 [**IAllocatorMXF:: GetMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iallocatormxf-getmessage)は、新しくゼロになった dmus\_カーネル\_イベント構造をアロケーターから取得して再利用します。 (アロケーターは、空の DMUS\_カーネル\_イベント構造を使用して作成され、空になることはありません)。次の図に示すように、Irp (DMUS\_EVENTHEADER 構造体の形式) は、バイナリからに送られます。

![ポートとミニポートドライバーを使用した irp のフローを示す図](images/dmalloc.png)

バイナリは、 **IAllocatorMXF:: GetMessage**を呼び出して、空の[**DMUS\_カーネル\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/ns-dmusicks-_dmus_kernel_event)構造を取得します。 バイナリは、DMUS\_カーネル\_イベント構造体を IRP から取得し、これらの構造体 (MIDI イベントごとに1つ) を入力して、(MXF インターフェイスを使用して) sequencer に渡します。 Sequencer は、タイムスタンプに基づいてそれらを並べ替え、期限が切れたときに、 **Imxf::P utMessage**を呼び出してミニポートドライバーに渡します。 ミニポートドライバーは、DMUS\_カーネル\_イベント構造から MIDI データを取り出して、wave データにレンダリングできるようにします。 使用されている DMUS\_カーネル\_イベント構造体を、別の**Imxf::P utMessage**呼び出しと共にアロケーターに渡します。

キャプチャでは、逆の状況が発生します。 MIDI データはハードウェアからミニポートドライバーに送信され、ミニポートドライバーは**IAllocatorMXF:: GetMessage**を呼び出して、空の dmus\_カーネル\_イベント構造を取得します。 DMUS\_カーネル\_イベント構造には、タイムスタンプとデータが格納され、 **Imxf::P utMessage**を使用してキャプチャシンクに渡されます。 Dmus\_カーネル\_イベント構造で DMUS\_KEF\_イベント\_不完全フラグが設定されている場合、ミニポートドライバーは、構造体ごとに複数のメッセージを渡すことができます。 DMus ポートドライバーのキャプチャシンクは、この未加工のデータストリームを解析し、時間スタンプが付けられた MIDI メッセージ (構造体ごとに1つ) を含む\_カーネル\_イベント構造を出力します。

また、ミニポートドライバー自体が、タイムスタンプが付けられたメッセージをキャプチャシンクに出力することもできます。 この場合、dmus\_KERNEL\_イベントで、ドライバーは DMUS\_KEF\_イベント\_不完全なビットを設定しません。 キャプチャシンクは、タイムスタンプ付き構造を packer に直接渡します。これにより、メッセージが Irp にパッケージ化され、dmusic .dll に送信されます。 DirectMusic capture は、MIDI を記録するためだけのものです。 Wave 記録の場合は、DirectSound capture を使用します。

Packer は、DMUS\_カーネル\_イベント構造からデータを取得するときに、使用されている DMUS\_カーネル\_イベント構造を**Imxf::P utMessage**を使用してアロケーターに破棄します。 IRP バッファーがいっぱいになると、dmusic .dll に渡されます。 Packer は、空の Irp を dmusic .dll から受け取り、それらを入力して完了します。 Irp が多くなるほど、常に1つのデータを cloud ことができます。

 

 




