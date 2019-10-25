---
title: 中間ドライバーの初期化
description: 中間ドライバーの初期化
ms.assetid: cd4903f8-f522-403a-bec4-03ee7e82dcac
keywords:
- NDIS 中間ドライバー WDK、初期化中
- 中間ドライバー WDK ネットワーク、初期化
- 中間ドライバーの初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c4afb002444841f74bc43eac8ca1600df100ce6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824489"
---
# <a name="initializing-an-intermediate-driver"></a>中間ドライバーの初期化



NDIS 中間ドライバーは、その*Miniportxxx*関数とその*Protocolxxx*関数を[driverentry](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンのコンテキストで登録します。 *Miniportxxx*関数を登録するには、中間ドライバーで[NdisMRegisterMiniportDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)関数を呼び出す必要があります。このとき、NDIS\_中間\_ドライバーフラグを設定します。 このフラグは、ドライバーが*Miniportdrivercharacteristics*に渡す、 [**NDIS\_ミニポート\_ドライバー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)の構造にあります。 *Protocolxxx*関数を登録するには、中間ドライバーで[NdisRegisterProtocolDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterprotocoldriver)関数を呼び出す必要があります。

ドライバーが NDIS 中間ドライバーとして正常に登録されている場合、 [Driverentry](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)は STATUS_SUCCESS、またはそれと同等の NDIS_STATUS_SUCCESS を返します。 **NdisXxx**関数またはカーネルモードのサポートルーチンによって返されたエラー状態を伝達することによって、driverentry が初期化に失敗した場合、ドライバーは読み込まれたままになりません。 **Driverentry**は同期的に実行する必要があります。つまり、ありますまたはそれに相当する NDIS_STATUS_PENDING を返すことはできません。

中間ドライバーを NDIS に登録するには、 [Driverentry](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンが少なくとも次の条件を備えている必要があります。

- NDIS_INTERMEDIATE_DRIVER フラグを設定して[NdisMRegisterMiniportDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)関数を呼び出し、ドライバーの*miniportxxx*関数を登録します。
- ドライバーが後で基になる NDIS ドライバーにバインドする場合は、 [NdisRegisterProtocolDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterprotocoldriver)関数を呼び出してドライバーの*protocolxxx*関数を登録します。
- [NdisIMAssociateMiniport](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisimassociateminiport)関数を呼び出して、ドライバーのミニポートの上端とプロトコルの下端との関連付けについて NDIS に通知します。

**NdisMRegisterMiniportDriver**が正常に返された後に**driverentry**でエラーが発生した場合、ドライバーは**Driverentry**を返す前に[NdisMDeregisterMiniportDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterminiportdriver)関数を呼び出す必要があります。 **Driverentry**が成功した場合、ドライバーは[Miniportdriverunload](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_unload)関数から**NdisMDeregisterMiniportDriver**を呼び出す必要があります。

中間ドライバーは、プロトコルドライバーとミニポートドライバーのほとんどの**Driverentry**要件を共有します。

ドライバーが[Protocolbindadapterex](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)関数から[NdisIMInitializeDeviceInstanceEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisiminitializedeviceinstanceex)関数を呼び出すと、中間ドライバーの仮想ミニポートの初期化が発生します。

すべての基になるミニポートドライバーが初期化された後、NDIS は*Protocolbindadapterex*関数を呼び出します。

実際には、NDIS 中間ドライバーの**Driverentry**関数は、 **NdisMRegisterMiniportDriver**に渡すと*RegistryPath*ポインターを無視できます。 このようなドライバーは、 **NdisMRegisterMiniportDriver**に渡すと、 *driverobject*ポインターを無視することもできます。 ただし、ドライバーは、 *NdisMiniportDriverHandle*で**NdisMRegisterMiniportDriver**によって返されるミニポートドライバーハンドルの値と、 **NdisRegisterProtocolDriver** at*によって返されるプロトコルハンドルの値を保存する必要があります。NdisProtocolHandle*は、 **NdisXxx**関数の後続の呼び出しに対して使用します。 中間ドライバーの*Protocolbindadapterex*関数は、 *MiniportInitializeEx*関数を呼び出して中間ドライバーの仮想ミニポートを初期化する前に、基になる各ミニポートドライバーにドライバーをバインドします。 それでも上位レベルのプロトコルドライバーは、それを作成する仮想ミニポートにバインドします。 この方法では、NDIS 中間ドライバーが、仮想ミニポートの作成時に、バインド先の基になるミニポートドライバーの機能に従ってリソースを割り当てることができます。
