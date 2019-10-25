---
title: AVStream の共通バッファー DMA
description: AVStream の共通バッファー DMA
ms.assetid: 8cbadb5a-f879-4fe0-a698-cde3b9f6df83
keywords:
- 共通バッファー DMA WDK AVStream
- WDK AVStream のバッファー
- AVStream WDK、ハードウェア
- ハードウェア WDK AVStream
- DMA サービス WDK AVStream
- ダイレクトメモリアクセス WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de6dbb52d010b13e74c4312c496dfb5f36ec90e7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844716"
---
# <a name="common-buffer-dma-in-avstream"></a>AVStream の共通バッファー DMA





一般的なバッファーダイレクトメモリアクセス (DMA) は、デバイスがキャプチャバッファーに直接書き込まない場合に発生します。代わりに、共通のバッファーとの間でデータをコピーします。

AVStream ミニドライバーで共通バッファー DMA を使用するには、次のようにします。

1.  パケットベースの DMA のように[**IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)を呼び出して、dma アダプターを取得します。 KSPIN\_\_フラグを指定しないでください。 kspin [ **\_DESCRIPTOR\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)構造体の**Flags**メンバーに\_マッピングを生成し、DMA アダプターを avstream に登録しないようにします。 独自のプライベートバッファー/コピースキームを実装することが必要になる場合があります。

2.  「[ハードウェアの AVStream ミニドライバーの作成](writing-avstream-minidrivers-for-hardware.md)」の説明に従って、interrupt service ルーチン (ISR) を登録します。

KSPIN\_記述子の**Flags**メンバー\_EX が kspin\_\_フラグを設定し、\_処理を開始\_ない場合は、Avstream が[*Avstrminipinprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspin)を呼び出す前に次の手順が実行されます。

1.  ミニドライバーは、一般的なバッファー転送を設定します。

2.  カーネルは、ベンダーが以前に登録した ISR を呼び出します。 ISR では、ミニドライバーは遅延プロシージャ呼び出し (DPC) をキューに置いています。

3.  共通バッファーがいっぱいになると、ミニドライバーは DPC から[**KsPinAttemptProcessing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspinattemptprocessing)を呼び出します。

4.  [**Kspin\_記述子\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)の**Flags**メンバーによって指定された条件が満たされた場合、avstream はプロセスディスパッチを呼び出します。

ベンダーから提供された[*Avstrminipinprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspin)コールバックルーチン内では、次のような1つの措置をとることができます。

1.  [**KsPinGetLeadingEdgeStreamPointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspingetleadingedgestreampointer)を呼び出します。

    ```cpp
    KSSTREAM_POINTER *Leading = KsPinGetLeadingEdgeStreamPointer (
                    Pin,
                    State
                   );
    ```

2.  フレームデータを先頭&gt;StreamHeader-&gt;データにコピーし、適切な[**Ksk ストリーム\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)に必要なフラグとタイムスタンプ情報を設定します。

3.  *Eject*が**TRUE**に設定された状態で、 [**ksstreamポインター unlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerunlock)を呼び出します。 (この*値を指定すると、* ストリームポインターが先に進みます)。

4.  ステータスを返す\_保留中です。

AVStream は、 [**Kspin\_記述子\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)構造体のミニドライバーによって設定されたフラグに基づいてキューを管理します。

 

 




