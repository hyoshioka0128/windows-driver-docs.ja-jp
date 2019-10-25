---
title: 802.11 WLAN アダプターの取り外し
description: 802.11 WLAN アダプターの取り外し
ms.assetid: 2181d284-7987-48db-b7a4-d1296d8313ed
keywords:
- アダプタ WDK 802.11 WLAN、削除
- WLAN アダプター WDK、削除
- WLAN アダプターの削除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78c86c10a279c3bb662359ee5fec7823d23edebe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838259"
---
# <a name="80211-wlan-adapter-removal"></a>802.11 WLAN アダプターの取り外し




 

ワイヤレス LAN (WLAN) アダプターを削除または無効にすると、オペレーティングシステムは[*Dot11ExtIhvDeinitAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)を呼び出して、アダプターの削除を IHV 拡張 DLL に通知します。 また、オペレーティングシステムは、オペレーティングシステムが DLL をアンロードする前に、IHV 拡張 DLL によって管理されるすべてのアダプターに対して*Dot11ExtIhvDeinitAdapter*関数を呼び出します。

[*Dot11ExtIhvDeinitAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)が呼び出された場合、IHV 拡張 DLL は次のガイドラインに従う必要があります。

-   IHV 拡張 DLL は、WLAN アダプターに割り当てられているリソースを解放する必要があります。 特に、 [**Dot11ExtAllocateBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_allocate_buffer)の呼び出しによって割り当てられたすべてのメモリは、 [**Dot11ExtFreeBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_free_buffer)を呼び出すことによって解放する必要があります。

-   [*Dot11ExtIhvDeinitAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)が呼び出されると、オペレーティングシステムが WLAN アダプターを参照するために使用するハンドルは無効になります。 [*Dot11ExtIhvInitAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_adapter)が呼び出されると、オペレーティングシステムは、 *hDot11SvcHandle*パラメーターを使用して、そのハンドルを IHV 拡張 DLL に渡します。

    *Dot11ExtIhvDeinitAdapter*関数の呼び出し内で、呼び出しから制御が戻った後、 *hDot11SvcHandle*パラメーターを宣言する IHV 拡張関数を呼び出すときに、DLL は handle 値を使用しないようにする必要があります。たとえば[ **、Dot11ExtSendPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_packet)。

-   [*Dot11ExtIhvPerformPreAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate) ihv ハンドラー関数の呼び出しによって開始された、保留中の関連付け前の操作が IHV 拡張 DLL にある場合、オペレーティングシステムは、の[*呼び出しによって操作を取り消したと見なします。Dot11ExtIhvDeinitAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)関数。 この呼び出しでは、DLL は内部的に関連付けの操作をキャンセルする必要がありますが、 [**Dot11ExtPreAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_pre_associate_completion)を呼び出して、事前関連付け操作を完了することはできません。

    事前関連付け操作の詳細については、「[事前関連付け操作](pre-association-operations.md)」を参照してください。

-   [*Dot11ExtIhvPerformPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate) ihv ハンドラー関数の呼び出しによって開始された、保留中の関連付け後の操作が IHV 拡張 DLL に存在する場合、オペレーティングシステムは、を[*呼び出して操作を取り消します。Dot11ExtIhvStopPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_stop_post_associate)関数は、 [*Dot11ExtIhvDeinitAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)を呼び出す前に関数を呼び出します。

    関連付け後の操作の詳細については、「[関連付け後の操作](post-association-operations.md)」を参照してください。

-   オペレーティングシステムは、オペレーティングシステムが DLL をアンロードする前に、IHV 拡張 DLL によって管理されるすべてのアダプターに対して[*Dot11ExtIhvDeinitAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)関数を呼び出します。 この場合、オペレーティングシステムは、 *Dot11ExtIhvDeinitAdapter*への呼び出しによって最後の WLAN アダプターが停止した後、 [*Dot11ExtIhvDeinitService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_service) IHV ハンドラー関数を呼び出します。

    この操作の詳細については、「 [DLL の停止操作](dll-stop-operations.md)」を参照してください。

 

 





