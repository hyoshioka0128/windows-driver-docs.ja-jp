---
title: 関連付け前の操作ガイドライン
description: 関連付け前の操作ガイドライン
ms.assetid: 35e9b701-6d5d-4c76-80fc-bb146be1ddb1
keywords:
- 前の関連付け操作 WDK ネイティブ 802.11 IHV 拡張 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c8fdc546233bcea904f8f7547fb7a6d051202af
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356069"
---
# <a name="pre-association-operation-guidelines"></a>関連付け前の操作ガイドライン




 

関連付け前の操作を実行するときに、IHV 拡張機能の DLL は次のガイドラインに従う必要があります。

-   ときに、 [ *Dot11ExtIhvPerformPreAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate)関数が呼び出されると、IHV 拡張機能の DLL は、次を実行する必要があります。
    -   接続とセキュリティ プロファイルの IHV 拡張機能を確認します。 プロファイルのパラメーターが有効でない場合、 *Dot11ExtIhvPerformPreAssociate* Winerror.h で定義されている関数が適切なエラー コードを返します。
    -   作成し、関連付け前の操作の完了のための新しいスレッドを開始します。 呼び出しから関連付け前の操作を非同期的に完了する必要がありますので[ *Dot11ExtIhvPerformPreAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate)、IHV 拡張機能の DLL を呼び出す必要があります[ **Dot11ExtPreAssociateCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_pre_associate_completion)操作の完了後は、このスレッドから。
    -   エラーを返す\_関数呼び出しから成功します。 この時点では、ネットワーク プロファイルが有効では、前の関連付け操作が進行中、オペレーティング システムに通知されます。
-   IHV 拡張機能の DLL を呼び出すことができます、 [ **Dot11ExtNicSpecificExtension** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_nic_specific_extension)ワイヤレス LAN (WLAN) アダプターを構成する関数。 呼び出し内のいずれかからこの関数を呼び出すことが[ *Dot11ExtIhvPerformPreAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate)または関連付け前から、操作を処理するスレッドから*Dot11ExtIhvPerformPreAssociate*を返します。

-   呼び出し、 [ **Dot11ExtSetProfileCustomUserData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_profile_custom_user_data)、 [ **Dot11ExtGetProfileCustomUserData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_get_profile_custom_user_data)、および[ **Dot11ExtSetCurrentProfile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_current_profile)への呼び出し内から確立できません必要があります[ *Dot11ExtIhvPerformPreAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate)します。 これらの関数は、後にのみ呼び出すことができます*Dot11ExtIhvPerformPreAssociate*エラーが返されます\_成功します。

-   IHV 拡張 DLL の後に呼び出す[ **Dot11ExtPreAssociateCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_pre_associate_completion)関連付け前の操作を完了するには、接続のセッションのハンドルは無効になりました。 オペレーティング システムを使ってこのハンドルを渡す、 *hConnectSession*パラメーターの[ *Dot11ExtIhvPerformPreAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate)します。 宣言をすべての IHV 拡張関数を呼び出すときに、DLL がこのハンドル値を使用する必要があります、 *hConnectSession*パラメーター。

    IHV 拡張機能の詳細については、次を参照してください。 [802.11 IHV 拡張関数をネイティブ](https://docs.microsoft.com/windows-hardware/drivers/network/native-802-11-ihv-extensibility-functions)します。

-   場合、 [ *Dot11ExtIhvAdapterReset* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_adapter_reset)関数が呼び出されると、IHV 拡張機能の DLL が呼び出すことによって、関連付け前の操作を取り消す必要があります[ **Dot11ExtPreAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_pre_associate_completion)します。 リセット操作の詳細については、次を参照してください。 [802.11 WLAN アダプターはリセット](802-11-wlan-adapter-reset.md)します。

-   場合、 [ *Dot11ExtIhvDeinitAdapter* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)関数が呼び出されると、IHV 拡張機能の DLL が内部的には、関連付け前の操作を取り消す必要があります。 ただし、これを呼び出してはならないアダプターの初期化後にのみ呼び出すことができる IHV 拡張関数のいずれかを含む[ **Dot11ExtPreAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_pre_associate_completion)します。

 

 





