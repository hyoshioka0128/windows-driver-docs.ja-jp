---
title: 登録して、アドレス ファミリを開く
description: 登録して、アドレス ファミリを開く
ms.assetid: 2249adf9-2876-4442-be94-1a966d3f1c88
keywords:
- アドレス ファミリの WDK ネットワーク
- AFs WDK ネットワーク
- アドレス ファミリを登録します。
- アドレス ファミリを開く
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07a20ebfb56bf93b080030a160c825baedfa86de
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560751"
---
# <a name="registering-and-opening-an-address-family"></a>登録して、アドレス ファミリを開く





コール マネージャーは、各 NIC の接続指向のクライアントに呼び出し manager サービスを提供するアドレス ファミリを登録する必要があります。 同様に、MCM、ドライバーは、管理している NIC のアドレス ファミリを登録する必要があります。

アドレス ファミリを登録することにより、コール マネージャーまたは MCM ドライバーは、アダプターにバインドされたすべての接続指向のクライアントに、コール マネージャーのまたは MCM ドライバーのサービスを提供する NDIS とします。

接続指向のクライアントが、コール マネージャーまたは MCM ドライバーによってアドバタイズされたサービスを使用する場合は、コール マネージャーや MCM ドライバーのアドレス ファミリを開くことできます。

### <a name="registering-an-address-family-from-a-call-manager"></a>コール マネージャーから、アドレス ファミリを登録します。

後にその[ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)関数バインドで基になるミニポート ドライバー [ **NdisOpenAdapterEx**](https://msdn.microsoft.com/library/windows/hardware/ff563715)、コール マネージャー呼び出し[ **NdisCmRegisterAddressFamilyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff561685)バインディングのアドレス ファミリを登録する (次の図を参照してください)。

![登録して、コール マネージャーを開くと、アドレス ファミリを示す図](images/cm-01.png)

呼び出し**NdisCmRegisterAddressFamilyEx**コール マネージャーの特定のシグナル通知サービスをアドバタイズします。 コール マネージャーは、アドレスを登録する必要がありますファミリするごとにその*ProtocolBindAdapterEx*関数し、呼びますし、使用して、NIC に正常にバインド[ **NdisOpenAdapterEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563715).

コール マネージャーは、バインドされているすべてのミニポート ドライバーは、複数のアドレス ファミリをサポートできます。 コール マネージャーでは、バインドされている NIC が 1 つでも 1 つ以上のアドレス ファミリをサポートできます。 コール マネージャーは、バインディングでは、各アドレス ファミリ用の同じエントリ ポイントを登録する必要があります。 1 つだけのコール マネージャーは、任意の特定のミニポート ドライバーにバインドされているクライアントに対して特定の種類のアドレス ファミリをサポートできます。 コール マネージャーのエントリ ポイントを登録の詳細については、次を参照してください。[いる CoNDIS 登録](condis-registration.md)します。

### <a name="registering-an-address-family-from-an-mcm-driver"></a>アドレス ファミリ、MCM ドライバーからの登録

MCM にドライバーを呼び出す**NdisMCmRegisterAddressFamilyEx**からその[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389) でそのミニポートドライバーのエントリポイントを登録すた後関数[**NdisMRegisterMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/ff563654)します。 Regsitering エントリに関する詳細については、「、[いる CoNDIS 登録](condis-registration.md)します。 MCM にドライバーを呼び出す[ **NdisMCmRegisterAddressFamilyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563554)接続指向のクライアントにそのサービスを提供する 1 回 (次の図を参照してください)。

![登録して、mcm のドライバーを開くと、アドレス ファミリを示す図](images/fig1-01.png)

接続指向のシグナリング サポートのオンボードになっている NIC のミニポート ドライバーとして登録できます自体、MCM ドライバー場合でも、コール マネージャーが使用可能な可能性があります。 これにより、このような MCM ドライバーには、その NIC にコール マネージャーとしてコール マネージャーが横取りされ

### <a name="opening-an-address-family"></a>アドレス ファミリを開く

呼び出しをコール マネージャーのまたは MCM ドライバーの**Ndis (M) CmRegisterAddressFamily** NDIS を呼び出すと、 [ **ProtocolCoAfRegisterNotify** ](https://msdn.microsoft.com/library/windows/hardware/ff570251)の各関数(前の 2 つの図に示すように)、バインドの接続指向クライアント。

*ProtocolCoAfRegisterNotify*クライアントがこの特定の CM または MCM のドライバーのサービスを使用できるかどうかを判断するアドレス ファミリのデータを調査します。 かどうか、クライアントは、(M) CM が指定したアドレス ファミリのデータの変更を加えることは、コール マネージャーまたは MCM ドライバーの特定のシグナル通知プロトコルのサポートによって異なります。

クライアントは、提供された呼び出し管理サービスを検索する場合*ProtocolCoAfRegisterNotify* 、クライアントと呼び出しの AF あたりコンテキストの領域を割り当てます[ **NdisClOpenAddressFamilyEx**](https://msdn.microsoft.com/library/windows/hardware/ff561639). **NdisClOpenAddressFamilyEx** NDIS を使用して、クライアントの接続指向のエントリ ポイントは登録されません。 NDIS との接続指向のエントリ ポイントの登録の詳細については、次を参照してください。[いる CoNDIS 登録](condis-registration.md)します。

呼び出し**NdisClOpenAddressFamilyEx**と呼び出しを上司に NDIS または MCM ドライバーの[ **ProtocolCmOpenAf** ](https://msdn.microsoft.com/library/windows/hardware/ff570249) (前述のように既に 2 つの関数図の場合)。 *ProtocolCmOpenAf*によって、クライアントの有効なアドレス ファミリで渡される割り当てとアドレス ファミリのこのインスタンスを開いているクライアントに代わって操作を実行するために必要なリソースを初期化します。 *ProtocolCmOpenAf* NDIS 指定も格納*NdisAfHandle*コール マネージャーとオープン アドレス ファミリ用のクライアント間の関連付けを表します。

*ProtocolCmOpenAf*同期または非同期で完了できます。 非同期的に完了する、 *ProtocolCmOpenAf*コール マネージャーの関数を呼び出す[ **NdisCmOpenAddressFamilyComplete**](https://msdn.microsoft.com/library/windows/hardware/ff561682)、 *ProtocolCmOpenAf* MCM ドライバーの関数を呼び出す[ **NdisMCmOpenAddressFamilyComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563552)します。 呼び出し**Ndis (M) CmOpenAddressFamilyComplete** NDIS を呼び出すと、 *ProtocolOpenAfComplete*関数を呼び出した元クライアントの**NdisClOpenAddressFamilyEx**.

場合に、クライアントの呼び出し**NdisClOpenAddressFamilyEx** NDIS をクライアントに返しますが、成功すると、 *NdisAfHandle*コール マネージャーとオープン アドレス用のクライアント間の関連付けを表すファミリ。

クライアントが、受信呼び出しを受け入れる場合通常は[レジスタの 1 つまたは複数の SAPs](registering-a-sap.md)からその*ProtocolClOpenAfCompleteEx*関数を呼び出すことによって[ **NdisClRegisterSap**](https://msdn.microsoft.com/library/windows/hardware/ff561648)次の成功した呼び出し[ **NdisClOpenAddressFamilyEx**](https://msdn.microsoft.com/library/windows/hardware/ff561639)します。

発信呼び出しは、クライアントが、それが[1 つまたは複数の VCs を作成](creating-a-vc.md)でその*ProtocolClOpenAfCompleteEx* 1 つまたは複数で、発信通話を行うには、そのクライアントの要求に応じるために機能します。

 

 





