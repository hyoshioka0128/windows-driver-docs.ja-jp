---
title: 関連付け前の操作ガイドライン
description: 関連付け前の操作ガイドライン
ms.assetid: 35e9b701-6d5d-4c76-80fc-bb146be1ddb1
keywords:
- 事前関連付け操作 WDK ネイティブ 802.11 IHV 拡張 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69d8baae687c95c0d24abecae29feaf51ca8f1d0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843497"
---
# <a name="pre-association-operation-guidelines"></a>関連付け前の操作ガイドライン




 

IHV 拡張 DLL は、関連付け前の操作を実行するときに、次のガイドラインに従う必要があります。

-   [*Dot11ExtIhvPerformPreAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate)関数が呼び出されると、IHV 拡張 DLL は次の操作を行う必要があります。
    -   接続とセキュリティプロファイルの IHV 拡張機能を確認します。 プロファイルパラメーターが無効な場合、 *Dot11ExtIhvPerformPreAssociate*関数は winerror.h で定義されている適切なエラーコードを返します。
    -   関連付け前の操作が完了するまで、新しいスレッドを作成して開始します。 事前関連付け操作は[*Dot11ExtIhvPerformPreAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate)の呼び出しから非同期に完了する必要があるため、IHV 拡張 DLL は、操作の完了後にこのスレッドから[**Dot11ExtPreAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_pre_associate_completion)を呼び出す必要があります。
    -   関数呼び出しからエラーを\_返します。 この時点で、ネットワークプロファイルが有効であり、関連付け前の操作が進行中であることがオペレーティングシステムに通知されます。
-   IHV 拡張 DLL は、 [**Dot11ExtNicSpecificExtension**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_nic_specific_extension)関数を呼び出して、ワイヤレス LAN (WLAN) アダプターを構成できます。 この関数は、 [*Dot11ExtIhvPerformPreAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate)の呼び出し内から、または*Dot11ExtIhvPerformPreAssociate*が返された後に、事前関連付け操作を処理するスレッドから呼び出すことができます。

-   [**Dot11ExtSetProfileCustomUserData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_profile_custom_user_data)、 [**Dot11ExtGetProfileCustomUserData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_get_profile_custom_user_data)、および[**Dot11ExtSetCurrentProfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_current_profile)への呼び出しは、 [*Dot11ExtIhvPerformPreAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate)の呼び出し内から行うことはできません。 これらの関数は、 *Dot11ExtIhvPerformPreAssociate*によってエラー\_返された後にのみ呼び出すことができます。

-   IHV 拡張 DLL が[**Dot11ExtPreAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_pre_associate_completion)を呼び出して、関連付け前の操作を完了すると、接続セッションのハンドルは無効になります。 オペレーティングシステムは、 [*Dot11ExtIhvPerformPreAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate)の*hconnectsession*パラメーターを使用してこのハンドルを渡します。 *Hconnectsession*パラメーターを宣言する IHV 拡張関数を呼び出す場合、DLL はこのハンドル値を使用しないようにする必要があります。

    IHV 拡張機能の詳細については、「[ネイティブ 802.11 Ihv 拡張関数](https://docs.microsoft.com/windows-hardware/drivers/network/native-802-11-ihv-extensibility-functions)」を参照してください。

-   [*Dot11ExtIhvAdapterReset*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_adapter_reset)関数が呼び出された場合、IHV 拡張 DLL は[**Dot11ExtPreAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_pre_associate_completion)を呼び出して、関連付け前の操作を取り消す必要があります。 リセット操作の詳細については、「 [802.11 WLAN Adapter reset](802-11-wlan-adapter-reset.md)」を参照してください。

-   [*Dot11ExtIhvDeinitAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)関数が呼び出された場合、IHV 拡張 DLL は、関連付け前の操作を内部的に取り消す必要があります。 ただし、 [**Dot11ExtPreAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_pre_associate_completion)を含め、アダプターの初期化後にのみ呼び出すことができる IHV 拡張関数を呼び出すことはできません。

 

 





