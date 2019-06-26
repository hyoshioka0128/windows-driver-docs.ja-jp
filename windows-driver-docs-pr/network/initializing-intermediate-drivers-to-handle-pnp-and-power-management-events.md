---
title: 中間ドライバーの PnP や電源管理イベントの処理
description: PnP および電源管理イベントを処理するための中間ドライバーの初期化
ms.assetid: 7c9f10f1-1094-4b43-990b-fc3b3fee5ed1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 688ca0538582b0acaf1a413850d02d90bf021010
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381271"
---
# <a name="initializing-intermediate-drivers-to-handle-pnp-and-power-management-events"></a>PnP および電源管理イベントを処理するための中間ドライバーの初期化


プラグ アンド プレイ (PnP) および電源管理イベントを処理するには、NDIS 中間ドライバは、次の操作を行う必要があります。

-   NDIS が、中間のドライバーを呼び出すときに[ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)関数の場合、 *BindParameters*パラメーターが指す、 [ **NDIS\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_capabilities)基になるミニポート アダプターの機能を含む構造体。 電源管理機能は、次のメンバーのいずれかで報告されます。

    -   **デバイス**

        このメンバーには、NDIS 内での電源管理機能が含まれていますの NDIS 6.0 および 6.1 の NDIS ドライバーを中間、\_PNP\_機能の構造体。 この構造体の詳細については、次を参照してください。 [OID\_PNP\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-capabilities)します。

        **注**の NDIS 6.20 が動作し、後で中間ドライバー、**デバイス**に設定されているメンバー **NULL** に電源管理機能が報告される**PowerManagementCapabilitiesEx**メンバー。



    -   **PowerManagementCapabilitiesEx**

        NDIS 6.20 が動作と中間ドライバーを後で、このメンバーには内での電源管理機能が含まれています、 [ **NDIS\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_capabilities)構造体。

        **注**NDIS 6.0 の NDIS 6.1 中級レベルのドライバー、 **PowerManagementCapabilitiesEx**に設定されているメンバー **NULL** に電源管理機能が報告される**デバイス**メンバー。




**注**基になるミニポート アダプターが電源管理のイベントをサポートしていない場合、**デバイス**と**PowerManagementCapabilitiesEx** にメンバーが設定されます**NULL**します。




-   NDIS を呼び出すと[MiniportInitializeEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize) NDIS 中間ドライバーでサポートされている各仮想ミニポートのドライバーが呼び出すことによって、電源管理機能を報告[ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)次のようにします。

    1.  いずれかで報告される電源管理機能、NDIS 中間ドライバのバージョンに応じて、**デバイス**(NDIS 6.0 および 6.1 の NDIS 中間ドライバ) のメンバーまたは**PowerManagementCapabilitiesEx** (NDIS 6.20 が動作を後で中間ドライバー) のメンバー [ **NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)します。 どちらの場合、**デバイス**または**PowerManagementCapabilitiesEx**のメンバー、 [ **NDIS\_バインド\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)構造体は、 **NULL**、中間のドライバーは、次を実行する必要があります。

        -   元の値を保存、 **MinMagicPacketWakeUp**、 **MinPatternWakeUp**、および**MinLinkChangeWakeUp**のメンバー、 **デバイス**(NDIS 6.0 および 6.1 の NDIS) または**PowerManagementCapabilitiesEx**(NDIS 6.20 およびそれ以降) のメンバー。

        -   電源管理機能を無効に設定して、 **MinMagicPacketWakeUp**、 **MinPatternWakeUp**、および**MinLinkChangeWakeUp**メンバー **NdisDeviceStateUnspecified**します。

        -   変更後のアドレスを渡す[ **NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)として構造体、 *MiniportAttributes*への呼び出しでパラメーター [ **NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)します。

    2.  中間のドライバーは、NDIS を設定する必要があります\_ミニポート\_属性\_いいえ\_HALT\_ON\_で SUSPEND フラグ、 **AttributeFlags**のメンバー、[ **NDIS\_ミニポート\_アダプター\_登録\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)構造体。 ドライバーとしてこの構造体のアドレスを渡す必要があります、 *MiniportAttributes*への呼び出しでパラメーター [ **NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)します。

    NDIS 中間ドライバの初期化要件の詳細については、次を参照してください。[初期化仮想ミニポート](initializing-virtual-miniports.md)します。









