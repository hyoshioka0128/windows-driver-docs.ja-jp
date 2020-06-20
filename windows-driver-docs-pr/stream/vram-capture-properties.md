---
title: VRAM キャプチャのプロパティ
description: VRAM キャプチャのプロパティ
ms.assetid: e3ab3a10-42af-488f-9b13-d2c6d5aac615
keywords:
- VRAM capture WDK AVStream、プロパティ
- システムメモリの WDK AVStream にキャプチャしています
- 固定 VRAM 処理 WDK AVStream
- VRAM capture WDK AVStream、要求シーケンス
ms.date: 06/19/2020
ms.localizationpriority: medium
ms.openlocfilehash: 46fb36bedb55839564a12ee88a89b569e850cdb2
ms.sourcegitcommit: baf3075858705d4c78d4ea4b0869bf6291bcb823
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2020
ms.locfileid: "85112133"
---
# <a name="vram-capture-properties"></a>VRAM キャプチャのプロパティ

ピン中心の AVStream ミニドライバーは、VRAM に取り込むために複数のプロパティをサポートする必要があります。 このセクションでは、ミニドライバーが VRAM 処理の前後に受け取る要求のシーケンスについて説明します。

キャプチャが開始される前に、KS プロキシは[**Ksk プロパティの推奨される \_ \_ キャプチャ \_ サーフェス**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-preferred-capture-surface)の get プロパティ要求を送信します。 ミニドライバーは、ドライバーがシステムメモリと VRAM のどちらにキャプチャされているかによって異なる値を返す必要があります。

## <a name="capturing-to-system-memory"></a>キャプチャ (システムメモリに)

システムメモリにキャプチャするには、KS \_ capture \_ ALLOC system AGP を返し \_ \_ ます。

キャプチャドライバーは、システムメモリ値の型を使用して、 [**Ksk プロパティの \_ 現在の \_ キャプチャ \_ 画面**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-current-capture-surface)のプロパティ要求を受け取ります。 キャプチャドライバーは、バスマスタ DMA デバイスとして機能し、データをシステムメモリに直接配置します。

このモードでは、キャプチャドライバーは、出力ピンの[*Avstrminipinprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspin)コールバック関数でシステムメモリバッファーを受け取ります。

Pin プロセスコールバックで DMA を実装する方法については、 [AVStream のパケットベースの dma](packet-based-dma-in-avstream.md)に関する説明を参照してください。

複数の出力ピン (たとえば、個別のビデオ、オーディオ、VBI ピン) でキャプチャするには、各ピンが前に説明した VRAM のプロパティと処理をサポートする必要があります。 プロキシは、pin ごとに個別のスレッドを生成します。

## <a name="capturing-to-vram"></a>VRAM へのキャプチャ

ドライバーが VRAM キャプチャをサポートしている場合は、KSPROPERTY の推奨されるキャプチャサーフェイスに応答して**KS \_ キャプチャの \_ アロケーション \_ VRAM**を返し \_ \_ \_ ます。

次に、ミニドライバーは、表示アダプターの GUID に対してクエリを実行して、 [**ksproperty \_ 表示 \_ アダプターの \_ guid**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-display-adapter-guid)取得プロパティの要求を受信します。

ベンダーから提供されたグラフィックスミニポートドライバーからアダプターの GUID を取得します。 [**DXGK \_ INTERFACESPECIFICDATA**](https://docs.microsoft.com/windows-hardware/drivers/display/dxgk-interfacespecificdata)構造体には、プロパティ要求で返すアダプター GUID が含まれています。 この構造は DirectX グラフィックスカーネル (DXGK) サブシステムによって生成され、アダプターの初期化時にミニポートドライバーに渡されます。

Pin が VRAM トランスポートをサポートし、ディスプレイアダプターとダウンストリームフィルターが一致する場合、KS プロキシモジュールがアロケーターとして選択されます。 このプロキシは、 [**Ksk プロパティの \_ 現在の \_ キャプチャ \_ サーフェイス**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-current-capture-surface)プロパティをキャプチャ用に選択されたサーフェイスの種類に設定することにより、ピン間での VRAM surface トランスポートの選択についてキャプチャピンに通知します。

ピンが KS キャプチャの \_ \_ アロケーション \_ vram を受け取ると、VRAM 処理要求を受信します。

VRAM 処理要求は2つの部分で構成されます。 最初に、キャプチャドライバーは、 [** \_ \_ \_ \_ \_ VRAM \_ アドレスに対して ksk プロパティマップキャプチャハンドル**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-map-capture-handle-to-vram-address)の get 要求を受け取ります。 Get ハンドラーは、カーネルモードの VRAM サーフェイスハンドルを含む IRP を受け取ります。

キャプチャドライバーまたはディスプレイミニポートドライバーは、VRAM サーフェイスハンドルを実際の VRAM 物理アドレスにマップする必要があります。 VRAM サーフェイスハンドル*は有効なままではありません。* 後で使用できるようにキャッシュしないでください。

プロパティ要求に指定された[**VRAM \_ SURFACE \_ INFO \_ プロパティ \_ **](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-vram_surface_info_property_s)のマップされたアドレスを返します。 キャプチャドライバーは、ディスプレイミニポートドライバーからのマッピングを要求する IOCTL を発行できます。

次に、キャプチャフィルターの*Avstrminipinprocess*は、ピンに処理するデータがあるときに呼び出されます。

ミニドライバーは、このピンのリーディングエッジストリームポインターを取得してロックするために、 [**KsPinGetLeadingEdgeStreamPointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspingetleadingedgestreampointer)を呼び出す必要があります。 この関数は、 [**Ksk ストリーム \_ ポインター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksstream_pointer)構造体へのポインターを返します。

このストリームポインター構造体には、 [**Ksk ストリーム \_ ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)へのポインターが含まれています。

ストリームヘッダーの**データ**メンバーで、 [**VRAM \_ SURFACE \_ 情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-vram_surface_info)構造体へのポインターを見つけます。

この構造体には、VRAM のプロパティマップのキャプチャハンドルへの応答として返される物理アドレスが含まれ \_ \_ \_ \_ \_ \_ ます。 ハンドルを表す**Hsurface**メンバーが**NULL**です。

キャプチャドライバーは次のことを行う必要があります。

- VRAM 物理アドレスを使用してキャプチャハードウェアをプログラムします。

- ビデオフレームの完了を処理します。

- VRAM サーフェイスにコピーされたバイト数を使用して、 **cbcaptured 情報の Cbcaptured**メンバーを入力し \_ \_ ます。 KSK ストリームヘッダーの**Dataused**メンバーに、 \_ キャプチャされたバイト数を設定しないでください。 代わりに、 **Dataused**を SIZEOF (VRAM \_ SURFACE INFO) に設定し \_ ます。

- キャプチャドライバーでタイムスタンプが実行される場合は、[KSK ストリームヘッダー] に [**プレゼンテーション時間**]、[**期間**]、および [関連する**オプション] フラグ**を設定し \_ ます。

- [**KsStreamPointerAdvanceOffsets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointeradvanceoffsets)を呼び出して、処理を続行するか、すべての複製を削除してから、 [**Ksstreamポインター delete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerdelete)を呼び出して要求を完了します。

Windows Driver Kit (WDK) のサンプルでは、Avstream でシミュレートされた[ハードウェアサンプルドライバー (AVSHwS)](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/avstream-simulated-hardware-sample-driver-avshws)の**CCapturePin::P rocessd3dsurface**メソッドは、このコールバックを実装して VRAM をサポートする方法の1つを示してい*ます。*
