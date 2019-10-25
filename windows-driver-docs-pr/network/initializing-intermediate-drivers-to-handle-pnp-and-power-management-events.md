---
title: 中間ドライバーでの PnP および電源管理イベントの処理
description: PnP および電源管理イベントを処理するための中間ドライバーの初期化
ms.assetid: 7c9f10f1-1094-4b43-990b-fc3b3fee5ed1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d60ef6b907985ddd73028cebd26973e33b51bb7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824444"
---
# <a name="initializing-intermediate-drivers-to-handle-pnp-and-power-management-events"></a>PnP および電源管理イベントを処理するための中間ドライバーの初期化


プラグアンドプレイ (PnP) と電源管理イベントを処理するために、NDIS 中間ドライバーは次の操作を行う必要があります。

-   NDIS が中間ドライバーの[*Protocolbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)関数を呼び出すと、 *bindparameters*パラメーターは、基になるミニポートの機能を含む[**ndis\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)構造を指します。アダプター. 電源管理機能は、次のいずれかのメンバーで報告されます。

    -   **PowerManagementCapabilities**

        NDIS 6.0 および NDIS 6.1 中間ドライバーの場合、このメンバーには、NDIS\_PNP\_機能の構造内の電源管理機能が含まれます。 この構造の詳細については、「 [OID\_PNP\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-capabilities)」を参照してください。

        **メモ** NDIS 6.20 以降の中間ドライバーでは、 **PowerManagementCapabilities**メンバーが**NULL**に設定され、電源管理機能が**PowerManagementCapabilitiesEx**メンバーに報告されます。



    -   **PowerManagementCapabilitiesEx**

        NDIS 6.20 以降の中間ドライバーの場合、このメンバーには、 [**ndis\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)の構造内の電源管理機能が含まれます。

        **メモ** NDIS 6.0 および NDIS 6.1 中間ドライバーの場合、 **PowerManagementCapabilitiesEx**メンバーは**NULL**に設定され、電源管理機能は**PowerManagementCapabilities**メンバーに報告されます。




**メモ** 基になるミニポートアダプターで電源管理イベントがサポートされていない場合、 **PowerManagementCapabilities**メンバーと**PowerManagementCapabilitiesEx**メンバーは**NULL**に設定されます。




-   Ndis が NDIS 中間ドライバーでサポートされている各仮想ミニポートに対して[MiniportInitializeEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)を呼び出すと、ドライバーは次の方法で[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)を呼び出して電源管理機能を報告します。

    1.  NDIS 中間ドライバーのバージョンに応じて、電源管理機能は**PowerManagementCapabilities**メンバー (ndis 6.0 および ndis 6.1 中間ドライバーの場合) または**PowerManagementCapabilitiesEx**で報告されます。[**ndis\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)のメンバー (ndis 6.20 以降の中間ドライバー用)。 [**NDIS\_BIND\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)構造体の**いずれかの**メンバーが**NULL**でない場合、中間**ドライバーは次**の操作を行う必要があります。

        -   **PowerManagementCapabilities**の**MinMagicPacketWakeUp**、 **Minpattern ウェイクアップ**、および**minlinkchangeウェイクアップ**のメンバーの元の値を保存します (Ndis 6.0 と ndis 6.1) または**PowerManagementCapabilitiesEx**(ndis)6.20 以降) のメンバー。

        -   **MinMagicPacketWakeUp**、 **minpattern ウェイクアップ**、および**Minlinkchangeウェイクアップ**メンバーを**NdisDeviceStateUnspecified**に設定して、電源管理機能を無効にします。

        -   [**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)への呼び出しで、変更した[**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)の構造体のアドレスを*miniportattributes*パラメーターとして渡します。

    2.  中間ドライバーでは、ndis\_ミニポート\_アダプターの**Attributeflags**メンバーの\_SUSPEND フラグに\_停止\_\_、NDIS\_ミニポート\_属性を設定する必要があり[ **\_登録\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)構造体。 ドライバーは、この構造体のアドレスを[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)への呼び出しの*miniportattributes*パラメーターとして渡す必要があります。

    NDIS 中間ドライバーの初期化要件の詳細については、「[仮想ミニポートの初期化](initializing-virtual-miniports.md)」を参照してください。









