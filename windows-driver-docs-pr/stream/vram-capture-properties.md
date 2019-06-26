---
title: VRAM キャプチャのプロパティ
description: VRAM キャプチャのプロパティ
ms.assetid: e3ab3a10-42af-488f-9b13-d2c6d5aac615
keywords:
- VRAM キャプチャ WDK AVStream、プロパティ
- WDK AVStream のシステム メモリへのキャプチャ
- pin VRAM WDK AVStream の処理
- VRAM は、WDK AVStream、要求シーケンスをキャプチャします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: edffc83e3dcc43882a60b55b1bcd4bfc183a89ac
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385359"
---
# <a name="vram-capture-properties"></a>VRAM キャプチャのプロパティ


暗証番号 (pin) を中心とした AVStream ミニドライバーは、VRAM をキャプチャするために、いくつかのプロパティをサポートする必要があります。 このセクションでは前に、と VRAM 処理中に、ミニドライバーが受信した要求のシーケンスについて説明します。

キャプチャが開始されると、前に、KS プロキシに送信、 [ **KSPROPERTY\_優先\_キャプチャ\_画面**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-preferred-capture-surface)プロパティの get 要求。 ミニドライバーは、システム メモリまたは VRAM にドライバーをキャプチャするかどうかに応じて異なる値を返す必要があります。

### <a name="capturing-to-system-memory"></a>システム メモリへのキャプチャ

システム メモリをキャプチャして、返す KS\_キャプチャ\_アロケーション\_システム\_AGP します。

キャプチャのドライバーを受信し、 [ **KSPROPERTY\_現在\_キャプチャ\_画面**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-current-capture-surface)システム メモリの値の型を持つプロパティの設定要求。 ようになりました、キャプチャ ドライバーは、バス マスター DMA デバイスとして動作し、システム メモリに直接データを配置します。

このモードでキャプチャ ドライバーがシステム メモリ バッファーを受信、 [ *AVStrMiniPinProcess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnkspin)出力ピンのコールバック関数。

暗証番号 (pin) プロセス コールバックで DMA を実装する方法については、次を参照してください。 [AVStream で DMA をパケットに基づく](packet-based-dma-in-avstream.md)します。

(たとえば、別のビデオ、オーディオ、および VBI ピン) の複数の出力ピンをキャプチャするには、各ピンする必要があります、VRAM プロパティや処理のサポート前述のようです。 プロキシは、各ピンに別のスレッドを生成します。

### <a name="capturing-to-vram"></a>VRAM へのキャプチャ

ドライバーは、VRAM キャプチャをサポートする場合に返す**KS\_キャプチャ\_アロケーション\_VRAM** KSPROPERTY への応答で\_優先\_キャプチャ\_画面。

次に、ミニドライバーを受け取る、 [ **KSPROPERTY\_表示\_アダプター\_GUID** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-display-adapter-guid)ディスプレイ アダプターの GUID のクエリのプロパティの get 要求。

ベンダーから提供されたグラフィックスのミニポート ドライバーからアダプターの GUID を取得します。 [ **DXGK\_INTERFACESPECIFICDATA** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxgk-interfacespecificdata)構造体には、アダプター プロパティの要求で返される GUID にはが含まれています。 この構造は、DirectX グラフィックスのカーネル (DXGK) サブシステムによって生成され、アダプターが初期化されるときに、ミニポート ドライバーに渡されます。

VRAM トランスポートとディスプレイ アダプターとダウン ストリームのフィルターの一致の Guid を暗証番号 (pin) をサポートする場合は、KS プロキシ モジュールが、アロケーターとして選択されます。 プロキシに通知を設定してピンの間の VRAM サーフェス トランスポートの選択に関するキャプチャ暗証番号 (pin)、 [ **KSPROPERTY\_現在\_キャプチャ\_画面**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-current-capture-surface)キャプチャに対して選択された画面の種類を持つプロパティです。

Pin が KS を受け取った場合\_キャプチャ\_アロケーション\_VRAM、VRAM 要求を処理し、受信されます。

VRAM 処理要求は、2 つの部分で構成されます。 キャプチャ ドライバーでの get 要求を受信する最初に、 [ **KSPROPERTY\_マップ\_キャプチャ\_処理\_TO\_VRAM\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-map-capture-handle-to-vram-address). Get ハンドラーは、カーネル モード VRAM サーフェス ハンドルを格納する IRP を受信します。

キャプチャ ドライバーまたはディスプレイのミニポート ドライバーは、実際の VRAM 物理アドレスを VRAM サーフェスのハンドルをマップする必要があります。 VRAM サーフェス ハンドル*はない有効なまま; しない*それを後で使用できるキャッシュです。

マップされたアドレスを返す、 [ **VRAM\_画面\_情報\_プロパティ\_S** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-vram_surface_info_property_s)プロパティ要求で指定されました。 キャプチャ ドライバーでは、ディスプレイのミニポート ドライバーからのマッピングを要求する IOCTL を発行できます。

2 番目、キャプチャ フィルターの*AVStrMiniPinProcess* pin があるデータを処理するときに呼び出されます。

呼び出す必要があります、ミニドライバー [ **KsPinGetLeadingEdgeStreamPointer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kspingetleadingedgestreampointer)を取得し、このピンのリーディング エッジ ストリーム ポインターをロックします。 この関数へのポインターを返します、 [ **KSSTREAM\_ポインター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksstream_pointer)構造体。

このストリーム ポインター構造体にはへのポインターが含まれています、 [ **KSSTREAM\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstream_header)します。

**データ**ストリーム ヘッダーのメンバーへのポインターを検索、 [ **VRAM\_画面\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-vram_surface_info)構造体。

この構造体には、KSPROPERTY への応答で返された物理アドレスが含まれています。\_マップ\_キャプチャ\_処理\_TO\_VRAM\_アドレス。 **HSurface**ハンドルを表すメンバーが**NULL**します。

キャプチャのドライバーが必要です。

-   プログラム、そのキャプチャ ハードウェア VRAM の物理アドレスを使用します。

-   ビデオ フレームの完了を処理します。

-   入力、 **cbCaptured** VRAM のメンバー\_画面\_バイト数の情報が VRAM サーフェスにコピーします。 設定しないでください、 **DataUsed** KSSTREAM のメンバー\_ヘッダーでキャプチャされたバイト数。 代わりに、設定**DataUsed**に sizeof (VRAM\_画面\_情報)。

-   キャプチャには、ドライバーは、タイムスタンプを実行する場合は、設定**PresentationTime**、**期間**、および該当する場合、 **OptionsFlags** KSSTREAM で\_ヘッダー。

-   呼び出す[ **KsStreamPointerAdvanceOffsets** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointeradvanceoffsets)処理を続行またはすべてのクローンを削除し、呼び出すことによって、要求を完了する[ **KsStreamPointerDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerdelete).

**CCapturePin::ProcessD3DSurface**メソッド*Capture.cpp*の[AVStream シミュレートされたハードウェア ドライバーのサンプル (AVSHwS)](https://go.microsoft.com/fwlink/p/?linkid=256083) Windows Driver Kit (WDK) のサンプルVRAM サポートに対するこのコールバックを実装する方法を説明します。

 

 




