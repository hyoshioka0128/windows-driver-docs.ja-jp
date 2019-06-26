---
title: MSI-X の事前登録
description: MSI-X の事前登録
ms.assetid: 93a09ebd-8a50-4c96-a926-54bb4686a618
keywords:
- MSI X の WDK ネットワーク、リソース要件をフィルター処理関数
- メッセージ シグナル割り込み WDK ネットワーク、リソース要件フィルター関数
- Msi WDK ネットワーク、リソース要件フィルター関数
- リソース要件関数 net WDK をフィルター処理します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f5451d7353d49b014868525c197ab30d623af71
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364051"
---
# <a name="msi-x-pre-registration"></a>MSI-X の事前登録





MSI X の変更の割り込みアフィニティをサポートするために、またはメッセージの割り込みのリソースを削除するには、ミニポート ドライバーは、リソース要件フィルター関数を確立する必要があります。 NDIS 呼び出される前にこの事前登録手順が発生した、 [ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数。

リソース要件フィルター関数を確立するために、ミニポート ドライバーを提供する必要があります、 [ *MiniportSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)関数。 ミニポート ドライバーを呼び出すと、 [ **NdisMRegisterMiniportDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)関数を[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチン、ドライバーエントリ ポイントを渡して*MiniportSetOptions*で、 [ **NDIS\_ミニポート\_ドライバー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_driver_characteristics)構造体。 NDIS 呼び出し、 *MiniportSetOptions*関数のコンテキストで**NdisMRegisterMiniportDriver**します。

*MiniportSetOptions*、ミニポート ドライバーの呼び出し、 [ **NdisSetOptionalHandlers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissetoptionalhandlers)関数を指定します、 [ **NDIS\_ミニポート\_PNP\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_pnp_characteristics)構造体。 この構造体のエントリ ポイントを定義する、 [ *MiniportAddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_add_device)、 [ *MiniportRemoveDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_remove_device)、 [ *MiniportStartDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_pnp_irp)、および[ *MiniportFilterResourceRequirements* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_pnp_irp)関数。

NDIS NDIS は、プラグ アンド プレイ (PnP) マネージャーから、デバイスの追加要求を受け取る、呼び出し、ミニポート ドライバーの*MiniportAddDevice*関数。 NDIS からに渡されるハンドル*MiniportAddDevice*で、 *MiniportAdapterHandle*パラメーターは、NDIS は後でに渡されるハンドル、 [ *MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数。

[ *MiniportAddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_add_device)、ドライバーの初期化、 [ **NDIS\_ミニポート\_追加\_デバイス\_登録\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_add_device_registration_attributes)構造体し、この構造体を渡す、 [ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)関数。 NDIS\_ミニポート\_追加\_デバイス\_登録\_属性の構造に含まれる、 **MiniportAddDeviceContext**ミニポートを識別するハンドルは、メンバーデバイスのドライバーに割り当てられたコンテキストの領域。 NDIS は後でこのコンテキストのハンドルを提供します、 [ *MiniportRemoveDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_remove_device)、 [ *MiniportFilterResourceRequirements*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_pnp_irp)、 [*MiniportStartDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_pnp_irp)、および[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数。 *MiniportInitializeEx*、コンテキスト ハンドルが渡された、 **MiniportAddDeviceContext**のメンバー、 [ **NDIS\_ミニポート\_INIT\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_init_parameters)構造体、 *MiniportInitParameters*パラメーターを指します。

NDIS 後[ *MiniportAddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_add_device)と*MiniportAddDevice*返します NDIS\_状態\_成功すると、NDIS 呼び出し、 *MiniportFilterResourceRequirements*関数を受信するたびに、 [ **IRP\_MN\_フィルター\_リソース\_要件** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements) I/O 要求パケット (IRP)。 *MiniportFilterResourceRequirements* MSI X メッセージごとに割り込みアフィニティを変更する、メッセージの割り込みのリソースを追加またはドライバーは行ベースでの割り込みを登録している場合は、メッセージの割り込みリソースを削除、 [*MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数。 割り込みアフィニティのポリシーを設定する方法についての詳細については、次を参照してください。 [MSI X リソース フィルター](msi-x-resource-filtering.md)します。

NDIS は、PnP マネージャーからデバイスの削除要求を受け取る、NDIS 呼び出し、ミニポート ドライバーの[ *MiniportRemoveDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_remove_device)関数。 *MiniportRemoveDevice*関数は、操作を取り消す必要がありますが、 [ *MiniportAddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_add_device)関数を実行します。

 

 





