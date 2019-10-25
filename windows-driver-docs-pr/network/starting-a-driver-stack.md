---
title: ドライバー スタックの起動
description: ドライバー スタックの起動
ms.assetid: 316de69e-38e8-4ac6-83c5-5d13090ee6d5
keywords:
- ドライバースタック WDK ネットワーク、開始
- ドライバースタックを開始する WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d9b38e466ee2de74d42c7ffa6e88c89b2170396
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841836"
---
# <a name="starting-a-driver-stack"></a>ドライバー スタックの起動





システムによってネットワークデバイスが検出されると、そのデバイスの NDIS ドライバースタックが開始されます。 デバイスには、仮想デバイスまたは物理デバイスを使用できます。 どちらの場合も、ドライバースタックの開始操作は次のように進行します。

1.  ドライバーがまだ読み込まれていない場合は、ドライバーが読み込まれ、初期化されます。

    ドライバーは特定の順序で読み込まれません。

2.  システムは、各ドライバーの**Driverentry**関数を呼び出します。

    **Driverentry**が戻ると、次のようになります。

    -   デバイスのミニポートアダプターが停止状態になっています。
    -   フィルターモジュールはデタッチされた状態です。
    -   プロトコルバインドはバインドされていない状態です。

3.  システムは、ミニポートアダプターを開始するように NDIS に要求します。

    ミニポートアダプターを初期化するために、NDIS はミニポートドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出します。 *MiniportInitializeEx*が成功すると、ミニポートアダプターは一時停止状態になります。

4.  NDIS は、ミニポートドライバーに最も近いモジュールから開始し、ドライバースタックの一番上まで進んで、フィルターモジュールをアタッチします。

    ドライバースタックにフィルターモジュールをアタッチするようにドライバーに要求するために、NDIS はフィルタードライバーの[*Filterattach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)関数を呼び出します。 各アタッチ操作が成功した場合、フィルターモジュールは一時停止状態になります。

5.  基になるすべてのドライバーが一時停止状態になると、NDIS はプロトコルドライバーの[*Protocolbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)関数を呼び出します。

    次に、プロトコルドライバーのバインドが開始状態になります。 プロトコルドライバーは、 [**NdisOpenAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenadapterex)関数を呼び出して、ミニポートアダプターでバインドを開きます。

6.  NDIS は、バインドに必要なリソースを割り当て、プロトコルドライバーの[*ProtocolOpenAdapterCompleteEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_open_adapter_complete_ex)関数を呼び出します。

    バインドは一時停止状態になります。

7.  バインド操作を完了するために、プロトコルドライバーは[**NdisCompleteBindAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscompletebindadapterex)関数を呼び出します。

8.  NDIS はドライバースタックを再起動します。 ドライバースタックの再起動の詳細については、「[ドライバースタックの再起動](restarting-a-driver-stack.md)」を参照してください。

 

 





