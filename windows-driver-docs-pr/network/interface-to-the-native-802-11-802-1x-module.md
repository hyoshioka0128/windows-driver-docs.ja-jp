---
title: ネイティブ 802.11 802.1X モジュールへのインターフェイス
description: ネイティブ 802.11 802.1X モジュールへのインターフェイス
ms.assetid: 8af78e5b-c9d9-4f07-8f07-f4a156ffdb9e
keywords:
- 後の関連付け操作 WDK ネイティブ 802.11 IHV 拡張 DLL
- 802.1 x モジュール WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d0831b2a20aa29a4f0afbb019acebfea99574f2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354990"
---
# <a name="interface-to-the-native-80211-8021x-module"></a>ネイティブ 802.11 802.1X モジュールへのインターフェイス




 

オペレーティング システムが、NDIS を受け取った後\_状態\_DOT11\_アソシエーション\_ネイティブ 802.11 ミニポート ドライバーから完了を示す値を呼び出し、 [ *Dot11ExtIhvPerformPostAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate) IHV 拡張機能の DLL によって後関連操作を開始する関数。

後の関連付け操作を実行している間、または、操作が完了した後は、IHV 拡張機能の DLL がアクセス ポイントにユーザーを認証するオペレーティング システムによってサポートされている拡張認証プロトコル (EAP) アルゴリズムを使用できます。(AP)。 このような状況で、EAP の AP で LAN (EAPOL) 形式で送信される EAP パケットの処理用のネイティブの 802.11 フレームワークの 802.1 X モジュールと IHV 拡張 DLL のインターフェイスします。

EAPOL 形式の詳細については、X-2001 標準の IEEE 802.1 句 7 を参照します。

802.1 X モジュールとネイティブの 802.11 フレームワークの詳細については、次を参照してください。[ネイティブ 802.11 ソフトウェア アーキテクチャ](native-802-11-software-architecture.md)します。

ユーザー認証用の 802.1 X モジュール インターフェイシングは、IHV 拡張機能の DLL は次のガイドラインに従う必要があります。

-   Windows vista の場合、IHV 拡張機能の DLL は、802.1 X のインフラストラクチャ サービスの基本的なセット (BSS) ネットワーク接続のみ、802.1 X モジュールから認証操作を開始できます。

-   IHV 拡張機能の DLL は、EAPOL パケットを受信するオペレーティング システムを登録する必要があります。 このような状況で、DLL を呼び出す必要があります、 [ **Dot11ExtSetEtherTypeHandling** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling)関数し、IEEE EAPOL EtherType (0x888E) を経由で渡される登録済みのEtherTypesの一覧に追加*pusRegistration*パラメーター。 オペレーティング システムが呼び出しを通じて IHV 拡張機能の DLL に受信の EAPOL パケットを転送、EtherType は、登録後、 [ *Dot11ExtIhvReceivePacket* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_receive_packet) IHV ハンドラー関数。

    EtherTypes の登録の詳細については、次を参照してください。 [IEEE EtherType 処理](ieee-ethertype-handling.md)します。

-   IHV 拡張機能の DLL が呼び出すことによって、802.1 X 認証操作を開始後の関連付け操作、実行中、 [ **Dot11ExtStartOneX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_onex_start)関数。 この関数が呼び出されると、オペレーティング システムは、次を行います。

    -   802.1 X 認証の構成のプロパティ ページを表示します。 この情報には、認証に使用される EAP アルゴリズムが含まれています。
    -   ユーザーに資格情報を要求する。
    -   802.1 X 認証を開始する ap、Eapol-start パケットを送信します。

    IHV 拡張機能の DLL を呼び出すことができます**Dot11ExtStartOneX**への呼び出し内で[ *Dot11ExtIhvPerformPostAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)または関数の後に呼び出しを返します。

-   IHV 拡張機能の DLL を呼び出すことができます、 [ **Dot11ExtStartOneX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_onex_start)ネイティブ 802.11 ミニポート ドライバーには、AP との関連付け操作が完了した後にのみ機能します。 このような状況で、IHV 拡張 DLL は呼び出す必要がありますいない、 **Dot11ExtStartOneX**関数は、次の条件のいずれか。
    -   オペレーティング システムの呼び出しの前に[ *Dot11ExtIhvPerformPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)します。 オペレーティング システムは、ミニポート ドライバーには、関連付け操作が正常に完了した後に、この関数を呼び出します。 この操作の詳細については、次を参照してください。[関連付け操作](association-operations.md)します。
    -   オペレーティング システムの呼び出し後[ *Dot11ExtIhvStopPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_stop_post_associate)します。 オペレーティング システムは、ミニポート ドライバーには、AP との関連付け解除操作が完了した後に、この関数を呼び出します。 この操作の詳細については、次を参照してください。[関連付け解除操作](disassociation-operations.md)します。
    -   オペレーティング システムの呼び出し後[ *Dot11ExtIhvAdapterReset*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_adapter_reset)します。 オペレーティング システムは、ミニポート ドライバーに基本的なサービスのセット (BSS) ネットワークを切断操作が完了した後に、この関数を呼び出します。 この操作の詳細については、次を参照してください。[切断操作](disconnection-operations.md)します。
-   IHV 拡張機能の DLL が呼び出すことによって、操作をキャンセルできます 802.1 X 認証操作の進行中は、 [ **Dot11ExtStopOneX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_onex_stop)します。

-   IHV 拡張機能の DLL を呼び出す必要があります、802.1 X 認証操作の進行中は、 [ **Dot11ExtProcessOneXPacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_process_onex_packet) EAPOL パケット処理用のオペレーティング システムを転送します。
    **注**  IHV 拡張 DLL は、AP から受信した Eapol-key パケットの処理を担当します。 DLL への呼び出しにより、オペレーティング システムにこれらのパケットを渡す必要がありますいない[ **Dot11ExtProcessOneXPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_process_onex_packet)します。

     

-   802.1 X 認証操作が完了したら、オペレーティング システムの呼び出し、 [ *Dot11ExtIhvOneXIndicateResult* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_onex_indicate_result) IHV ハンドラー関数。 この関数が呼び出されると、IHV 拡張機能の DLL は暗号キーの派生に使用する Eapol-key パケットなど、AP から受信したすべての EAPOL パケットの処理を担当します。

-   オペレーティング システムがする MPPE-送信-キーの値を渡します 802.1 X 認証操作が正常に完了している場合、 [ **DOT11\_MSONEX\_結果\_PARAMS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/ns-wlanihv-_dot11_msonex_result_params)によって示される構造体、 *pDot11MsOneXResultParams*パラメーターの[ *Dot11ExtIhvOneXIndicateResult*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_onex_indicate_result)します。 指す MPPE-送信-キー値、 **pbMPPESendKey** DOT11 のメンバー\_MSONEX\_結果\_PARAMS は、認証プロセスは派生し、IHV 拡張機能の DLL によって使用時にAP に Eapol-key パケットを送信します。 このキーは暗号化されており、呼び出すことによって復号化する必要があります、 **CryptUnprotectData** Windows SDK に記載されている関数。

-   暗号キーを派生させるために使用されるアルゴリズムは、独立系ハードウェア ベンダー (IHV) の実装によって異なります。 IHV 拡張機能の DLL は、IEEE 802.11i の句 8.5 で定義されているアルゴリズムなどの標準キー派生アルゴリズムをサポートできる、同様に 2004 standard では、独自のキー派生アルゴリズムをサポートできます。

-   キー派生後、IHV 拡張機能の DLL は、ワイヤレス LAN (WLAN) アダプターを管理するネイティブの 802.11 ミニポート ドライバーに暗号キーをダウンロードするには、次の関数を呼び出すことができます。

    -   [**Dot11ExtSetDefaultKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_default_key)

    -   [**Dot11ExtSetDefaultKeyId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_default_key_id)

    -   [**Dot11ExtSetKeyMappingKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_key_mapping_key)

-   IHV 拡張機能の DLL が呼び出すことにより、後の関連付け操作を完了、 [ **Dot11ExtPostAssociateCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)関数。 後の関連付け操作が完了すると、IHV 拡張機能の DLL は、ユーザーを再認証する必要がある、DLL と判断した場合別の 802.1 X 認証操作を開始できます。

次の図は、IHV 拡張機能の DLL は、後の関連付け操作中に 802.1 X 認証操作を開始したときにイベントの順序を示します。

![一連の ihv 拡張機能の dll は、後の関連付け操作中に、802.1 x 認証の操作を開始したときにイベントを示す図](images/ihv-ext-802.1x.png)

 

 





