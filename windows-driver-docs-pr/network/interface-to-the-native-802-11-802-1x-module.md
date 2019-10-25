---
title: ネイティブ 802.11 802.1X モジュールへのインターフェイス
description: ネイティブ 802.11 802.1X モジュールへのインターフェイス
ms.assetid: 8af78e5b-c9d9-4f07-8f07-f4a156ffdb9e
keywords:
- アソシエーション後の操作 WDK ネイティブ 802.11 IHV 拡張 DLL
- 802.1 x モジュール WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea63a0ffc55be888a18963337cfc140ec851c20b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844189"
---
# <a name="interface-to-the-native-80211-8021x-module"></a>ネイティブ 802.11 802.1X モジュールへのインターフェイス




 

オペレーティングシステムは、ネイティブ802.11 ミニポートドライバーからの NDIS\_状態\_DOT11\_関連付け\_完了を受信した後、 [*Dot11ExtIhvPerformPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)関数を呼び出して、IHV 拡張 DLL による関連付け後の操作です。

関連付け後の操作を実行するとき、または操作が完了した後に、IHV 拡張 DLL は、オペレーティングシステムでサポートされている拡張認証プロトコル (EAP) アルゴリズムを使用して、アクセスポイントでユーザーを認証することができます。(AP)。 この状況では、IHV 拡張 DLL は、EAP over LAN (EAPOL) 形式で AP によって送信された EAP パケットの処理のために、ネイティブ802.11 フレームワークの 802.1 X モジュールとインターフェイスします。

EAPOL 形式の詳細については、IEEE 802.1 X-2001 標準の句7を参照してください。

802.1 X モジュールとネイティブ802.11 フレームワークの詳細については、「[ネイティブ802.11 ソフトウェアアーキテクチャ](native-802-11-software-architecture.md)」を参照してください。

ユーザー認証のために 802.1 X モジュールをインターフェイスする場合、IHV 拡張 DLL は次のガイドラインに従う必要があります。

-   Windows Vista の場合、IHV Extensions DLL は、802.1 X モジュールを介して 802.1 X 認証操作を開始できます。これは、インフラストラクチャの基本サービスセット (BSS) のネットワーク接続の場合のみです。

-   EAPOL パケットを受信するには、IHV 拡張 DLL をオペレーティングシステムに登録する必要があります。 この場合、DLL は[**Dot11ExtSetEtherTypeHandling**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling)関数を呼び出し、 *pusRegistration*パラメーターを通じて渡される登録済みの ETHERTYPES のリストに IEEE EAPOL EtherType (0x888 e) を追加する必要があります。 EtherType が登録されると、オペレーティングシステムは、 [*Dot11ExtIhvReceivePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_receive_packet) ihv ハンドラー関数の呼び出しを通じて、受信した EAPOL パケットを IHV 拡張 DLL に転送します。

    EtherTypes の登録の詳細については、「 [IEEE EtherType の処理](ieee-ethertype-handling.md)」を参照してください。

-   関連付け後の操作を実行している間、IHV 拡張 DLL は[**Dot11ExtStartOneX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_onex_start)関数を呼び出して 802.1 x 認証操作を開始します。 この関数が呼び出されると、オペレーティングシステムは次の処理を実行します。

    -   802.1 X 認証の構成のプロパティページを表示します。 この情報には、認証に使用される EAP アルゴリズムが含まれます。
    -   ユーザーに資格情報の入力を求めます。
    -   802.1 X 認証を開始するには、EAPOL 開始パケットを AP に送信します。

    IHV 拡張 DLL は、 [*Dot11ExtIhvPerformPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)の呼び出し内、または関数呼び出しが返された後に、 **Dot11ExtStartOneX**を呼び出すことができます。

-   IHV 拡張 DLL は、ネイティブ802.11 ミニポートドライバーが AP との関連付け操作を完了した後にのみ、 [**Dot11ExtStartOneX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_onex_start)関数を呼び出すことができます。 この場合、IHV 拡張 DLL は、次のいずれかの条件下で**Dot11ExtStartOneX**関数を呼び出すことはできません。
    -   オペレーティングシステムが[*Dot11ExtIhvPerformPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)を呼び出す前。 オペレーティングシステムは、ミニポートドライバーがアソシエーション操作を正常に完了した後に、この関数を呼び出します。 この操作の詳細については、「[アソシエーション操作](association-operations.md)」を参照してください。
    -   オペレーティングシステムが[*Dot11ExtIhvStopPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_stop_post_associate)を呼び出した後。 オペレーティングシステムは、ミニポートドライバーが AP との関連付け操作を完了した後に、この関数を呼び出します。 この操作の詳細については、「[関連付け Operations](disassociation-operations.md)」を参照してください。
    -   オペレーティングシステムが[*Dot11ExtIhvAdapterReset*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_adapter_reset)を呼び出した後。 オペレーティングシステムは、ミニポートドライバーが基本サービスセット (BSS) ネットワークを使用して切断操作を完了した後に、この関数を呼び出します。 この操作の詳細については、「[切断操作](disconnection-operations.md)」を参照してください。
-   802.1 X 認証操作の実行中は、IHV 拡張 DLL は[**Dot11ExtStopOneX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_onex_stop)を呼び出して操作を取り消すことができます。

-   802.1 X 認証操作の実行中は、IHV 拡張 DLL が[**Dot11ExtProcessOneXPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_process_onex_packet)を呼び出して、EAPOL パケットを処理のためにオペレーティングシステムに転送する必要があります。
    IHV 拡張 DLL は、AP から受信した EAPOL キーパケットの処理を担当し  **ことに注意**してください。 DLL は、 [**Dot11ExtProcessOneXPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_process_onex_packet)を呼び出すことによって、これらのパケットをオペレーティングシステムに渡すことはできません。

     

-   802.1 X 認証操作が完了すると、オペレーティングシステムは[*Dot11ExtIhvOneXIndicateResult*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_onex_indicate_result) IHV ハンドラー関数を呼び出します。 この関数が呼び出された後、IHV 拡張 DLL は、暗号キーの派生に使用される EAPOL キーパケットなど、AP から受信したすべての EAPOL パケットを処理します。

-   802.1 X 認証操作が正常に完了した場合、オペレーティングシステムは*pDot11MsOneXResultParams*によってポイントされている[**DOT11\_MSONEX onex の結果\_PARAMS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11_msonex_result_params)構造に MPPE-送信キーの値を渡します。[*Dot11ExtIhvOneXIndicateResult*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_onex_indicate_result)のパラメーター。 DOT11\_MSONEX\_RESULT\_PARAMS の**pbMPPESendKey**メンバーによってポイントされる MPPE-送信キーの値は、認証プロセスを通じて派生し、EAPOL キーパケットを AP に送信するときに IHV 拡張 DLL によって使用されます。 このキーは暗号化されており、Windows SDK に記載されている**CryptUnprotectData**関数を呼び出すことによって暗号化を解除する必要があります。

-   暗号キーの派生に使用されるアルゴリズムは、独立系ハードウェアベンダー (IHV) の実装に依存します。 IHV 拡張 DLL は、IEEE 802.11 の i-2004 標準の句8.5 で定義されているアルゴリズムなどの標準キー派生アルゴリズムをサポートできます。また、独自のキー派生アルゴリズムをサポートすることもできます。

-   IHV 拡張 DLL は、キーを取得した後、次の関数を呼び出して、ワイヤレス LAN (WLAN) アダプターを管理するネイティブ802.11 ミニポートドライバーに暗号キーをダウンロードできます。

    -   [**Dot11ExtSetDefaultKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_default_key)

    -   [**Dot11ExtSetDefaultKeyId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_default_key_id)

    -   [**Dot11ExtSetKeyMappingKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_key_mapping_key)

-   IHV Extensions DLL は、 [**Dot11ExtPostAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)関数を呼び出すことによって、関連付け後の操作を完了します。 関連付け後の操作が完了すると、ユーザーが再認証される必要があると DLL が判断した場合、IHV 拡張 DLL は別の 802.1 X 認証操作を開始できます。

次の図は、IHV Extensions DLL がアソシエーション後の操作中に 802.1 X 認証操作を開始するときのイベントのシーケンスを示しています。

![アソシエーションの操作中に ihv 拡張 dll が 802.1 x 認証操作を開始したときの一連のイベントを示す図](images/ihv-ext-802.1x.png)

 

 





