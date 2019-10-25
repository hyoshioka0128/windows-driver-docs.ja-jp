---
title: MSI-X の事前登録
description: MSI-X の事前登録
ms.assetid: 93a09ebd-8a50-4c96-a926-54bb4686a618
keywords:
- MSI-X WDK ネットワーク, リソース要件フィルター関数
- メッセージシグナル割り込み、WDK ネットワーク、リソース要件フィルター関数
- Msi WDK ネットワーク、リソース要件フィルター関数
- リソース要件フィルター関数 WDK net
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6af56278c3d771d822db1e9f61cb3f23f77f684
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844213"
---
# <a name="msi-x-pre-registration"></a>MSI-X の事前登録





MSI-X の割り込みのアフィニティの変更やメッセージの割り込みリソースの削除をサポートするには、ミニポートドライバーがリソース要件のフィルター機能を確立する必要があります。 この事前登録手順は、NDIS が[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出す前に発生します。

リソース要件フィルター関数を確立するには、ミニポートドライバーで[*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)関数を提供する必要があります。 ミニポートドライバーが[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンから[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)関数を呼び出すと、ドライバーは*MiniportSetOptions*のエントリポイントを[**NDIS\_ミニポート\_ドライバーに渡し\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)の構造。 NDIS は、 **NdisMRegisterMiniportDriver**のコンテキストで*MiniportSetOptions*関数を呼び出します。

*MiniportSetOptions*から、ミニポートドライバーは[**NdisSetOptionalHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)関数を呼び出し、 [**NDIS\_ミニポート\_PNP\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_pnp_characteristics)の構造を指定します。 この構造体は、 [*MiniportAddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_add_device)、 [*miniportremovedevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_remove_device)、 [*miniportremovedevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pnp_irp)、および[*MiniportFilterResourceRequirements*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pnp_irp)関数のエントリポイントを定義します。

NDIS がプラグアンドプレイ (PnP) マネージャーからデバイスの追加要求を受信すると、NDIS はミニポートドライバーの*MiniportAddDevice*関数を呼び出します。 *Miniportadapterhandle*パラメーターで Ndis が*MiniportAddDevice*に渡すハンドルは、後で[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数に渡されるハンドルです。

[*MiniportAddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_add_device)では、ドライバーは[**NDIS\_ミニポート\_初期化し、\_デバイス\_登録\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_add_device_registration_attributes)構造を追加して、この構造体を[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)に渡します。プロシージャ. NDIS\_ミニポート\_追加\_デバイス\_登録\_属性構造には、デバイスのミニポートドライバーで割り当てられたコンテキスト領域へのハンドルである**Miniportadddevicecontext**メンバーが含まれています。 このコンテキストハンドルは、後で[*Miniportremovedevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_remove_device)、 [*MiniportFilterResourceRequirements*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pnp_irp)、 [*miniportremovedevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pnp_irp)、および[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数に提供されます。 *MiniportInitializeEx*の場合、コンテキストハンドルは、 *Miniportinitparameters*パラメーターを指定した[**NDIS\_ミニポート\_INIT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_init_parameters)構造体の**miniportadddevicecontext**メンバーに渡されます。はを指します。

Ndis 呼び出し[*MiniportAddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_add_device)と*MiniportAddDevice*は、NDIS\_STATUS\_SUCCESS を返すと、IRP\_完了するたびに*MiniportFilterResourceRequirements*関数を呼び出し[ **@no__t\_リソース\_要件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements)i/o 要求パケット (IRP) をフィルター処理します (_s)。 *MiniportFilterResourceRequirements*は、各 MSI-X メッセージの割り込み関係を変更したり、メッセージ割り込みリソースを追加したり、メッセージ割り込みリソースを削除し[*たりできます。MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数。 割り込みアフィニティポリシーを確立する方法の詳細については、「 [MSI-X リソースフィルター](msi-x-resource-filtering.md)」を参照してください。

NDIS が PnP マネージャーからデバイスの削除要求を受信すると、NDIS はミニポートドライバーの[*Miniportremovedevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_remove_device)関数を呼び出します。 *Miniportremovedevice*関数は、 [*MiniportAddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_add_device)関数によって実行された操作を元に戻す必要があります。

 

 





