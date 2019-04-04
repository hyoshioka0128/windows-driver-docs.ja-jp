---
title: 中間ドライバーの PnP や電源管理イベントの処理
description: 電源管理イベントおよび処理 PnP に中間のドライバーの初期化
ms.assetid: 7c9f10f1-1094-4b43-990b-fc3b3fee5ed1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a14f345f48748f8c61ca890eb7fd7f5aeab6246f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530132"
---
# <a name="initializing-intermediate-drivers-to-handle-pnp-and-power-management-events"></a>電源管理イベントおよび処理 PnP に中間のドライバーの初期化


プラグ アンド プレイ (PnP) および電源管理イベントを処理するには、NDIS 中間ドライバは、次の操作を行う必要があります。

-   NDIS が、中間のドライバーを呼び出すときに[ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)関数の場合、 *BindParameters*パラメーターが指す、 [ **NDIS\_PM\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)基になるミニポート アダプターの機能を含む構造体。 電源管理機能は、次のメンバーのいずれかで報告されます。

    -   **デバイス**

        このメンバーには、NDIS 内での電源管理機能が含まれていますの NDIS 6.0 および 6.1 の NDIS ドライバーを中間、\_PNP\_機能の構造体。 この構造体の詳細については、[OID\_PNP\_機能](https://msdn.microsoft.com/library/windows/hardware/ff569774)を参照してください。

        **注**の NDIS 6.20 が動作し、後で中間ドライバー、**デバイス**に設定されているメンバー **NULL** に電源管理機能が報告される**PowerManagementCapabilitiesEx**メンバー。



    -   **PowerManagementCapabilitiesEx**

        NDIS 6.20 が動作と中間ドライバーを後で、このメンバーには内での電源管理機能が含まれています、 [ **NDIS\_PM\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)構造体。

        **注**NDIS 6.0 の NDIS 6.1 中級レベルのドライバー、 **PowerManagementCapabilitiesEx**に設定されているメンバー **NULL** に電源管理機能が報告される**デバイス**メンバー。




**注**基になるミニポート アダプターが電源管理のイベントをサポートしていない場合、**デバイス**と**PowerManagementCapabilitiesEx** にメンバーが設定されます**NULL**します。




-   NDIS を呼び出すと[MiniportInitializeEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize) NDIS 中間ドライバーでサポートされている各仮想ミニポートのドライバーが呼び出すことによって、電源管理機能を報告[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)次のようにします。

    1.  いずれかで報告される電源管理機能、NDIS 中間ドライバのバージョンに応じて、**デバイス**(NDIS 6.0 および 6.1 の NDIS 中間ドライバ) のメンバーまたは**PowerManagementCapabilitiesEx** (NDIS 6.20 が動作を後で中間ドライバー) のメンバー [ **NDIS\_ミニポート\_アダプター\_全般\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)します。 どちらの場合、**デバイス**または**PowerManagementCapabilitiesEx**のメンバー、 [ **NDIS\_バインド\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff564832)構造体は、 **NULL**、中間のドライバーは、次を実行する必要があります。

        -   元の値を保存、 **MinMagicPacketWakeUp**、 **MinPatternWakeUp**、および**MinLinkChangeWakeUp**のメンバー、 **デバイス**(NDIS 6.0 および 6.1 の NDIS) または**PowerManagementCapabilitiesEx**(NDIS 6.20 およびそれ以降) のメンバー。

        -   電源管理機能を無効に設定して、 **MinMagicPacketWakeUp**、 **MinPatternWakeUp**、および**MinLinkChangeWakeUp**メンバー **NdisDeviceStateUnspecified**します。

        -   変更後のアドレスを渡す[ **NDIS\_ミニポート\_アダプター\_全般\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)として構造体、 *MiniportAttributes*への呼び出しでパラメーター [ **NdisMSetMiniportAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff563672)します。

    2.  中間のドライバーは、NDIS を設定する必要があります\_ミニポート\_属性\_いいえ\_HALT\_ON\_で SUSPEND フラグ、 **AttributeFlags**のメンバー、[ **NDIS\_ミニポート\_アダプター\_登録\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565934)構造体。 ドライバーとしてこの構造体のアドレスを渡す必要があります、 *MiniportAttributes*への呼び出しでパラメーター [ **NdisMSetMiniportAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff563672)します。

    NDIS 中間ドライバの初期化要件の詳細については、[初期化仮想ミニポート](initializing-virtual-miniports.md)を参照してください。









