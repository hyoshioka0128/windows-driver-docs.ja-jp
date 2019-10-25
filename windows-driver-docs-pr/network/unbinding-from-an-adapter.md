---
title: アダプターからのバインド解除
description: アダプターからのバインド解除
ms.assetid: cea2ce45-df0c-4c75-a780-5810ea01b987
keywords:
- プロトコルドライバー WDK ネットワーク、バインド解除
- NDIS プロトコルドライバー WDK、バインド解除
- アダプター WDK ネットワークからのバインド解除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fad4143ef0f7d18657ae4e94b03687738b01da3a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843017"
---
# <a name="unbinding-from-an-adapter"></a>アダプターからのバインド解除





NDIS は、プロトコルドライバーの[*Protocolunbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex)関数を呼び出して、基になるアダプターからドライバーのバインドを解除するように要求します。 [*Protocolbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)の逆数として、NDIS は*protocolunbindadapterex*を呼び出して、アダプターへのバインドを閉じ、ドライバーによってバインドに割り当てられたリソースを解放します。

*Protocolunbindadapterex*では、プロトコルドライバーは[**NdisCloseAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseadapterex)を呼び出して、基になるアダプターへのバインドを閉じます。 プロトコルドライバーは、 *NdisBindingHandle*パラメーターで指定された[**NdisOpenAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenadapterex)のハンドルを**NdisCloseAdapterEx**渡します。 このハンドルは、NDIS が閉じる必要のあるバインディングを識別します。

プロトコルドライバーは、 *Protocolbindadapterex*関数または*protocolunbindadapterex*関数からアダプターを閉じる必要があります。

プロトコルドライバーがバインディングを閉じる操作を開始する必要がある場合、ドライバーは[**NdisUnbindAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisunbindadapter)を呼び出すことができます。 **NdisUnbindAdapter**は、 *Protocolunbindadapterex*への NDIS 呼び出しを実行する作業項目をスケジュールします。 この作業項目は、 **NdisUnbindAdapter**の呼び出しが返される前に実行できます。 したがって、ドライバーの作成者は、 **NdisUnbindAdapter**がを返すと、バインドハンドルが無効であると想定する必要があります。

プロトコルドライバーが*Protocolunbindadapterex*から保留中の NDIS\_STATUS\_を返した場合、バインド要求を完了するには、最終的な状態で[**NdisCompleteUnbindAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscompleteunbindadapterex)を呼び出す必要があります。

Ndis が NDIS\_STATUS\_**NdisCloseAdapterEx**から PENDING を返した場合、ndis は後でプロトコルドライバーの[*Protocolcloseadaptercompleteex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_close_adapter_complete_ex)関数を呼び出します。

バインドが一時停止状態の場合、NDIS は*Protocolunbindadapterex*を呼び出すことができます。

すべてのバインド解除操作が完了すると、バインドはバインドされていない状態になります。

 

 





