---
title: ドライバースタックの停止
description: ドライバースタックの停止
ms.assetid: 2ecc0ebb-89d8-4cd8-ac1c-f9f1da7d2ca8
keywords:
- ドライバースタック WDK ネットワーク、停止
- ドライバースタックの停止 WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 751d41d189ca38d177731ff673913b5c3c659aaf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841822"
---
# <a name="stopping-a-driver-stack"></a>ドライバースタックの停止





デバイスが削除されると、NDIS はドライバースタックを停止します。 ドライバースタック停止操作は次のように実行される。

1.  NDIS はドライバースタックを一時停止します。 ドライバースタックの一時停止の詳細については、「[ドライバースタックの一時停止](pausing-a-driver-stack.md)」を参照してください。

2.  NDIS は、プロトコルドライバーの[*Protocolunbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex)関数を呼び出します。

    バインディングは、終了状態になります。 未処理の OID と送信要求が完了し、すべての受信データが返されると、バインドはバインドされていない状態になります。

3.  NDIS は、スタックの一番上から順に移動し、ミニポートドライバーにダウンして、すべてのフィルターモジュールをデタッチします。

    NDIS がフィルタードライバーの[*Filterdetach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_detach)関数を呼び出し、フィルタードライバーがフィルターモジュールのすべてのリソースを解放すると、フィルターモジュールはデタッチされた状態になります。

4.  NDIS はミニポートアダプターを停止します。

    NDIS がミニポートドライバーの[*Miniporthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)関数を呼び出した後、ミニポートドライバーはミニポートアダプターのすべてのリソースを解放し、ミニポートアダプターは停止状態になります。

5.  フィルタードライバーのすべてのモジュールがデタッチされている場合、システムはフィルタードライバーをアンロードできます。

6.  ミニポートドライバーが管理するすべてのミニポートアダプターが停止している場合、システムはミニポートドライバーをアンロードできます。

 

 





