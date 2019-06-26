---
title: インターフェイス プロバイダーとしての登録
description: インターフェイス プロバイダーとしての登録
ms.assetid: 7eb4b86d-077a-48de-94b6-11906e847569
keywords:
- NDIS ネットワーク インターフェイス、WDK インターフェイス プロバイダー
- ネットワーク インターフェイス、WDK インターフェイス プロバイダー
- インターフェイス プロバイダー WDk のネットワーク インターフェイス
- インターフェイス プロバイダーを登録します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f152e5ba02a9706888643f6112c2f59044af32d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374777"
---
# <a name="registering-as-an-interface-provider"></a>インターフェイス プロバイダーとしての登録





NDIS インターフェイス プロバイダーは、提供し、NDIS ネットワーク インターフェイスの情報を管理するソフトウェア コンポーネントです。 たとえば、プロトコル ドライバー、MUX の中間ドライバーおよび NDIS インターフェイス プロバイダーには。 (NDIS プロキシを提供インターフェイス プロバイダー ミニポート ドライバーとフィルター ドライバー。 ただし、ミニポート ドライバーとフィルター ドライバーもできるインターフェイス プロバイダー。)各インターフェイス プロバイダーを呼び出す、 [ **NdisIfRegisterProvider** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifregisterprovider)ネットワーク インターフェイスのプロバイダーとして登録する関数。

場合に呼び出し**NdisIfRegisterProvider**成功すると、 **NdisIfRegisterProvider**ハンドルのアドレスを返します、 *pNdisProviderHandle*パラメーターを指定します。 呼び出し元は、後続の呼び出し (たとえば、インターフェイスを登録する場合など) で、このハンドルを使用します。 *ProviderCharacteristics*パラメーターが指す、 [ **NDIS\_場合\_プロバイダー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_if_provider_characteristics)構造体OID のクエリを処理し、要求を設定するプロバイダーのエントリ ポイントが含まれています。 NDIS\_場合\_プロバイダー\_特性には、次が含まれています。 クエリを実行し、関数の設定。

-   [**ProviderQueryObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-if_query_object)

-   [**ProviderSetObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-if_set_object)

プロバイダーのインターフェイスの詳細についてはクエリを実行し、ハンドラーの設定を参照してください[OID クエリの処理および NDIS インターフェイス プロバイダーでの要求の設定](handling-oid-query-and-set-requests-in-an-ndis-interface-provider.md)します。

NDIS ドライバーを呼び出すことができます、 [ **NdisIfDeregisterProvider** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifderegisterprovider)ネットワーク インターフェイスのプロバイダーとしての登録を解除する関数。 たとえば、インターフェイス プロバイダーとしては、読み込まれていないときに、NDIS ドライバーを登録解除する必要があります。 インターフェイスをプロバイダーを呼び出す前に登録されているすべてのインターフェイスがないことを確認する必要があります**NdisIfDeregisterProvider**します。 プロバイダーはプロバイダー ハンドルに渡されることを使用する必要があります、 *NdisProviderHandle*パラメーターの**NdisIfDeregisterProvider**呼び出した後**NdisIfDeregisterProvider**.

 

 





