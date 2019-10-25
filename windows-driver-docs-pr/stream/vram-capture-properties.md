---
title: VRAM キャプチャのプロパティ
description: VRAM キャプチャのプロパティ
ms.assetid: e3ab3a10-42af-488f-9b13-d2c6d5aac615
keywords:
- VRAM capture WDK AVStream、プロパティ
- システムメモリの WDK AVStream にキャプチャしています
- 固定 VRAM 処理 WDK AVStream
- VRAM capture WDK AVStream、要求シーケンス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ec43e1ea3bf5a577fc0d6906b085011c6cc9798
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845275"
---
# <a name="vram-capture-properties"></a>VRAM キャプチャのプロパティ


ピン中心の AVStream ミニドライバーは、VRAM に取り込むために複数のプロパティをサポートする必要があります。 このセクションでは、ミニドライバーが VRAM 処理の前後に受け取る要求のシーケンスについて説明します。

キャプチャが開始される前に、KS プロキシは\_SURFACE の get プロパティ要求\_キャプチャするために[ **\_Ksk プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-preferred-capture-surface)を送信します。 ミニドライバーは、ドライバーがシステムメモリと VRAM のどちらにキャプチャされているかによって異なる値を返す必要があります。

### <a name="capturing-to-system-memory"></a>キャプチャ (システムメモリに)

システムメモリにキャプチャするには、\_ALLOC\_SYSTEM\_AGP\_キャプチャする KS を返します。

キャプチャドライバーは、[**現在\_\_Ksk プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-current-capture-surface)を受け取ります。このプロパティには、システムメモリ値の型を持つ\_SURFACE set-property 要求がキャプチャされます。 キャプチャドライバーは、バスマスタ DMA デバイスとして機能し、データをシステムメモリに直接配置します。

このモードでは、キャプチャドライバーは、出力ピンの[*Avstrminipinprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspin)コールバック関数でシステムメモリバッファーを受け取ります。

Pin プロセスコールバックで DMA を実装する方法については、 [AVStream のパケットベースの dma](packet-based-dma-in-avstream.md)に関する説明を参照してください。

複数の出力ピン (たとえば、個別のビデオ、オーディオ、VBI ピン) でキャプチャするには、各ピンが前に説明した VRAM のプロパティと処理をサポートする必要があります。 プロキシは、pin ごとに個別のスレッドを生成します。

### <a name="capturing-to-vram"></a>VRAM へのキャプチャ

ドライバーで VRAM キャプチャがサポートされている場合は、\_を返します。\_は、KSK\_プロパティに応答して**ALLOC\_vram をキャプチャ**し、\_の\_キャプチャを推奨します。

次のミニドライバーは、 [ **\_アダプター\_guid**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-display-adapter-guid)の取得プロパティの要求を表示\_ksk プロパティを受け取り、表示アダプターの guid を照会します。

ベンダーから提供されたグラフィックスミニポートドライバーからアダプターの GUID を取得します。 [**DXGK\_INTERFACESPECIFICDATA**](https://docs.microsoft.com/windows-hardware/drivers/display/dxgk-interfacespecificdata)構造体には、プロパティ要求で返すアダプター GUID が含まれています。 この構造は DirectX グラフィックスカーネル (DXGK) サブシステムによって生成され、アダプターの初期化時にミニポートドライバーに渡されます。

Pin が VRAM トランスポートをサポートし、ディスプレイアダプターとダウンストリームフィルターが一致する場合、KS プロキシモジュールがアロケーターとして選択されます。 このプロキシは、 [**Ksk プロパティ\_現在\_キャプチャ\_surface**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-current-capture-surface)プロパティをキャプチャに選択されたサーフェイスの種類に設定することにより、ピン間の VRAM の移動をキャプチャピンに通知します。

ピンが\_ALLOC\_VRAM\_キャプチャすると、VRAM 処理要求を受け取ります。

VRAM 処理要求は2つの部分で構成されます。 まず、キャプチャドライバーは Ksk プロパティの get 要求を受信します。この[ **\_マップ\_キャプチャ\_ハンドルして\_を\_VRAM\_アドレスに処理**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-map-capture-handle-to-vram-address)します。 Get ハンドラーは、カーネルモードの VRAM サーフェイスハンドルを含む IRP を受け取ります。

キャプチャドライバーまたはディスプレイミニポートドライバーは、VRAM サーフェイスハンドルを実際の VRAM 物理アドレスにマップする必要があります。 VRAM サーフェイスハンドル*は有効なままではありません。* 後で使用できるようにキャッシュしないでください。

プロパティ要求で提供された[ **\_情報\_プロパティ\_の、VRAM\_SURFACE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-vram_surface_info_property_s)内のマップされたアドレスを返します。 キャプチャドライバーは、ディスプレイミニポートドライバーからのマッピングを要求する IOCTL を発行できます。

次に、キャプチャフィルターの*Avstrminipinprocess*は、ピンに処理するデータがあるときに呼び出されます。

ミニドライバーは、このピンのリーディングエッジストリームポインターを取得してロックするために、 [**KsPinGetLeadingEdgeStreamPointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspingetleadingedgestreampointer)を呼び出す必要があります。 この関数は、 [**Ksk ストリーム\_ポインター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksstream_pointer)構造体へのポインターを返します。

このストリームポインター構造体には、 [**Ksk ストリーム\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)へのポインターが含まれています。

ストリームヘッダーの**データ**メンバーで、 [**VRAM\_SURFACE\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-vram_surface_info)構造体へのポインターを見つけます。

この構造体には、KSK プロパティ\_マップ\_キャプチャ\_ハンドル\_を\_VRAM\_アドレスに返すために返される物理アドレスが含まれます。 ハンドルを表す**Hsurface**メンバーが**NULL**です。

キャプチャドライバーは次のことを行う必要があります。

-   VRAM 物理アドレスを使用してキャプチャハードウェアをプログラムします。

-   ビデオフレームの完了を処理します。

-   VRAM\_\_SURFACE の**Cbcaptured**されたメンバーに、vram サーフェイスにコピーされたバイト数を入力します。 KSK ストリーム\_ヘッダーの**Dataused**メンバーを、キャプチャされたバイト数で設定しないでください。 代わりに、 **Dataused**を SIZEOF (VRAM\_SURFACE\_INFO) に設定します。

-   キャプチャドライバーがタイムスタンプを実行する場合は、**プレゼンテーション時間**、**期間** を設定し、必要に応じて、ksk ストリーム\_ヘッダーに**オプションフラグ**を設定します。

-   [**KsStreamPointerAdvanceOffsets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointeradvanceoffsets)を呼び出して、処理を続行するか、すべての複製を削除してから、 [**Ksstreamポインター delete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerdelete)を呼び出して要求を完了します。

Windows Driver Kit (WDK) のサンプルに含まれている[Avstream](https://go.microsoft.com/fwlink/p/?linkid=256083)の**CCapturePin::P rocessd3dsurface**メソッドは、このコールバックを実装する1つの方法を示しています *。*

 

 




