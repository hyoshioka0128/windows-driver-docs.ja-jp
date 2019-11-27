---
title: NDIS Scatter/Gather DMA
description: NDIS Scatter/Gather DMA
ms.assetid: 70b8321b-7b21-4d11-a9c2-46b0caa26ce6
keywords:
- ミニポートドライバー WDK ネットワーク、スキャッター/ギャザー DMA
- NDIS ミニポートドライバー WDK、スキャッター/ギャザー DMA
- スキャッター/ギャザー DMA WDK ネットワーク
- SGDMA WDK ネットワーク
- Nic WDK ネットワーク、システムメモリ転送
- ネットワークインターフェイスカード WDK ネットワーク、s
ms.date: 06/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: fdfd21539c62e40f85ecd8017c7fd3685f82bd9c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833747"
---
# <a name="ndis-scattergather-dma"></a>NDIS Scatter/Gather DMA

[!include[NDIS DMA ARM note](ndis-dma-arm-note.md)]

NDIS ミニポートドライバーでは、スキャッター/ギャザー DMA (SGDMA) メソッドを使用して、NIC とシステムメモリ間でデータを転送できます。 DMA 転送を成功させるには、NIC がサポートするアドレス範囲にデータの物理アドレスを指定する必要があります。 HAL は、MDL チェーンの物理アドレスリストを取得するためのドライバーのメカニズムを提供します。また、必要に応じて、データを物理アドレス範囲にダブルバッファーします。

Ndis 6.0 より前のバージョンの NDIS では、ミニポートドライバーおよび NDIS での SGDMA のサポートはいくつかの点で制限されており、特にマルチパケット送信シナリオでは適切に機能しません。 NDIS 6.0 SGDMA のサポートでは、これらの制限を克服しながら、ミニポートドライバー用のシンプルなインターフェイスを提供しています。

## <a name="history-of-ndis-sgdma"></a>NDIS SGDMA の履歴

Ndis 6.0 より前の NDIS バージョンでは、NDIS はパケットをミニポートドライバーに送信する前に、各パケットに対してスキャッター gather (SG) リストを取得します。 また、NDIS では、過度な断片化が原因で、SG リストを取得する元の試行が失敗するケースも処理されます。 この場合、NDIS はパケットを連続するバッファーにダブルバッファーし、もう一度実行しようとします。 また、たとえば、データの物理アドレスが32ビットの最大値を超え、NIC が64ビット DMA をサポートしていない場合、NIC がサポートする物理アドレスにデータをダブルバッファーすることもできます。

デッドロック状態を回避するために、NDIS はパケットの SG リストを取得し、一度に1つのパケットを送信します。 NDIS がすべてのパケットをミニポートドライバーに送信する前にマップしようとすると、システムでリソースが不足する可能性があります。 この場合、NDIS はマップレジスタが使用可能になるのを待機していますが、一部のマップレジスタは、送信されていないパケットに対してロックダウンされています。 ロックダウンされたパケットを再利用することはできません。

この SGDMA サポートへのアプローチには、次の制限があります。

-   パケットはミニポートドライバーに送信される前にマップされるため、ドライバーは、サイズの小さいパケットや、断片化が過剰になっているパケットを最適化することはできません。 ミニポートドライバーは、既知の物理アドレスにパケットをダブルバッファーできません。

-   NDIS がミニポートドライバーに渡す物理アドレス配列が元のデータの仮想アドレスにマップされる保証はありません。 このため、ドライバーがデータを送信する前に、MDL チェーン内の仮想アドレスにあるデータを変更した場合、データに加えられた変更は物理アドレスのデータに反映されません。 この場合、NIC は未変更のデータを送信します。

-   NDIS では、リソースの問題によるデッドロックを避けるために、一度に1つのパケットを送信することに制限されています。 これは、複数のパケットを送信するほど効率的ではありません。

-   NDIS はミニポートドライバーの送信機能を判別できないため、SG リストバッファー用の記憶域を事前に割り当てることはできません。 そのため、NDIS は実行時に必要なストレージを割り当てる必要があります。 これは、ストレージの事前ほど効率的ではありません。

-   SG リストを割り当てる HAL 関数は、IRQL = DISPATCH\_レベルで呼び出す必要があります。 NDIS には現在の IRQL 情報が含まれていないため、ディスパッチ\_レベルで既にディスパッチされている場合でも、\_レベルをディスパッチするように IRQL を設定する必要があります。 これは、IRQL がディスパッチ\_レベルで既に存在する場合は効率的ではありません。

## <a name="benefits-of-ndis-sgdma-support"></a>NDIS SGDMA のサポートの利点

Ndis 6.0 以降の SGDMA インターフェイスでは、NDIS はデータバッファーをミニポートドライバーに送信する前にマップしません。 代わりに、NDIS によってドライバーがネットワークデータをマップするためのインターフェイスが提供されます。

この方法では、次のような利点があります。

-   NDIS ではネットワークデータをマップするためのインターフェイスが HAL に提供されるため、NDIS では、マッピングプロセスの複雑さと詳細から、ミニポートドライバーを使用できます。

-   ミニポートドライバーは、マップされる前にデータにアクセスできます。 そのため、元のデータに加えられた変更は、NDIS または HAL によってデータがダブルバッファーされる場合でも、SG リストによって表されるデータに反映されます。

-   ミニポートドライバーを使用すると、既知の物理アドレスを持つ事前割り当て済みのバッファーにコピーすることで、小規模または高度に断片化されたパケットの送信を最適化できます。 この方法では、不要なマッピングが回避されるため、システムのパフォーマンスが向上します。

-   NDIS では、複数のバッファーをミニポートドライバーに安全に送信できます。 その結果、ミニポートドライバーの呼び出しが減り、システムのパフォーマンスが向上します。

-   ミニポートドライバーは、送信記述子ブロックの一部として SG リストのメモリを事前に割り当てることができます。 したがって、NDIS またはミニポートドライバーは、実行時に SG リストにメモリを割り当てる必要はありません。

-   ミニポートドライバーは IRQL = ディスパッチ\_レベルで実行できるため、ポートドライバーは不要な呼び出しを回避して、\_レベルをディスパッチする IRQL を上げることができます。 たとえば、割り込み DPC のコンテキストで送信の完了が発生した場合、ミニポートドライバーは、IRQL を発生させずに SG リストを解放できます。


## <a name="registering-and-deregistering-dma-channels"></a>DMA チャネルの登録と登録解除

NDIS ミニポートドライバーは、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数から[**NdisMRegisterScatterGatherDma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterscattergatherdma)関数を呼び出して、DMA チャネルを ndis に登録します。

ミニポートドライバーは、 *DmaDescription*パラメーターの[**NdisMRegisterScatterGatherDma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterscattergatherdma)に DMA の説明を渡します。 **NdisMRegisterScatterGatherDma**は、スキャッター/ギャザーリストを保持するのに十分な大きさのバッファーのサイズを返します。 ミニポートドライバーは、このサイズを使用して、スキャッター/ギャザーリストの記憶域を事前に割り当てる必要があります。

また、ミニポートドライバーは、NDIS が呼び出す*Miniportxxx*関数のエントリポイントを[**NdisMRegisterScatterGatherDma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterscattergatherdma)に渡して、スキャッター/ギャザーリストを処理します。 MiniportProcessSGList は、HAL がバッファーのスキャッター/ギャザーリストを作成した後に、ミニポートドライバーの[](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_process_sg_list)関数を呼び出します。 **NdisMRegisterScatterGatherDma**は、 *pNdisMiniportDmaHandle*パラメーターにハンドルを提供します。このパラメーターは、ミニポートドライバーが NDIS スキャッター/gather DMA 関数の後続の呼び出しで使用する必要があります。

NDIS ミニポートドライバーは、 [*Miniporthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)関数から[**NdisMDeregisterScatterGatherDma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterscattergatherdma)関数を呼び出して、スキャッター/ギャザー DMA リソースを解放します。

## <a name="allocating-and-freeing-scattergather-lists"></a>スキャッター/ギャザーリストの割り当てと解放

NDIS ミニポートドライバーは、 [*Miniportsendnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)関数で[**NdisMAllocateNetBufferSGList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocatenetbuffersglist)関数を呼び出します。 ミニポートドライバーは、マップする必要がある各[**NET\_BUFFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造体に対して**NdisMAllocateNetBufferSGList**を1回呼び出します。 リソースが使用可能になり、HAL に SG リストが準備できたら、NDIS はドライバーの[*MiniportProcessSGList*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_process_sg_list)関数を呼び出します。 NDIS は、ミニポートドライバーの**NdisMAllocateNetBufferSGList**呼び出しの前または後に*MiniportProcessSGList*を呼び出すことができます。

システムパフォーマンスを向上させるために、スキャッター/ギャザーリストは、関連付けられている[**NET\_BUFFER\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_data)構造の**currentmdl**メンバーで指定された MDL の先頭から始まるネットワークデータから生成されます。 SG リストのネットワークデータの先頭は、関連付けられている**NET\_BUFFER\_データ**構造体の**Currentmdloffset**メンバーに指定された値によって、sg リストの先頭からのオフセットになります。

送信完了の割り込みに対して DPC を処理しているときに、ミニポートドライバーが SG リストを必要としない場合、ミニポートドライバーは[**NdisMFreeNetBufferSGList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreenetbuffersglist)関数を呼び出して、sg リストを解放する必要があります。

NdisMFreeNetBufferSGList を呼び出さないでください。 [](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreenetbuffersglist)は、ドライバーまたはハードウェアが、スキャッター/ギャザーリストに関連付けられている[**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造によって記述されているメモリに引き続きアクセスしていることを  **確認**してください。 

受信したデータにアクセスする前に、ミニポートドライバーは[**NdisMFreeNetBufferSGList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreenetbuffersglist)を呼び出してメモリキャッシュをフラッシュする必要があります。
