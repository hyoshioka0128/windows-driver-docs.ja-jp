---
title: ミニポート アダプターの初期化
description: ミニポート アダプターの初期化
ms.assetid: 6d7a23dc-cc09-46d3-89d3-34e8e8f17a51
keywords:
- ミニポート アダプタ WDK ネットワーク、初期化しています
- アダプタ WDK ネットワーク、初期化しています
- ミニポート アダプタの初期化
- WDK ネットワークの状態を初期化しています
- MiniportInitializeEx
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3433a48f2db627b6fe8fa5ce0392edb4679927ef
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383691"
---
# <a name="initializing-a-miniport-adapter"></a>ミニポート アダプターの初期化





ネットワーク デバイスが使用可能になるときに、システムは、既に読み込まれていない場合、必要なの NDIS ミニポート ドライバーを読み込みます。 その後、プラグ アンド プレイ (PnP) マネージャーは、プラグ アンド プレイ デバイスを起動する IRP NDIS 送信します。 NDIS ミニポート ドライバーを呼び出す[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)ネットワーク I/O 操作用のアダプターを初期化します。 NDIS を呼び出すことができます*MiniportInitializeEx*ドライバーが初期化された後、いつでもできます。 ミニポート ドライバーの初期化の詳細については、次を参照してください。[ミニポート ドライバーの初期化](initializing-a-miniport-driver.md)します。

まで[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize) NDIS が初期化されているアダプターの要求を送信しないを返します。 アダプターは、初期化状態です。

ミニポート ドライバーが通常では、次のタスクを実行します[ *MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize):

1.  アダプターの構成情報を取得します。

2.  アダプターのハードウェア リソースについての情報を取得します。

3.  呼び出し、 [ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)し、アダプターに関連付けられている次の属性を提供します。
    -   コンテキストのドライバーに割り当てられた領域へのポインター。
    -   適切な属性フラグ。
    -   呼び出し元のタイムアウト間隔、 [ *MiniportCheckForHangEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_check_for_hang)関数。
    -   インターフェイスの型。

4.  アダプターに固有のリソースを初期化します。

ミニポート ドライバーはアダプターの属性を指定します、 [ **NDIS\_ミニポート\_アダプター\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_attributes)構造体[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)に渡す[ **NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)します。

通常、 [ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)次の順序でアダプターに固有のリソースを割り当てます。

1.  非ページ プール メモリ。

2.  [**NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)と[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)プール (を参照してください[ミニポート ドライバーの送信と受信操作](miniport-driver-send-and-receive-operations.md))。

3.  ロックをスピンします。

4.  タイマー。

5.  IO ポート。

6.  DMA (を参照してください[スキャッター/ギャザー DMA](scatter-gather-dma2.md))。

7.  共有メモリです。

8.  中断 (を参照してください[管理の割り込み](managing-interrupts.md))。

後[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)アダプターが一時停止状態に正常に返されます。 NDIS を呼び出すことができます、 [ **MiniportRestart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_restart)アダプターは実行中の状態を遷移する関数。 詳細については、次を参照してください。[ミニポート アダプター開始](starting-an-adapter.md)します。

場合[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)返します NDIS\_状態\_成功すると、ドライバーは、アダプターでのすべてのリソースを解放する必要があります、 [ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)関数。 詳細については、次を参照してください。[ミニポート アダプターを停止する](halting-a-miniport-adapter.md)します。

場合[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)失敗、 *MiniportInitializeEx*と返されますアダプターは、中止の状態を返します前に、割り当てられているすべてのリソースを解放する必要があります.

## <a name="related-topics"></a>関連トピック


[ミニポート アダプターを停止します。](halting-a-miniport-adapter.md)

[ミニポート アダプタの状態と操作](miniport-adapter-states-and-operations.md)

[ミニポート ドライバーの送信し、受信操作](miniport-driver-send-and-receive-operations.md)

[DMA のスキャッター/ギャザー](scatter-gather-dma2.md)

[ミニポート アダプタの開始](starting-an-adapter.md)

 

 






