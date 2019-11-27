---
title: アドレス ファミリの登録と開始
description: アドレス ファミリの登録と開始
ms.assetid: 2249adf9-2876-4442-be94-1a966d3f1c88
keywords:
- アドレスファミリ WDK ネットワーク
- AFs WDK ネットワーク
- アドレスファミリの登録
- アドレスファミリを開く
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 912909cf2a8de29ab5e059d7ce2abf945f2e0599
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842089"
---
# <a name="registering-and-opening-an-address-family"></a>アドレス ファミリの登録と開始





呼び出しマネージャーは、接続指向クライアントにコールマネージャーサービスを提供する各 NIC のアドレスファミリを登録する必要があります。 同様に、MCM ドライバーは、管理する NIC のアドレスファミリを登録する必要があります。

アドレスファミリを登録すると、呼び出しマネージャーまたは MCM ドライバーによって、NDIS は、アダプターにバインドされているすべての接続指向クライアントに、呼び出しマネージャーまたは MCM ドライバーのサービスを提供します。

接続指向クライアントで、コールマネージャーまたは MCM ドライバーによって提供されるサービスを使用できる場合は、通話マネージャーまたは MCM ドライバーを使用してアドレスファミリを開くことができます。

### <a name="registering-an-address-family-from-a-call-manager"></a>通話マネージャーからのアドレスファミリの登録

[*Protocolbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)関数を[**NdisOpenAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenadapterex)を使用して基になるミニポートドライバーにバインドした後、呼び出しマネージャーは[**NdisCmRegisterAddressFamilyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmregisteraddressfamilyex)を呼び出して、バインドのアドレスファミリを登録します (次の図を参照)。).

![通話マネージャーを使用したアドレスファミリの登録とオープンを示す図](images/cm-01.png)

**NdisCmRegisterAddressFamilyEx**を呼び出すと、呼び出しマネージャー固有のシグナリングサービスがアドバタイズされます。 呼び出しマネージャーは、 *Protocolbindadapterex*関数が呼び出され、 [**NdisOpenAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenadapterex)を使用して NIC に正常にバインドされるたびに、アドレスファミリを登録する必要があります。

コールマネージャーは、バインドされているすべてのミニポートドライバーで複数のアドレスファミリをサポートできます。 また、呼び出しマネージャーは、1つの NIC で1つ以上のアドレスファミリをサポートすることもできます。 呼び出しマネージャーは、バインドの各アドレスファミリに対して同じエントリポイントを登録する必要があります。 特定の種類のアドレスファミリは、特定のミニポートドライバーにバインドされているクライアントに対して1つしかサポートできません。 呼び出しマネージャーのエントリポイントの登録の詳細については、「 [Condis 登録](condis-registration.md)」を参照してください。

### <a name="registering-an-address-family-from-an-mcm-driver"></a>MCM ドライバーからのアドレスファミリの登録

MCM ドライバーは、そのミニポートドライバーエントリポイントを[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)に登録した後、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数から**NdisMCmRegisterAddressFamilyEx**を呼び出します。 レジストリポイントの詳細については、「」を参照し[てください。](condis-registration.md) MCM ドライバーは、 [**NdisMCmRegisterAddressFamilyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmregisteraddressfamilyex)を1回呼び出して、そのサービスを接続指向クライアントに提供します (次の図を参照してください)。

![mcm ドライバーを使用したアドレスファミリの登録とオープンを示す図](images/fig1-01.png)

オンボード接続指向の信号サポートを備えた NIC のミニポートドライバーは、コールマネージャーが使用可能な場合でも、それ自体を MCM ドライバーとして登録できます。 このようにすることで、このような MCM ドライバーは、その NIC の呼び出しマネージャーとしてプリエンプションを呼び出します。

### <a name="opening-an-address-family"></a>アドレスファミリを開く

呼び出しマネージャーまたは MCM ドライバーの**ndis (M) CmRegisterAddressFamily**呼び出しによって、ndis はバインド上の各接続指向クライアントの[**Protocolcoafregisternotify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_af_register_notify)関数を呼び出します (前の2つの図を参照)。

*Protocolcoafregisternotify*は、アドレスファミリデータを調べて、クライアントがこの特定の CM または mcm ドライバーのサービスを使用できるかどうかを判断します。 クライアントが (M) CM によって指定されたアドレスファミリデータを変更できるかどうかは、呼び出しマネージャーまたは MCM ドライバーの特定のシグナリングプロトコルのサポートに依存します。

提供されている呼び出し管理サービスがクライアントによって検出された場合、 *Protocolcoafregisternotify*はクライアントに AF コンテキスト領域を割り当て、 [**NdisClOpenAddressFamilyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclopenaddressfamilyex)を呼び出します。 **NdisClOpenAddressFamilyEx**は、クライアントの接続指向エントリポイントを NDIS に登録しません。 接続指向エントリポイントを NDIS に登録する方法の詳細については、「 [Condis 登録](condis-registration.md)」を参照してください。

**NdisClOpenAddressFamilyEx**を呼び出すと、NDIS によって、呼び出しマネージャーまたは mcm ドライバーの[**protocolcmoを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_open_af)呼び出すことができます (前の2つの図を参照)。 *Protocolcmoの af*は、クライアントが有効なアドレスファミリで渡されたことを確認し、アドレスファミリのこのインスタンスを開いているクライアントに代わって操作を実行するために必要なリソースを割り当てて初期化します。 *ProtocolcmoNdisAfHandle*は、オープンアドレスファミリの呼び出しマネージャーとクライアントの関連付けを表す、NDIS によって提供されるも格納します。

*Protocolcmoの af*は、同期的または非同期的に完了できます。 非同期的に完了するために[ **、呼び出しマネージャー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmopenaddressfamilycomplete)の*ProtocolcmoNdisCmOpenAddressFamilyComplete af*関数は、を呼び出します。MCM ドライバーの*ProtocolcmoNdisMCmOpenAddressFamilyComplete af*関数は、 [](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmopenaddressfamilycomplete)を呼び出します。 **Ndis (M) CmOpenAddressFamilyComplete**を呼び出すと、ndis は、もともと**NdisClOpenAddressFamilyEx**と呼ばれていたクライアントの*ProtocolOpenAfComplete*関数を呼び出します。

クライアントの**NdisClOpenAddressFamilyEx**への呼び出しが成功した場合、NDIS は、open address ファミリの呼び出しマネージャーとクライアントの関連付けを表す*NdisAfHandle*をクライアントに返します。

クライアントが着信呼び出しを受け入れる場合は、通常、 [**NdisClOpenAddressFamilyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclopenaddressfamilyex)への呼び出しが成功した後に[**NdisClRegisterSap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclregistersap)を呼び出すことによって、 *Protocolclo afcompleteex*関数から[1 つ](registering-a-sap.md)以上の sap を登録します。

クライアントが発信呼び出しを行う場合、発信呼び出しを行うために1つまたは複数のクライアントからの要求を想定して、その*Protocolcloの*関数に[1 つ](creating-a-vc.md)以上の VCs を作成できます。

 

 





