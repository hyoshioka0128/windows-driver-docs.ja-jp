---
title: アロケーター
description: アロケーター
ms.assetid: 8f263288-2f79-4f1d-b740-d78d40f47b32
keywords:
- MIDI トランスポート WDK オーディオ
- wave オーディオ、MIDI トランスポートの WDK をシンクします。
- シンセサイザー WDK オーディオ、MIDI トランスポート
- アロケーター WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04494c700050578df176a55e52db5445a2854823
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355778"
---
# <a name="allocator"></a>アロケーター


## <span id="allocator"></span><span id="ALLOCATOR"></span>


アロケーターの間のインターフェイスは[IMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-imxf)と[IAllocatorMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-iallocatormxf)します。 これらのインターフェイスでは、再利用できます。 [ **DMU\_カーネル\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/ns-dmusicks-_dmus_kernel_event)の割り当てとメモリを解放せずに構造体。 [**IMXF::PutMessage** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-imxf-putmessage)アロケーターへの構造体を提供し、 [ **IAllocatorMXF::GetMessage** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iallocatormxf-getmessage)新しくゼロ DMU を取得\_カーネル\_再利用するためのアロケーターからのイベント構造体。 (アロケーターは、DMU を空にすると作成される\_カーネル\_しない空の状態を開始するように、プール内のイベント構造です)。ダイアグラムの次の図の Irp で示すように (DMU の形式で\_EVENTHEADER 構造体) を返し、dmusic.dll から受け取る。

![ポートおよびミニポートのドライバーを介して irp のフローを示す図](images/dmalloc.png)

アンパッカー呼び出し**IAllocatorMXF::GetMessage**空を取得する[ **DMU\_カーネル\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/ns-dmusicks-_dmus_kernel_event)構造体。 取得、DMU を返し、\_カーネル\_イベント IRP から構造体、(MIDI イベントごとに 1 つ)、これらの構造体に格納および sequencer を (その MXF インターフェイスを使用) に渡します。 Sequencer そのタイムスタンプに基づいて順序変更を期限になったに渡しますミニポート ドライバーを呼び出して**IMXF::PutMessage**します。 ミニポート ドライバーは、DMU から MIDI データ\_カーネル\_wave データに表示されるように、イベントが構造体します。 使用の DMU を渡す\_カーネル\_イベント構造体が別のアロケーターにバックアップ**IMXF::PutMessage**呼び出します。

逆の状況では、キャプチャは発生します。 MIDI データの元ハードウェア、ミニポート ドライバーとミニポート ドライバーの呼び出しに**IAllocatorMXF::GetMessage**空の DMU を取得する\_カーネル\_イベント構造体。 DMU\_カーネル\_構造体のイベントのタイムスタンプとデータの格納し、を使用してキャプチャ シンクに渡される**IMXF::PutMessage**します。 DMU を設定する場合、ミニポート ドライバーは構造体ごとの 1 つ以上のメッセージを渡すことができます\_KEF\_イベント\_未完了フラグ、DMU\_カーネル\_イベント構造体。 Dmu ポート ドライバーのキャプチャのシンクは、この生データ ストリームを解析し、DMU を出力\_カーネル\_タイムスタンプ MIDI メッセージ (構造体ごとに 1 つ) が含まれるイベントの構造体。

ミニポート ドライバー自体キャプチャ シンクへのメッセージのタイムスタンプを生成することもできます。 この場合、ドライバーが、DMU を設定しません\_KEF\_イベント\_DMU 内のビットが完了していない\_カーネル\_イベント。 キャプチャ シンクは、Irp にメッセージをパッケージ化し、dmusic.dll に送信すると、packer に直接、タイムスタンプの構造体を渡します。 DirectMusic キャプチャは MIDI を記録するだけです。 Wave 記録、DirectSound のキャプチャを使用します。

Packer が、DMU からデータをプルするときに\_カーネル\_イベント構造、使用の DMU を破棄します\_カーネル\_イベントの構造を持つアロケーターに**IMXF::PutMessage**します。 IRP バッファーがいっぱいに dmusic.dll 渡されます。 Packer は、dmusic.dll から空の Irp を受信するには、入力、およびそれを完了しました。 Irp の詳細については、常に入力するいずれかにダウン配信を保持します。

 

 




