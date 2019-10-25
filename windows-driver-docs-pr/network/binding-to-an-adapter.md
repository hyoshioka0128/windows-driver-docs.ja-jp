---
title: アダプターへのバインド
description: アダプターへのバインド
ms.assetid: 583b7c73-fbc7-4d25-95f7-973cede61ec8
keywords:
- プロトコルドライバー WDK ネットワーク、アダプターへのバインド
- NDIS プロトコルドライバー WDK、アダプターへのバインド
- バインド操作 (WDK ネットワーク)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95b0c9f15e7fb5cc865b5c4b199432b882ec2478
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838215"
---
# <a name="binding-to-an-adapter"></a>アダプターへのバインド





NDIS は、プロトコルドライバーの[*Protocolbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)関数を呼び出して、ドライバーのバインド先となる基になるアダプターが使用可能になるたびにバインドを開きます。 NDIS が*Protocolbindadapterex*を呼び出した後、バインドは開始状態になります。 *オープン*状態では、プロトコルドライバーによってバインドのリソースが割り当てられ、アダプターが開きます。

NDIS が*Protocolbindadapterex*に渡されます。これに加えて、バインド操作の ndis コンテキストと、 [**ndis\_BIND\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)構造体へのポインターが渡されます。 この構造体には、次のようなアダプターに関する情報が含まれています。

-   アダプターの名前。

-   レジストリのプロトコルサービスエントリで、このバインディングに固有のパラメーターのレジストリの場所。

-   アダプターの物理デバイスオブジェクト。

アダプターを開くために、プロトコルドライバーは[**NdisOpenAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenadapterex)関数を呼び出します。 プロトコルドライバーは、次のものを**NdisOpenAdapterEx**に渡します。

-   NDIS が**NdisRegisterProtocolDriver**関数の*NdisProtocolHandle*パラメーターでドライバーに返すハンドル。

-   このバインディングのプロトコルドライバーのコンテキスト。

-   [ **\_パラメーターを開く\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_open_parameters)の構造体へのポインター。

[**NDIS\_open\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_open_parameters)には、 **NdisOpenAdapterEx**が開くアダプターの名前、プロトコルドライバーでサポートされている中程度の種類の配列、およびドライバーがサポートするフレームの種類の配列 (省略可能) などの情報が含まれています。は、このバインディングでを受け取ることができます。

プロトコルドライバーが*Protocolbindadapterex*から保留中の NDIS\_STATUS\_を返した場合、バインド要求を完了するには、最終的な状態で[**NdisCompleteBindAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscompletebindadapterex)を呼び出す必要があります。

Ndis が NDIS\_STATUS\_**NdisOpenAdapterEx**から PENDING を返した場合、ndis は、open 要求が完了した後で、プロトコルドライバーの[*ProtocolOpenAdapterCompleteEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_open_adapter_complete_ex)関数を最後のステータスで呼び出します。

ドライバーがアダプターへのバインドを正常に開くと、バインドは一時停止状態になります。

プロトコルドライバーは、アダプターを閉じるために[**NdisCloseAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseadapterex)関数を呼び出します。 ドライバーは、 *Protocolbindadapterex*関数または[*Protocolunbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex)関数から**NdisCloseAdapterEx**を呼び出すことができます。

アダプターを開いた後にバインド要求を完了する前に、 *Protocolbindadapterex*でエラーが発生し、アダプターへのバインドを閉じる必要があります。これにより、 **NdisCloseAdapterEx**を呼び出すことができます。 アダプターを閉じる方法の詳細については、「[アダプターからのバインド](unbinding-from-an-adapter.md)解除」を参照してください。

 

 





