---
title: NDIS Scatter/Gather DMA
description: NDIS Scatter/Gather DMA
ms.assetid: 70b8321b-7b21-4d11-a9c2-46b0caa26ce6
keywords:
- ミニポート ドライバー WDK スキャッター/ギャザー DMA ネットワーク、
- NDIS ミニポート ドライバー WDK、スキャッター/ギャザー DMA
- スキャッター/ギャザー ネットワーク DMA WDK
- ネットワーク SGDMA WDK
- Nic の WDK ネットワーク、システム メモリの転送
- ネットワーク インターフェイス カードの WDK ネットワー キング、s
ms.date: 06/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: b2ce441905447e1dbabea41dfd879779074583b5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368596"
---
# <a name="ndis-scattergather-dma"></a>NDIS Scatter/Gather DMA

[!include[NDIS DMA ARM note](ndis-dma-arm-note.md)]

NDIS ミニポート ドライバーでは、スキャッター/ギャザー DMA (SGDMA) メソッドを使用して、NIC ドライバーとシステムのメモリの間でデータを転送します。 成功した DMA 転送には、NIC をサポートするアドレス範囲内で指定するデータの物理アドレスが必要です。 HAL は、ドライバー、MDL チェーンの物理アドレスの一覧を取得し、必要に応じてはダブル バッファー データの物理アドレスの範囲のためのメカニズムを提供します。

NDIS 6.0 より前のバージョンの NDIS では、ミニポート ドライバーおよび NDIS SGDMA サポートは、いくつかの点では制限があり、multipacket 送信シナリオでも特に機能しません。 NDIS 6.0 SGDMA サポートは、ミニポート ドライバー用の単純なインターフェイスを提供しながら、これらの制限を克服しています。

## <a name="history-of-ndis-sgdma"></a>NDIS SGDMA の履歴

NDIS 6.0 より前のバージョンの NDIS、NDIS ミニポート ドライバーにパケットを送信する前に散布図 (SG) の収集には、各パケットに対するボックスの一覧を取得します。 NDIS は、過剰な断片化のため、セキュリティ グループの一覧を取得する元の試行が失敗した場合にも処理します。 この場合は、NDIS ダブル バッファーでパケットを連続したバッファーし、もう一度試みます。 HAL こともできますダブル バッファーにデータを 32 ビットの最大値、および NIC 上のデータの物理アドレスは、たとえば場合、は、NIC をサポートする物理アドレスは 64 ビットの DMA をサポートしていません。

デッドロックの状況を避けるためには、NDIS がパケットの場合は、セキュリティ グループの一覧を取得し、一度に 1 つのパケットを送信します。 NDIS ミニポート ドライバーに送信する前にすべてのパケットをマップしようとすると、システム リソースを実行できます。 この場合は、NDIS の場合は、いくつかのマップのレジスタが送信されていないパケットのロック中に使用可能になるマップ レジスタを待機しています。 ロック ダウンされているパケットを再利用することはできません。

SGDMA をサポートするには、このアプローチでは、次の制限があります。

-   ミニポート ドライバーに到達する前に、パケットがマップされているために、ドライバーは、小さなパケットまたは過度に断片化されるパケットの最適化できません。 ミニポート ドライバーには、既知の物理アドレスへのパケットをバッファー double ことはできません。

-   NDIS がミニポート ドライバーに渡された物理アドレスの配列は、元のデータの仮想アドレスにマップされる保証はありません。 そのため、ドライバーは、送信する前に、MDL チェーン内の仮想アドレスにデータを変更する場合、物理アドレス内のデータには、データに加えられた変更は反映されません。 この場合は、NIC は、変更されていないデータを送信します。

-   NDIS は、リソースの問題により、デッドロックを回避するために、一度に 1 つのパケットの送信に制限されます。 複数のパケットを送信するほど効率的ではありません。

-   NDIS は、ミニポート ドライバーの送信機能を特定できないために、セキュリティ グループ一覧バッファ ストレージもあらかじめ割り当てことはできません。 そのため、NDIS は、実行時に必要な記憶域を割り当てる必要があります。 これは、記憶域の事前割り当てほど効率的ではありません。

-   IRQL で、セキュリティ グループの一覧を割り当てる HAL 関数を呼び出す必要がある = ディスパッチ\_レベル。 NDIS はディスパッチに IRQL を設定する必要があるため、現在の IRQL 情報がない\_レベルは、既にディスパッチ場合でも\_レベル。 これは、IRQL が既にディスパッチになっている場合は効率的ではありません\_レベル。

## <a name="benefits-of-ndis-sgdma-support"></a>NDIS SGDMA サポートの利点

NDIS 6.0 とそれ以降の SGDMA インターフェイスでは、NDIS は、ミニポート ドライバーに送信する前に、データ バッファーをマップしません。 代わりに、NDIS ドライバー ネットワーク データをマップするためのインターフェイスを提供します。

このアプローチでは、次の利点が得られます。

-   NDIS は、ネットワーク データをマッピングするため、HAL にインターフェイスを提供、ため NDIS は、ミニポート ドライバーから複雑さとマッピングのプロセスの詳細についてを保護します。

-   ミニポート ドライバーでは、マップされている前に、データへのアクセスがあります。 セキュリティ グループの一覧も場合によって表されるデータに、元のデータに加えられた変更を反映するため、NDIS または HAL ダブル バッファー データ。

-   ミニポート ドライバーでは、既知の物理アドレスを使用して、事前に割り当てられるバッファーにコピーして、小規模または高度に断片化されたパケットの送信を最適化できます。 このアプローチでは、マッピングは必要ありませんし、そのためシステム パフォーマンスが向上を回避できます。

-   NDIS は、ミニポート ドライバーには、複数のバッファーを安全に送信できます。 これによってミニポート ドライバーが少ない呼び出しでなり、したがってシステムのパフォーマンスが向上します。

-   ミニポート ドライバーでは、送信記述子のブロックの一部として、セキュリティ グループの一覧については、メモリを事前ことができます。 そのため、NDIS ミニポート ドライバーでは、実行時にセキュリティ グループ リストのメモリを割り当てる必要はありません。

-   ミニポート ドライバーは、IRQL で実行できるため、= ディスパッチ\_レベル、ミニポート ドライバーにディスパッチ IRQL を発生させるの不要な呼び出しを回避できます\_レベル。 たとえば、この DPC、割り込みのコンテキストでが行われる送信を完了するためミニポート ドライバーは IRQL は生成せずセキュリティ グループの一覧を解放できます。


## <a name="registering-and-deregistering-dma-channels"></a>登録して、DMA チャネルの登録を解除

NDIS ミニポート ドライバーを呼び出す、 [ **NdisMRegisterScatterGatherDma** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterscattergatherdma)関数からその[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数NDIS DMA チャネルを登録します。

ミニポート ドライバーは、DMA の説明を渡します[ **NdisMRegisterScatterGatherDma** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterscattergatherdma)で、 *DmaDescription*パラメーター。 **NdisMRegisterScatterGatherDma**スキャッター/ギャザーの一覧を保持するのに十分な大きさにする必要があるバッファーのサイズを返します。 ミニポート ドライバーでは、スキャッター/ギャザー リストの記憶域を事前に割り当てられるこのサイズを使用する必要があります。

ミニポート ドライバーにも渡す[ **NdisMRegisterScatterGatherDma** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterscattergatherdma)エントリ ポイントを*MiniportXxx*関数呼び出し、NDIS、スキャッター/ギャザーの処理リスト。 NDIS ミニポート ドライバーの呼び出す[ *MiniportProcessSGList* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_process_sg_list) HAL がバッファーのスキャッター/ギャザーのリストをビルドした後に機能します。 **NdisMRegisterScatterGatherDma**にハンドルを提供、 *pNdisMiniportDmaHandle*パラメーターで、ミニポート ドライバーは、NDIS スキャッター/ギャザー DMA 関数への後続の呼び出しで使用する必要があります。

NDIS ミニポート ドライバーを呼び出す、 [ **NdisMDeregisterScatterGatherDma** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismderegisterscattergatherdma)関数からその[ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)関数スキャッター/ギャザー DMA のリソースを解放します。

## <a name="allocating-and-freeing-scattergather-lists"></a>割り当てと解放のスキャッター/ギャザー リスト

NDIS ミニポート ドライバーを呼び出す、 [ **NdisMAllocateNetBufferSGList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismallocatenetbuffersglist)関数でその[ *MiniportSendNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_send_net_buffer_lists)関数。 ミニポート ドライバー呼び出し**NdisMAllocateNetBufferSGList**ごとに 1 回[ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)構造にマップする必要があります。 NDIS がドライバーを呼び出し、リソースが利用可能になるし、HAL がセキュリティ グループ一覧の準備ができて、 [ *MiniportProcessSGList* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_process_sg_list)関数。 NDIS を呼び出すことができます*MiniportProcessSGList*ミニポート ドライバーの呼び出しの前後に**NdisMAllocateNetBufferSGList**を返します。

システムのパフォーマンスを向上させる、スキャッター/ギャザー リストがで指定された MDL の早い段階でネットワーク データから生成された、 **CurrentMdl** 、関連付けられているメンバー [ **NET\_バッファー\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_data)構造体。 指定した値によって SG リストの先頭からセキュリティ グループの一覧でネットワーク データの先頭のオフセット、 **CurrentMdlOffset** 、関連付けられているメンバー **NET\_バッファー\_データ**構造体。

ミニポート ドライバーがセキュリティ グループの一覧をこれ以上必要ありませんの前後の送信完了の割り込み、DPC を処理中に、ミニポート ドライバーを呼び出す必要があります、 [ **NdisMFreeNetBufferSGList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismfreenetbuffersglist)を解放する関数、セキュリティ グループの一覧です。

**注**  呼び出さない[ **NdisMFreeNetBufferSGList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismfreenetbuffersglist)ドライバーやハードウェアがまだメモリへのアクセスで説明されているときに、 [ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)スキャッター/ギャザー リストに関連付けられている構造体。 

受信したデータにアクセスする前に、ミニポート ドライバーを呼び出す必要があります[ **NdisMFreeNetBufferSGList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismfreenetbuffersglist)メモリ キャッシュをフラッシュします。
