---
title: ドライバー スタックの起動
description: ドライバー スタックの起動
ms.assetid: 316de69e-38e8-4ac6-83c5-5d13090ee6d5
keywords:
- ドライバー スタックの WDK ネットワーク、開始
- 開始ドライバー スタックの WDK ネットワー キング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37d75c5675fc16e9bcbe390538346cd5e0aa8e71
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377566"
---
# <a name="starting-a-driver-stack"></a>ドライバー スタックの起動





ネットワーク デバイスが検出されると、システム、デバイス用の NDIS ドライバー スタックが開始されます。 デバイスには、仮想デバイスまたは物理デバイスを指定できます。 どちらの場合はドライバー スタック操作をよう開始します。

1.  システムでは、読み込みを既に読み込まれていない場合に、ドライバーを初期化します。

    特定の順序で、ドライバーは読み込まれません。

2.  システム呼び出しの各ドライバーの**DriverEntry**関数。

    後**DriverEntry**を返します。

    -   デバイスのミニポート アダプターは、中止状態です。
    -   フィルター モジュールでは、デタッチされた状態にします。
    -   プロトコルのバインドは、非連結状態です。

3.  システムでは、NDIS ミニポート アダプタの開始を要求します。

    NDIS ミニポート アダプターを初期化するために、ミニポート ドライバーが呼び出す[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数。 場合*MiniportInitializeEx*が成功すると、ミニポート アダプターが一時停止状態です。

4.  NDIS は、以降では、ミニポート ドライバーに最も近いモジュールとドライバー スタックの先頭に進行して、フィルター モジュールをアタッチします。

    NDIS フィルター ドライバーの呼び出しはドライバー スタックにフィルター モジュールをアタッチするドライバーを要求する[ *FilterAttach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_attach)関数。 各アタッチ操作が成功すると、フィルター モジュールは、一時停止状態になります。

5.  基になるすべてのドライバーは、一時停止状態では、NDIS 呼び出してプロトコル ドライバーの[ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)関数。

    ドライバーのプロトコル バインド Opening 状態に遷移します。 プロトコル ドライバーの呼び出し、 [ **NdisOpenAdapterEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisopenadapterex)ミニポート アダプターを使用したバインディングを開きます。

6.  バインディングのために必要なリソースの割り当ての NDIS および呼び出しプロトコル ドライバーの[ *ProtocolOpenAdapterCompleteEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_open_adapter_complete_ex)関数。

    バインディングは、一時停止状態になります。

7.  プロトコル ドライバーの呼び出し、バインド操作を完了する、 [ **NdisCompleteBindAdapterEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscompletebindadapterex)関数。

8.  NDIS は、ドライバー スタックを再起動します。 ドライバー スタックの再起動に関する詳細については、次を参照してください。[ドライバー スタックの再起動](restarting-a-driver-stack.md)します。

 

 





