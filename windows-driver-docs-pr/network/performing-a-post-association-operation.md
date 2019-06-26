---
title: 関連付け後の操作の実行
description: 関連付け後の操作の実行
ms.assetid: b029d499-a23d-4f2f-aa28-2e8bfb2a00e5
keywords:
- 後の関連付け操作 WDK ネイティブ 802.11 IHV 拡張 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9dadc0f245427398f7c93b831220a08c8ee8451
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384541"
---
# <a name="performing-a-post-association-operation"></a>関連付け後の操作の実行




 

ワイヤレス LAN (WLAN) アダプターには、アクセス ポイント (AP) の 802.11 関連付け操作は正常に完了すると、ネイティブ 802.11 ミニポート ドライバーには、ことで、オペレーティング システムを通知する[NDIS\_状態\_DOT11\_アソシエーション\_完了](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-dot11-association-completion)を示す値。 関連付け操作の詳細については、次を参照してください。[関連付け操作](association-operations.md)します。

**注**  Windows Vista の IHV 拡張機能の DLL は、基本的なサービスのインフラストラクチャ (BSS) ネットワークの設定のみをサポートします。

 

オペレーティング システムが、NDIS を受け取った後\_状態\_DOT11\_アソシエーション\_呼び出しの完了を示す値を[ *Dot11ExtIhvPerformPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)に、次の IHV 拡張 DLL を通知する関数。

-   AP との関連付けの新しいデータ ポートを作成します。 IHV 拡張機能の DLL でのデータ ポートの現在の状態が渡される、 *pPortState*のパラメーター、 [ *Dot11ExtIhvPerformPostAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)関数。 ポートの状態パラメーターの詳細については、次を参照してください。 [ **DOT11\_ポート\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlclient/ns-wlclient-_dot11_port_state)します。

-   ワイヤレス LAN (WLAN) アダプターと AP 間の関連付けのパラメーター。 IHV 拡張機能の DLL がを通じて関連付けパラメーターに渡される、 *pDot11AssocParams*のパラメーター、 [ *Dot11ExtIhvPerformPostAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)関数。 アソシエーション パラメータの詳細については、次を参照してください。 [ **DOT11\_アソシエーション\_完了\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/windot11/ns-windot11-dot11_association_completion_parameters)します。

ときに[ *Dot11ExtIhvPerformPostAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)は IHV 拡張機能の DLL 呼び出されると、データ ポートを認証する AP と後の関連付け操作を開始します。 この操作を IHV 拡張機能の DLL は、次の方法ことができます。

-   新しいデータ ポートに必要なすべてのリソースを割り当てます。

-   独自のセキュリティ関連のデータ ポートで処理を実行します。 IHV 拡張機能の DLL からのデータ ポートの現在の状態を調べる*pPortState*のパラメーター、 [ *Dot11ExtIhvPerformPostAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)関数。

-   呼び出す、 [ **Dot11ExtSendUIRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_send_ui_request)ユーザーの資格情報などのセキュリティ パラメーターのユーザー入力を求める IHV UI 拡張機能の DLL を要求する関数。

-   認証を有効になっている認証アルゴリズムを使用する AP と[ **Dot11ExtSetAuthAlgorithm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_auth_algorithm)します。 拡張 DLL の IHV 呼び出し**Dot11ExtSetAuthAlgorithm**関連付け前の操作中にします。 この操作の詳細については、次を参照してください。[関連付け前操作](pre-association-operations.md)します。

-   呼び出しを通じて AP にセキュリティのパケットを送信、 [ **Dot11ExtSendPacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_send_packet)関数。

    セキュリティ パケットが送信されたときに、オペレーティング システムに通知、IHV 拡張機能の DLL を呼び出すことによって、 [ *Dot11ExtIhvSendPacketCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_send_packet_completion)関数。

    セキュリティのパケットを送信する詳細については、次を参照してください。[送信操作](send-operations.md)します。

-   AP からセキュリティ パケットを受信します。 オペレーティング システムの呼び出し、 [ *Dot11ExtIhvReceivePacket* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_receive_packet) WLAN アダプターで受信した各セキュリティ パケットの関数。

    受信したセキュリティの各パケットでは、シリアル化され、WLAN アダプターから受信した順序で示されます。 オペレーティング システムのみを呼び出して、 [ *Dot11ExtIhvReceivePacket* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_receive_packet)を IHV で指定された IEEE EtherTypes のリスト内のエントリと一致する受信したセキュリティ パケットを示すために関数呼び出すことによって拡張 DLL を[ **Dot11ExtSetEtherTypeHandling** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling)関数。

    セキュリティのパケットの受信の詳細については、次を参照してください。[受信操作](receive-operations.md)します。

-   認証アルゴリズムから派生した暗号キーを使用して、WLAN アダプターを構成します。 WLAN アダプターに暗号キーをダウンロードするは、次の IHV 拡張関数を呼び出すことができます。
    -   [**Dot11ExtSetDefaultKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_default_key)
    -   [**Dot11ExtSetDefaultKeyId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_default_key_id)
    -   [**Dot11ExtSetKeyMappingKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_key_mapping_key)
-   呼び出すことによって暗号化されていないパケットを除外する WLAN アダプターを構成、 [ **Dot11ExtSetExcludeUnencrypted** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_exclude_unencrypted) IHV 拡張関数。

IHV 拡張機能の DLL を呼び出す必要がありますが、データ ポートの認証された後[ **Dot11ExtPostAssociateCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)後関連操作を完了します。

次の図では、後の関連付け操作中に関連する手順を示します。

![後の関連付け操作中に必要な手順を示す図](images/ihv-ext-postassoc.png)

後の関連付け操作を実行するときに、IHV 拡張機能の DLL はガイドラインに従ってする必要があります。

-   IHV 拡張機能の DLL を呼び出す必要があります[ **Dot11ExtPostAssociateCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)への呼び出しから非同期的に[ *Dot11ExtIhvPerformPostAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate).

-   後の関連付け操作を完了すると、IHV 拡張機能の DLL を呼び出すことができます[ **Dot11ExtPostAssociateCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)データの認証の状態が変更を移植するたびにします。

-   場合、 [ *Dot11ExtIhvAdapterReset* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_adapter_reset)関数が呼び出されると、IHV 拡張機能の DLL が呼び出すことによってすべての保留中の後の関連付け操作を取り消す必要があります[ **Dot11ExtPostAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)します。 リセット操作の詳細については、次を参照してください。 [802.11 WLAN アダプターはリセット](802-11-wlan-adapter-reset.md)します。

-   場合、 [ *Dot11ExtIhvDeinitAdapter* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)関数が呼び出されると、IHV 拡張機能の DLL が内部的に保留中のすべての後の関連付け操作を取り消す必要があります。 ただし、これを呼び出してはならないアダプターの初期化後にのみ呼び出すことができる IHV 拡張関数のいずれかを含む[ **Dot11ExtPostAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)します。 IHV 拡張機能の詳細については、次を参照してください。 [802.11 IHV 拡張関数をネイティブ](https://docs.microsoft.com/windows-hardware/drivers/network/native-802-11-ihv-extensibility-functions)します。

 

 





