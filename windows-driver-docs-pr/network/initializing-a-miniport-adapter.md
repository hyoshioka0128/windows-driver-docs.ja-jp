---
title: ミニポート アダプターの初期化
description: ミニポート アダプターの初期化
ms.assetid: 6d7a23dc-cc09-46d3-89d3-34e8e8f17a51
keywords:
- ミニポートアダプター WDK ネットワーク、初期化
- アダプタ WDK ネットワーク, 初期化
- ミニポートアダプターの初期化
- 状態 WDK ネットワークを初期化しています
- MiniportInitializeEx
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d605fee54fccb3faf35249c39ca5275f2e0fe995
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824595"
---
# <a name="initializing-a-miniport-adapter"></a>ミニポート アダプターの初期化





ネットワークデバイスが使用可能になると、システムは必要な NDIS ミニポートドライバーを読み込みます (まだ読み込まれていない場合)。 その後、プラグアンドプレイ (PnP) マネージャーは、デバイスを起動するために NDIS a プラグアンドプレイ IRP を送信します。 NDIS は、ミニポートドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出して、ネットワーク i/o 操作用のアダプターを初期化します。 NDIS は、ドライバーが初期化された後、いつでも*MiniportInitializeEx*を呼び出すことができます。 ミニポートドライバーの初期化の詳細については、「[ミニポートドライバーの初期化](initializing-a-miniport-driver.md)」を参照してください。

[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)が返されるまで、NDIS は初期化されているアダプターに対して要求を送信しません。 アダプターは初期化中です。

ミニポートドライバーは、通常、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)で次のタスクを実行します。

1.  アダプターの構成情報を取得します。

2.  アダプターのハードウェアリソースに関する情報を取得します。

3.  [**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)を呼び出し、アダプターに関連付けられている次の属性を提供します。
    -   ドライバーによって割り当てられたコンテキスト領域へのポインター。
    -   適切な属性フラグ。
    -   [*MiniportCheckForHangEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_check_for_hang)関数を呼び出すタイムアウト間隔。
    -   インターフェイス型。

4.  アダプター固有のリソースを初期化します。

ミニポートドライバーは、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)によって[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)に渡される、 [**NDIS\_ミニポート\_アダプター\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_attributes)構造のアダプター属性を指定します。

通常、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)は次の順序でアダプター固有のリソースを割り当てます。

1.  非ページプールメモリ。

2.  [**Net\_buffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)と[**net\_buffer\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)プール (「[ミニポートドライバーの送受信操作](miniport-driver-send-and-receive-operations.md)」を参照してください)。

3.  スピンロック。

4.  タイ.

5.  IO ポート。

6.  DMA (「[スキャッター/GATHER dma](scatter-gather-dma2.md)」を参照)。

7.  共有メモリ。

8.  割り込み (「[割り込みの管理](managing-interrupts.md)」を参照してください)。

[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)が正常に返されると、アダプターは一時停止状態になります。 NDIS は、 [**Miniportrestart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_restart)関数を呼び出して、アダプターを実行中の状態に遷移させることができます。 詳細については、「[ミニポートアダプターの開始](starting-an-adapter.md)」を参照してください。

[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)が NDIS\_STATUS\_SUCCESS を返した場合、ドライバーは[*Miniporthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)関数でアダプターのすべてのリソースを解放する必要があります。 詳細については、「[ミニポートアダプターの停止](halting-a-miniport-adapter.md)」を参照してください。

[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)が失敗した場合、 *MiniportInitializeEx*は、それが返される前に割り当てられたすべてのリソースを解放する必要があり、アダプターは停止状態に戻ります。

## <a name="related-topics"></a>関連トピック


[ミニポートアダプターの停止](halting-a-miniport-adapter.md)

[ミニポートアダプターの状態と操作](miniport-adapter-states-and-operations.md)

[ミニポートドライバーの送信と受信の操作](miniport-driver-send-and-receive-operations.md)

[スキャッター/ギャザー DMA](scatter-gather-dma2.md)

[ミニポートアダプターの開始](starting-an-adapter.md)

 

 






