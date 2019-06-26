---
title: ドライバー スタックの停止
description: ドライバー スタックの停止
ms.assetid: 2ecc0ebb-89d8-4cd8-ac1c-f9f1da7d2ca8
keywords:
- ドライバー スタック WDK ネットワークは、停止しています
- ドライバー スタックの WDK ネットワークの停止
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bce966f2bcdfd658155cabb8beb82dbc02d7f4dd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383597"
---
# <a name="stopping-a-driver-stack"></a>ドライバー スタックの停止





デバイスが削除されると、NDIS ドライバー スタックは停止します。 ドライバー スタックは、次のように操作を停止します。

1.  NDIS は、ドライバー スタックを一時停止します。 ドライバー スタックを一時停止の詳細については、次を参照してください。[ドライバー スタックを一時停止](pausing-a-driver-stack.md)します。

2.  NDIS 呼び出しプロトコル ドライバーの[ *ProtocolUnbindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_unbind_adapter_ex)関数。

    バインディングは、終了状態になります。 未処理の OID と送信要求が完了して、すべての受信データが返されると、バインディングは連結なし状態になります。

3.  NDIS は、スタックの先頭から開始し、ミニポート ドライバーに進行してすべてのフィルター モジュールをデタッチします。

    NDIS フィルター ドライバーを呼び出してから[ *FilterDetach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_detach)関数とフィルター ドライバーは、フィルター モジュールのすべてのリソースを解放、フィルター モジュールがデタッチされた状態にします。

4.  NDIS は、ミニポート アダプターが停止します。

    NDIS ミニポート ドライバーを呼び出してから[ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)関数、ミニポート ドライバー ミニポート アダプタとミニポート アダプタ用のリソースは、中止の状態がすべて解放します。

5.  すべてのフィルター ドライバーのモジュールがデタッチされている場合、システムは、フィルター ドライバーをアンロードできます。

6.  ミニポート ドライバーを管理するすべてのミニポート アダプターが停止した場合、システムは、ミニポート ドライバーをアンロードできます。

 

 





