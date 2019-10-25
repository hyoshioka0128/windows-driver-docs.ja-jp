---
title: 802.11 WLAN アダプターのリセット
description: 802.11 WLAN アダプターのリセット
ms.assetid: 1f993977-b4a1-42ec-8de3-2f4855db93a7
keywords:
- アダプター WDK 802.11 WLAN、リセット
- WLAN アダプター WDK、リセット
- WLAN アダプターのリセット
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4fcb3aacf6b0745b256fc023f107815d0d4a592
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835399"
---
# <a name="80211-wlan-adapter-reset"></a>802.11 WLAN アダプターのリセット




 

オペレーティングシステムは、ワイヤレス LAN (WLAN) アダプタを初期化された状態に復元する必要が生じたときに、 [*Dot11ExtIhvAdapterReset*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_adapter_reset)を呼び出します。 オペレーティングシステムは、次のいずれかのイベントが発生するたびに、この関数を呼び出します。

-   WLAN アダプタが切断操作を実行します。 この操作の詳細については、「[切断操作](disconnection-operations.md)」を参照してください。

-   オペレーティングシステムによって、アダプターを管理するネイティブ802.11 ミニポートドライバーがリセットされます。これは、OID\_DOT11 の set 要求を介して[\_要求\_リセット](https://docs.microsoft.com/windows-hardware/drivers/network/oid-dot11-reset-request)します。

[*Dot11ExtIhvAdapterReset*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_adapter_reset)が呼び出された場合、IHV 拡張 DLL は次のガイドラインに従う必要があります。

-   IHV Extensions DLL は、 [*Dot11ExtIhvInitAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_adapter)関数が呼び出された後の状態と同じ状態に復元する必要があります。 DLL で WLAN アダプターに固有の設定が構成されている場合、これらの設定を*Dot11ExtIhvInitAdapter*が呼び出されたときと同じ状態に復元する必要があります。

-   [*Dot11ExtIhvPerformPreAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate) ihv ハンドラー関数の呼び出しによって開始された、保留中の関連付け前操作が IHV 拡張 dll に存在する場合、DLL は[**Dot11ExtPreAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_pre_associate_completion)を呼び出して操作を取り消す必要があります。 この場合、DLL は**Dot11ExtPreAssociateCompletion**の*DWWIN32ERROR*パラメーターを ERROR\_キャンセルに設定します。

    事前関連付け操作の詳細については、「[事前関連付け操作](pre-association-operations.md)」を参照してください。

-   DLL に、 [*Dot11ExtIhvPerformPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate) IHV ハンドラー関数の呼び出しによって開始された、保留中のポスト関連付け操作がある場合、Dll は[**Dot11ExtPostAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)を呼び出して操作を取り消す必要があります。 この場合、DLL は**Dot11ExtPostAssociateCompletion**の*DWWIN32ERROR*パラメーターを ERROR\_キャンセルに設定します。

    関連付け後の操作の詳細については、「[関連付け後の操作](post-association-operations.md)」を参照してください。

 

 





