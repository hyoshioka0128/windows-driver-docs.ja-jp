---
title: インターフェイス プロバイダーとしての登録
description: インターフェイス プロバイダーとしての登録
ms.assetid: 7eb4b86d-077a-48de-94b6-11906e847569
keywords:
- NDIS ネットワークインターフェイス WDK、インターフェイスプロバイダー
- ネットワークインターフェイス WDK、インターフェイスプロバイダー
- インターフェイスプロバイダーの WDk ネットワークインターフェイス
- インターフェイスプロバイダーの登録
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e2c8281920f82345770ecb368206308d1f131c9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842084"
---
# <a name="registering-as-an-interface-provider"></a>インターフェイス プロバイダーとしての登録





NDIS インターフェイスプロバイダーは、NDIS ネットワークインターフェイスの情報を提供して管理するソフトウェアコンポーネントです。 たとえば、プロトコルドライバー、MUX 中間ドライバー、および NDIS はインターフェイスプロバイダーです。 (NDIS は、ミニポートドライバーおよびフィルタードライバー用のプロキシインターフェイスプロバイダーを提供します。 ただし、ミニポートドライバーとフィルタードライバーをインターフェイスプロバイダーにすることもできます)。各インターフェイスプロバイダーは、 [**NdisIfRegisterProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifregisterprovider)関数を呼び出して、ネットワークインターフェイスプロバイダーとして登録します。

**NdisIfRegisterProvider**への呼び出しが成功した場合、 **NdisIfRegisterProvider**は、 *pndisproviderhandle*パラメーターが指定したアドレスにハンドルを返します。 呼び出し元は、後続の呼び出しでこのハンドルを使用します (たとえば、インターフェイスを登録する場合)。 *Providercharacteristics 特性*パラメーターは、プロバイダーのエントリポイントを含む[ **\_\_プロバイダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_if_provider_characteristics)が OID クエリおよび set 要求を処理する場合に、NDIS\_を指します。 \_プロバイダー\_の特性に次のクエリおよびセット関数が含まれている場合、NDIS\_ます。

-   [**ProviderQueryObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-if_query_object)

-   [**ProviderSetObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-if_set_object)

インターフェイスプロバイダーのクエリおよびセットハンドラーの詳細については、「 [NDIS インターフェイスプロバイダーでの OID クエリおよび Set 要求の処理](handling-oid-query-and-set-requests-in-an-ndis-interface-provider.md)」を参照してください。

NDIS ドライバーは、 [**NdisIfDeregisterProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifderegisterprovider)関数を呼び出して、ネットワークインターフェイスプロバイダーとして登録を解除できます。 たとえば、NDIS ドライバーは、アンロードされるときに、インターフェイスプロバイダーとして登録を解除する必要があります。 インターフェイスプロバイダーは、 **NdisIfDeregisterProvider**を呼び出す前に、インターフェイスが登録されていないことを確認する必要があります。 プロバイダーは、 **NdisIfDeregisterProvider**を呼び出した後、 **NdisIfDeregisterProvider**の*NdisProviderHandle*パラメーターで渡されたプロバイダーハンドルを使用することはできません。

 

 





