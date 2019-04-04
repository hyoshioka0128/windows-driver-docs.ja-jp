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
ms.openlocfilehash: d3f8a783d806952ad850034f2c6654643f4f2e73
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573418"
---
# <a name="vram-capture-properties"></a>VRAM キャプチャのプロパティ


暗証番号 (pin) を中心とした AVStream ミニドライバーは、VRAM をキャプチャするために、いくつかのプロパティをサポートする必要があります。 このセクションでは前に、と VRAM 処理中に、ミニドライバーが受信した要求のシーケンスについて説明します。

キャプチャが開始されると、前に、KS プロキシに送信、 [ **KSPROPERTY\_優先\_キャプチャ\_画面**](https://msdn.microsoft.com/library/windows/hardware/ff565209)プロパティの get 要求。 ミニドライバーは、システム メモリまたは VRAM にドライバーをキャプチャするかどうかに応じて異なる値を返す必要があります。

### <a name="capturing-to-system-memory"></a>システム メモリへのキャプチャ

システム メモリをキャプチャして、返す KS\_キャプチャ\_アロケーション\_システム\_AGP します。

キャプチャのドライバーを受信し、 [ **KSPROPERTY\_現在\_キャプチャ\_画面**](https://msdn.microsoft.com/library/windows/hardware/ff565130)システム メモリの値の型を持つプロパティの設定要求。 ようになりました、キャプチャ ドライバーは、バス マスター DMA デバイスとして動作し、システム メモリに直接データを配置します。

このモードでキャプチャ ドライバーがシステム メモリ バッファーを受信、 [ *AVStrMiniPinProcess* ](https://msdn.microsoft.com/library/windows/hardware/ff556351)出力ピンのコールバック関数。

暗証番号 (pin) プロセス コールバックで DMA を実装する方法については、[AVStream で DMA をパケットに基づく](packet-based-dma-in-avstream.md)を参照してください。

(たとえば、別のビデオ、オーディオ、および VBI ピン) の複数の出力ピンをキャプチャするには、各ピンする必要があります、VRAM プロパティや処理のサポート前述のようです。 プロキシは、各ピンに別のスレッドを生成します。

### <a name="capturing-to-vram"></a>VRAM へのキャプチャ

ドライバーは、VRAM キャプチャをサポートする場合に返す**KS\_キャプチャ\_アロケーション\_VRAM** KSPROPERTY への応答で\_優先\_キャプチャ\_画面。

次に、ミニドライバーを受け取る、 [ **KSPROPERTY\_表示\_アダプター\_GUID** ](https://msdn.microsoft.com/library/windows/hardware/ff565134)ディスプレイ アダプターの GUID のクエリのプロパティの get 要求。

ベンダーから提供されたグラフィックスのミニポート ドライバーからアダプターの GUID を取得します。 [ **DXGK\_INTERFACESPECIFICDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff561134)構造体には、アダプター プロパティの要求で返される GUID にはが含まれています。 この構造は、DirectX グラフィックスのカーネル (DXGK) サブシステムによって生成され、アダプターが初期化されるときに、ミニポート ドライバーに渡されます。

VRAM トランスポートとディスプレイ アダプターとダウン ストリームのフィルターの一致の Guid を暗証番号 (pin) をサポートする場合は、KS プロキシ モジュールが、アロケーターとして選択されます。 プロキシに通知を設定してピンの間の VRAM サーフェス トランスポートの選択に関するキャプチャ暗証番号 (pin)、 [ **KSPROPERTY\_現在\_キャプチャ\_画面**](https://msdn.microsoft.com/library/windows/hardware/ff565130)キャプチャに対して選択された画面の種類を持つプロパティです。

Pin が KS を受け取った場合\_キャプチャ\_アロケーション\_VRAM、VRAM 要求を処理し、受信されます。

VRAM 処理要求は、2 つの部分で構成されます。 キャプチャ ドライバーでの get 要求を受信する最初に、 [ **KSPROPERTY\_マップ\_キャプチャ\_処理\_TO\_VRAM\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/ff565177). Get ハンドラーは、カーネル モード VRAM サーフェス ハンドルを格納する IRP を受信します。

キャプチャ ドライバーまたはディスプレイのミニポート ドライバーは、実際の VRAM 物理アドレスを VRAM サーフェスのハンドルをマップする必要があります。 VRAM サーフェス ハンドル*はない有効なまま; しない*それを後で使用できるキャッシュです。

マップされたアドレスを返す、 [ **VRAM\_画面\_情報\_プロパティ\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff568785)プロパティ要求で指定されました。 キャプチャ ドライバーでは、ディスプレイのミニポート ドライバーからのマッピングを要求する IOCTL を発行できます。

2 番目、キャプチャ フィルターの*AVStrMiniPinProcess* pin があるデータを処理するときに呼び出されます。

呼び出す必要があります、ミニドライバー [ **KsPinGetLeadingEdgeStreamPointer** ](https://msdn.microsoft.com/library/windows/hardware/ff563513)を取得し、このピンのリーディング エッジ ストリーム ポインターをロックします。 この関数へのポインターを返します、 [ **KSSTREAM\_ポインター** ](https://msdn.microsoft.com/library/windows/hardware/ff567139)構造体。

このストリーム ポインター構造体にはへのポインターが含まれています、 [ **KSSTREAM\_ヘッダー**](https://msdn.microsoft.com/library/windows/hardware/ff567138)します。

**データ**ストリーム ヘッダーのメンバーへのポインターを検索、 [ **VRAM\_画面\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff568783)構造体。

この構造体には、KSPROPERTY への応答で返された物理アドレスが含まれています。\_マップ\_キャプチャ\_処理\_TO\_VRAM\_アドレス。 **HSurface**ハンドルを表すメンバーが**NULL**します。

キャプチャのドライバーが必要です。

-   プログラム、そのキャプチャ ハードウェア VRAM の物理アドレスを使用します。

-   ビデオ フレームの完了を処理します。

-   入力、 **cbCaptured** VRAM のメンバー\_画面\_バイト数の情報が VRAM サーフェスにコピーします。 設定しないでください、 **DataUsed** KSSTREAM のメンバー\_ヘッダーでキャプチャされたバイト数。 代わりに、設定**DataUsed**に sizeof (VRAM\_画面\_情報)。

-   キャプチャには、ドライバーは、タイムスタンプを実行する場合は、設定**PresentationTime**、**期間**、および該当する場合、 **OptionsFlags** KSSTREAM で\_ヘッダー。

-   呼び出す[ **KsStreamPointerAdvanceOffsets** ](https://msdn.microsoft.com/library/windows/hardware/ff567126)処理を続行またはすべてのクローンを削除し、呼び出すことによって、要求を完了する[ **KsStreamPointerDelete**](https://msdn.microsoft.com/library/windows/hardware/ff567130).

**CCapturePin::ProcessD3DSurface**メソッド*Capture.cpp*の[AVStream シミュレートされたハードウェア ドライバーのサンプル (AVSHwS)](https://go.microsoft.com/fwlink/p/?linkid=256083) Windows Driver Kit (WDK) のサンプルVRAM サポートに対するこのコールバックを実装する方法を説明します。

 

 




