---
title: 関連付け後の操作の実行
description: 関連付け後の操作の実行
ms.assetid: b029d499-a23d-4f2f-aa28-2e8bfb2a00e5
keywords:
- アソシエーション後の操作 WDK ネイティブ 802.11 IHV 拡張 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5df8cb077fb86e4a1b9e034c07e3860ab4e16002
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843691"
---
# <a name="performing-a-post-association-operation"></a>関連付け後の操作の実行




 

ワイヤレス LAN (WLAN) アダプターがアクセスポイント (AP) と802.11 の関連付け操作を正常に完了すると、ネイティブ802.11 ミニポートドライバーは、 [\_DOT11\_関連付け\_完了](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-dot11-association-completion)を示すように、NDIS\_状態を作成することによって、オペレーティングシステムに通知します。 アソシエーション操作の詳細については、「[アソシエーション操作](association-operations.md)」を参照してください。

**注**  Windows Vista では、IHV 拡張 DLL は、インフラストラクチャの基本サービスセット (BSS) ネットワークのみをサポートしています。

 

オペレーティングシステムは、\_DOT11\_関連付け\_完了を示す\_状態を受信した後、 [*Dot11ExtIhvPerformPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)関数を呼び出して、次のことを IHV 拡張 DLL に通知します。

-   AP との関連付けに使用する新しいデータポートの作成。 IHV 拡張 DLL には、 [*Dot11ExtIhvPerformPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)関数の*pportstate*パラメーターを通じて、データポートの現在の状態が渡されます。 ポートの状態パラメーターの詳細については、「 [**DOT11\_ポート\_の状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlclient/ns-wlclient-_dot11_port_state)」を参照してください。

-   ワイヤレス LAN (WLAN) アダプターと AP 間の関連付けのパラメーター。 IHV 拡張 DLL には、 [*Dot11ExtIhvPerformPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)関数の*pDot11AssocParams*パラメーターを通じてアソシエーションパラメーターが渡されます。 アソシエーションパラメーターの詳細については、「 [**DOT11\_関連付け\_完了\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/windot11/ns-windot11-dot11_association_completion_parameters)」を参照してください。

[*Dot11ExtIhvPerformPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)が呼び出されると、IHV 拡張 DLL は、データポートを認証するための AP との関連付け後の操作を開始します。 この操作により、IHV 拡張 DLL は次のことを実行できます。

-   新しいデータポートに必要なリソースを割り当てます。

-   データポートで、関連する独自のセキュリティ処理を実行します。 IHV 拡張 DLL は、 [*Dot11ExtIhvPerformPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)関数の*pportstate*パラメーターからデータポートの現在の状態を特定できます。

-   [**Dot11ExtSendUIRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_ui_request)関数を呼び出して、ユーザーにユーザーの資格情報などのセキュリティパラメーターの入力を求めるメッセージを表示するように、IHV UI Extensions DLL を要求します。

-   [**Dot11ExtSetAuthAlgorithm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_auth_algorithm)によって有効にされた認証アルゴリズムを使用して、AP で認証します。 IHV 拡張 DLL は、関連付け前の操作中に**Dot11ExtSetAuthAlgorithm**を呼び出します。 この操作の詳細については、「[事前関連付け操作](pre-association-operations.md)」を参照してください。

-   [**Dot11ExtSendPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_packet)関数の呼び出しによって、セキュリティパケットを AP に送信します。

    セキュリティパケットが送信されると、操作は[*Dot11ExtIhvSendPacketCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_send_packet_completion)関数の呼び出しを通じて、IHV 拡張 DLL に通知します。

    セキュリティパケットの送信の詳細については、「[送信操作](send-operations.md)」を参照してください。

-   AP からセキュリティパケットを受信します。 オペレーティングシステムは、WLAN アダプターによって受信された各セキュリティパケットに対して[*Dot11ExtIhvReceivePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_receive_packet)関数を呼び出します。

    受信した各セキュリティパケットは、WLAN アダプターから受信した順序でシリアル化され、示されます。 オペレーティングシステムは、 [*Dot11ExtIhvReceivePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_receive_packet)関数を呼び出して、 [**Dot11ExtSetEtherTypeHandling**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling)関数の呼び出しによって IHV 拡張 DLL によって指定された、IEEE EtherTypes の一覧のエントリと一致する受信したセキュリティパケットを示します。

    セキュリティパケットを受信する方法の詳細については、「[受信操作](receive-operations.md)」を参照してください。

-   認証アルゴリズムを通じて派生した暗号キーを使用して WLAN アダプターを構成します。 次の IHV 機能拡張関数を呼び出して、暗号化キーを WLAN アダプターにダウンロードできます。
    -   [**Dot11ExtSetDefaultKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_default_key)
    -   [**Dot11ExtSetDefaultKeyId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_default_key_id)
    -   [**Dot11ExtSetKeyMappingKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_key_mapping_key)
-   [**Dot11ExtSetExcludeUnencrypted**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_exclude_unencrypted) IHV 拡張機能の呼び出しによって暗号化されていないパケットを除外するように、WLAN アダプターを構成します。

データポートが認証された後、IHV 拡張 DLL は[**Dot11ExtPostAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)を呼び出して、関連付け後の操作を完了する必要があります。

次の図は、関連付け後の操作中に必要な手順を示しています。

![関連付け後の操作中に必要な手順を示す図](images/ihv-ext-postassoc.png)

IHV 拡張 DLL は、関連付け後の操作を実行するときに、次のガイドラインに従う必要があります。

-   IHV 拡張 DLL は、 [*Dot11ExtIhvPerformPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)への呼び出しから非同期的に[**Dot11ExtPostAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)を呼び出す必要があります。

-   関連付け後の操作が完了すると、データポートの認証状態が変更されるたびに、IHV 拡張 DLL は[**Dot11ExtPostAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)を呼び出すことができます。

-   [*Dot11ExtIhvAdapterReset*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_adapter_reset)関数が呼び出された場合、IHV 拡張 DLL は[**Dot11ExtPostAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)を呼び出して、保留中のすべてのポストアソシエーション操作をキャンセルする必要があります。 リセット操作の詳細については、「 [802.11 WLAN Adapter reset](802-11-wlan-adapter-reset.md)」を参照してください。

-   [*Dot11ExtIhvDeinitAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)関数が呼び出された場合、IHV 拡張 DLL は、保留中のすべてのポストアソシエーション操作を内部的にキャンセルする必要があります。 ただし、 [**Dot11ExtPostAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)を含め、アダプターの初期化後にのみ呼び出すことができる IHV 拡張関数を呼び出すことはできません。 IHV 拡張機能の詳細については、「[ネイティブ 802.11 Ihv 拡張関数](https://docs.microsoft.com/windows-hardware/drivers/network/native-802-11-ihv-extensibility-functions)」を参照してください。

 

 





