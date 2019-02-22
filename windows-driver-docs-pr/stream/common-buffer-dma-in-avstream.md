---
title: 一般的なバッファー AVStream で DMA
description: 一般的なバッファー AVStream で DMA
ms.assetid: 8cbadb5a-f879-4fe0-a698-cde3b9f6df83
keywords:
- 一般的なバッファー DMA WDK AVStream
- WDK AVStream のバッファー
- AVStream WDK、ハードウェア
- ハードウェア WDK AVStream
- DMA は、WDK AVStream をサービスします。
- ダイレクト メモリ アクセスの WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac16acaa0dc352119f56e77d397587d42fb92043
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559108"
---
# <a name="common-buffer-dma-in-avstream"></a>一般的なバッファー AVStream で DMA





一般的なバッファーのダイレクト メモリ アクセス (DMA) は、デバイスは、キャプチャ バッファーに直接書き込みませんときに発生します。代わりに共通のバッファーとの間のデータをコピーします。

AVStream ミニドライバーで共通のバッファー DMA を使用します。

1.  DMA アダプターを呼び出すことによって取得[ **IoGetDmaAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff549220)パケットに基づく DMA のようにします。 KSPIN を指定しない\_フラグ\_生成\_のマッピング、**フラグ**のメンバー、 [ **KSPIN\_記述子\_EX**](https://msdn.microsoft.com/library/windows/hardware/ff563534)構造体、および AVStream では、DMA アダプターを登録しないでください。 独自のプライベート バッファーのコピー/スキームを実装する必要があります。

2.  割り込みサービス ルーチン (ISR) の登録」の説明に従って[ハードウェア AVStream ミニドライバーの書き込み](writing-avstream-minidrivers-for-hardware.md)

場合、**フラグ**KSPIN のメンバー\_記述子\_EX 設定 KSPIN\_フラグ\_は\_いない\_開始\_次の処理AVStream 呼び出し前に、の手順が実行[ *AVStrMiniPinProcess*](https://msdn.microsoft.com/library/windows/hardware/ff556351):

1.  ミニドライバーは、その共通のバッファー転送を設定します。

2.  カーネルは、仕入先が以前に登録されている ISR を呼び出します。 ISR、ミニドライバーは遅延プロシージャ呼び出し (DPC) をキューします。

3.  一般的なバッファーがいっぱいになった場合、ミニドライバーを呼び出す[ **KsPinAttemptProcessing** ](https://msdn.microsoft.com/library/windows/hardware/ff563494) DPC から。

4.  AVStream 呼び出しで指定された条件の場合は、プロセスのディスパッチ、**フラグ**のメンバー [ **KSPIN\_記述子\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff563534)が満たされています。

ベンダーから提供された内[ *AVStrMiniPinProcess* ](https://msdn.microsoft.com/library/windows/hardware/ff556351)コールバック ルーチンでは、1 つの可能な一連のアクションが次のようにします。

1.  呼び出す[ **KsPinGetLeadingEdgeStreamPointer**](https://msdn.microsoft.com/library/windows/hardware/ff563513):

    ```cpp
    KSSTREAM_POINTER *Leading = KsPinGetLeadingEdgeStreamPointer (
                    Pin,
                    State
                   );
    ```

2.  先頭のフレーム データをコピー&gt;StreamHeader -&gt;データと必要なフラグを設定し、時刻、適切なスタンプ情報[ **KSSTREAM\_ヘッダー**](https://msdn.microsoft.com/library/windows/hardware/ff567138)します。

3.  呼び出す[ **KsStreamPointerUnlock** ](https://msdn.microsoft.com/library/windows/hardware/ff567137)で*取り出し*に設定**TRUE**します。 (この値の*取り出し*を進めるストリーム ポインターをによりします)。

4.  状態を返す\_保留します。

AVStream のミニドライバーによって設定されたフラグに基づいてこのキューを管理し、 [ **KSPIN\_記述子\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff563534)構造体。

 

 




