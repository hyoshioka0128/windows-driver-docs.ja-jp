---
title: インターフェイスをプロバイダーとして登録します。
description: インターフェイスをプロバイダーとして登録します。
ms.assetid: 7eb4b86d-077a-48de-94b6-11906e847569
keywords:
- NDIS ネットワーク インターフェイス、WDK インターフェイス プロバイダー
- ネットワーク インターフェイス、WDK インターフェイス プロバイダー
- インターフェイス プロバイダー WDk のネットワーク インターフェイス
- インターフェイス プロバイダーを登録します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb5c2189951c1fdc7c49c244c95df022f20c22ac
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552370"
---
# <a name="registering-as-an-interface-provider"></a>インターフェイスをプロバイダーとして登録します。





NDIS インターフェイス プロバイダーは、提供し、NDIS ネットワーク インターフェイスの情報を管理するソフトウェア コンポーネントです。 たとえば、プロトコル ドライバー、MUX の中間ドライバーおよび NDIS インターフェイス プロバイダーには。 (NDIS プロキシを提供インターフェイス プロバイダー ミニポート ドライバーとフィルター ドライバー。 ただし、ミニポート ドライバーとフィルター ドライバーもできるインターフェイス プロバイダー。)各インターフェイス プロバイダーを呼び出す、 [ **NdisIfRegisterProvider** ](https://msdn.microsoft.com/library/windows/hardware/ff562716)ネットワーク インターフェイスのプロバイダーとして登録する関数。

場合に呼び出し**NdisIfRegisterProvider**成功すると、 **NdisIfRegisterProvider**ハンドルのアドレスを返します、 *pNdisProviderHandle*パラメーターを指定します。 呼び出し元は、後続の呼び出し (たとえば、インターフェイスを登録する場合など) で、このハンドルを使用します。 *ProviderCharacteristics*パラメーターが指す、 [ **NDIS\_場合\_プロバイダー\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565728)構造体OID のクエリを処理し、要求を設定するプロバイダーのエントリ ポイントが含まれています。 NDIS\_場合\_プロバイダー\_特性には、次が含まれています。 クエリを実行し、関数の設定。

-   [**ProviderQueryObject**](https://msdn.microsoft.com/library/windows/hardware/ff570399)

-   [**ProviderSetObject**](https://msdn.microsoft.com/library/windows/hardware/ff570403)

プロバイダーのインターフェイスの詳細についてはクエリを実行し、ハンドラーの設定を参照してください[OID クエリの処理および NDIS インターフェイス プロバイダーでの要求の設定](handling-oid-query-and-set-requests-in-an-ndis-interface-provider.md)します。

NDIS ドライバーを呼び出すことができます、 [ **NdisIfDeregisterProvider** ](https://msdn.microsoft.com/library/windows/hardware/ff562703)ネットワーク インターフェイスのプロバイダーとしての登録を解除する関数。 たとえば、インターフェイス プロバイダーとしては、読み込まれていないときに、NDIS ドライバーを登録解除する必要があります。 インターフェイスをプロバイダーを呼び出す前に登録されているすべてのインターフェイスがないことを確認する必要があります**NdisIfDeregisterProvider**します。 プロバイダーはプロバイダー ハンドルに渡されることを使用する必要があります、 *NdisProviderHandle*パラメーターの**NdisIfDeregisterProvider**呼び出した後**NdisIfDeregisterProvider**.

 

 





