---
title: 802.11 WLAN アダプターの取り外し
description: 802.11 WLAN アダプターの取り外し
ms.assetid: 2181d284-7987-48db-b7a4-d1296d8313ed
keywords:
- WDK 802.11 の WLAN のアダプターを削除します。
- WLAN アダプター、WDK を削除します。
- WLAN のアダプターを削除します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8838add8a48c46bc90c1e724ecbd7863e508993
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379304"
---
# <a name="80211-wlan-adapter-removal"></a>802.11 WLAN アダプターの取り外し




 

ワイヤレス LAN (WLAN) アダプターが削除または無効になっている、オペレーティング システムの呼び出し[ *Dot11ExtIhvDeinitAdapter* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)アダプターの削除の IHV 拡張機能の DLL に通知します。 オペレーティング システムも呼び出して、 *Dot11ExtIhvDeinitAdapter* IHV 拡張機能の DLL によって管理されるオペレーティング システムは、DLL をアンロードする前にすべてのアダプターの関数。

ときに[ *Dot11ExtIhvDeinitAdapter* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)が呼び出されると、IHV 拡張機能の DLL は次のガイドラインを従う必要があります。

-   IHV 拡張機能の DLL には、WLAN アダプターに割り当てられたリソースを解放する必要があります。 呼び出しを通じて具体的には、すべてのメモリが割り当てられている[ **Dot11ExtAllocateBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_allocate_buffer)呼び出しを通じて解放する必要があります[ **Dot11ExtFreeBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_free_buffer).

-   ハンドルは、使用、オペレーティング システムによって、WLAN を参照するアダプターが無効になってとき[ *Dot11ExtIhvDeinitAdapter* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)が呼び出されます。 オペレーティング システムでは、そのハンドルを渡しますを介して IHV 拡張 DLL を*hDot11SvcHandle*パラメーターと[ *Dot11ExtIhvInitAdapter* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_init_adapter)が呼び出されます。

    呼び出し内で、 *Dot11ExtIhvDeinitAdapter*関数呼び出しから返された後、DLL する必要がありますいない値を使用して、ハンドル、IHV 拡張関数を呼び出すことを宣言する場合、 *hDot11SvcHandle*パラメーターなど[ **Dot11ExtSendPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_send_packet)します。

-   IHV 拡張機能の DLL を呼び出すことによって開始された保留中の関連付け前操作がある場合、 [ *Dot11ExtIhvPerformPreAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate) IHV ハンドラー関数では、オペレーティング システムにおいて、操作を呼び出して取り消し対象として、 [ *Dot11ExtIhvDeinitAdapter* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)関数。 呼び出し内で、DLL は内部的には、関連付け前の操作を取り消す必要がありますを呼び出してはならない[ **Dot11ExtPreAssociateCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_pre_associate_completion)関連付け前に操作を完了します。

    前の関連付け操作の詳細については、次を参照してください。[関連付け前操作](pre-association-operations.md)します。

-   IHV 拡張機能の DLL を呼び出すことによって開始された保留中の後の関連付け操作がある場合、 [ *Dot11ExtIhvPerformPostAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate) IHV ハンドラー関数をオペレーティング システムを取り消します。呼び出して、操作、 [ *Dot11ExtIhvStopPostAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_stop_post_associate)関数を呼び出す前に[ *Dot11ExtIhvDeinitAdapter* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter).

    詳細については、後の関連付け操作は、次を参照してください。[後関連付け操作](post-association-operations.md)します。

-   オペレーティング システムの呼び出し、 [ *Dot11ExtIhvDeinitAdapter* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter) IHV 拡張機能の DLL によって管理されるオペレーティング システムは、DLL をアンロードする前にすべてのアダプターの関数。 このような状況でオペレーティング システムの呼び出し、 [ *Dot11ExtIhvDeinitService* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_deinit_service) IHV ハンドラー関数を呼び出すことによって、最後の WLAN のアダプターが停止した後に*Dot11ExtIhvDeinitAdapter*します。

    この操作の詳細については、次を参照してください。 [DLL 停止操作](dll-stop-operations.md)します。

 

 





