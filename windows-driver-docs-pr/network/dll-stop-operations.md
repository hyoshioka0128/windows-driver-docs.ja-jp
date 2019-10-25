---
title: DLL 停止操作
description: DLL 停止操作
ms.assetid: b49e9215-3781-4e19-8287-f484553ccb2e
keywords:
- IHV 拡張機能 DLL WDK ネイティブ802.11、停止操作
- IHV 拡張 DLL をアンロードしています
- IHV 拡張 DLL を停止しています
- ネイティブ 802.11 IHV 拡張 DLL WDK、停止操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16f4a7cfe8eac2677b1f8573203047c38a2b0670
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838130"
---
# <a name="dll-stop-operations"></a>DLL 停止操作




 

オペレーティングシステムは、常に IHV 拡張 DLL を停止し、アンロードします。

-   DLL によって管理されている最後のワイヤレス LAN (WLAN) アダプタは、削除されるか無効になります。

-   ホストコンピューターはリセットまたはシャットダウンされます。

IHV 拡張 DLL を停止およびアンロードする場合、オペレーティングシステムはこのシーケンスに従います。

1.  オペレーティングシステムは、まず、IHV 拡張 DLL によって管理されるすべての WLAN アダプターに対して[*Dot11ExtIhvDeinitAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter) IHV ハンドラー関数を呼び出します。 この操作の詳細については、「 [802.11 WLAN アダプターの削除](802-11-wlan-adapter-removal.md)」を参照してください。

    *Dot11ExtIhvDeinitAdapter*の呼び出しの後、IHV 拡張 DLL は、 [**Dot11ExtNicSpecificExtension**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_nic_specific_extension)などのアダプター固有の操作に関連する ihv 拡張機能を呼び出すことはできません。

2.  次に、オペレーティングシステムは[*Dot11ExtIhvDeinitService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_service) IHV ハンドラー関数を呼び出します。 この関数が呼び出されると、IHV 拡張 DLL は、割り当てられたすべてのリソースを解放し、アンロード用に準備する必要があります。

    *Dot11ExtIhvDeinitService*の呼び出しの後、IHV 拡張 DLL は、任意の ihv 拡張機能を呼び出すことはできません。

3.  最後に、オペレーティングシステムは、 *Fdwreason*パラメーターを dll に設定して、IHV 拡張 DLL の*DllMain*関数を呼び出し\_プロセス\_デタッチします。 *DllMain*と dll の詳細については、Microsoft Windows SDK のドキュメント内の「ダイナミックリンクライブラリについて」を参照してください。

IHV 拡張機能の詳細については、「[ネイティブ 802.11 Ihv 拡張関数](https://docs.microsoft.com/windows-hardware/drivers/network/native-802-11-ihv-extensibility-functions)」を参照してください。

 

 





