---
title: ネイティブ 802.11 802.1X モジュールへのインターフェイス
description: ネイティブ 802.11 802.1X モジュールへのインターフェイス
ms.assetid: 8af78e5b-c9d9-4f07-8f07-f4a156ffdb9e
keywords:
- 後の関連付け操作 WDK ネイティブ 802.11 IHV 拡張 DLL
- 802.1 x モジュール WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1a7e66214cbb91b2adb545285e2ad0fcfa5e449
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571504"
---
# <a name="interface-to-the-native-80211-8021x-module"></a>ネイティブ 802.11 802.1X モジュールへのインターフェイス




 

オペレーティング システムが、NDIS を受け取った後\_状態\_DOT11\_アソシエーション\_ネイティブ 802.11 ミニポート ドライバーから完了を示す値を呼び出し、 [ *Dot11ExtIhvPerformPostAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547492) IHV 拡張機能の DLL によって後関連操作を開始する関数。

後の関連付け操作を実行している間、または、操作が完了した後は、IHV 拡張機能の DLL がアクセス ポイントにユーザーを認証するオペレーティング システムによってサポートされている拡張認証プロトコル (EAP) アルゴリズムを使用できます。(AP)。 このような状況で、EAP の AP で LAN (EAPOL) 形式で送信される EAP パケットの処理用のネイティブの 802.11 フレームワークの 802.1 X モジュールと IHV 拡張 DLL のインターフェイスします。

EAPOL 形式の詳細については、X-2001 標準の IEEE 802.1 句 7 を参照します。

802.1 X モジュールとネイティブの 802.11 フレームワークの詳細については、[ネイティブ 802.11 ソフトウェア アーキテクチャ](native-802-11-software-architecture.md)を参照してください。

ユーザー認証用の 802.1 X モジュール インターフェイシングは、IHV 拡張機能の DLL は次のガイドラインに従う必要があります。

-   Windows vista の場合、IHV 拡張機能の DLL は、802.1 X のインフラストラクチャ サービスの基本的なセット (BSS) ネットワーク接続のみ、802.1 X モジュールから認証操作を開始できます。

-   IHV 拡張機能の DLL は、EAPOL パケットを受信するオペレーティング システムを登録する必要があります。 このような状況で、DLL を呼び出す必要があります、 [ **Dot11ExtSetEtherTypeHandling** ](https://msdn.microsoft.com/library/windows/hardware/ff547587)関数し、IEEE EAPOL EtherType (0x888E) を経由で渡される登録済みのEtherTypesの一覧に追加*pusRegistration*パラメーター。 オペレーティング システムが呼び出しを通じて IHV 拡張機能の DLL に受信の EAPOL パケットを転送、EtherType は、登録後、 [ *Dot11ExtIhvReceivePacket* ](https://msdn.microsoft.com/library/windows/hardware/ff547513) IHV ハンドラー関数。

    EtherTypes の登録の詳細については、[IEEE EtherType 処理](ieee-ethertype-handling.md)を参照してください。

-   IHV 拡張機能の DLL が呼び出すことによって、802.1 X 認証操作を開始後の関連付け操作、実行中、 [ **Dot11ExtStartOneX** ](https://msdn.microsoft.com/library/windows/hardware/ff547610)関数。 この関数が呼び出されると、オペレーティング システムは、次を行います。

    -   802.1 X 認証の構成のプロパティ ページを表示します。 この情報には、認証に使用される EAP アルゴリズムが含まれています。
    -   ユーザーに資格情報を要求する。
    -   802.1 X 認証を開始する ap、Eapol-start パケットを送信します。

    IHV 拡張機能の DLL を呼び出すことができます**Dot11ExtStartOneX**への呼び出し内で[ *Dot11ExtIhvPerformPostAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547492)または関数の後に呼び出しを返します。

-   IHV 拡張機能の DLL を呼び出すことができます、 [ **Dot11ExtStartOneX** ](https://msdn.microsoft.com/library/windows/hardware/ff547610)ネイティブ 802.11 ミニポート ドライバーには、AP との関連付け操作が完了した後にのみ機能します。 このような状況で、IHV 拡張 DLL は呼び出す必要がありますいない、 **Dot11ExtStartOneX**関数は、次の条件のいずれか。
    -   オペレーティング システムの呼び出しの前に[ *Dot11ExtIhvPerformPostAssociate*](https://msdn.microsoft.com/library/windows/hardware/ff547492)します。 オペレーティング システムは、ミニポート ドライバーには、関連付け操作が正常に完了した後に、この関数を呼び出します。 この操作の詳細については、[関連付け操作](association-operations.md)を参照してください。
    -   オペレーティング システムの呼び出し後[ *Dot11ExtIhvStopPostAssociate*](https://msdn.microsoft.com/library/windows/hardware/ff547521)します。 オペレーティング システムは、ミニポート ドライバーには、AP との関連付け解除操作が完了した後に、この関数を呼び出します。 この操作の詳細については、[関連付け解除操作](disassociation-operations.md)を参照してください。
    -   オペレーティング システムの呼び出し後[ *Dot11ExtIhvAdapterReset*](https://msdn.microsoft.com/library/windows/hardware/ff547434)します。 オペレーティング システムは、ミニポート ドライバーに基本的なサービスのセット (BSS) ネットワークを切断操作が完了した後に、この関数を呼び出します。 この操作の詳細については、[切断操作](disconnection-operations.md)を参照してください。
-   IHV 拡張機能の DLL が呼び出すことによって、操作をキャンセルできます 802.1 X 認証操作の進行中は、 [ **Dot11ExtStopOneX**](https://msdn.microsoft.com/library/windows/hardware/ff547614)します。

-   IHV 拡張機能の DLL を呼び出す必要があります、802.1 X 認証操作の進行中は、 [ **Dot11ExtProcessOneXPacket** ](https://msdn.microsoft.com/library/windows/hardware/ff547541) EAPOL パケット処理用のオペレーティング システムを転送します。
    **注**  IHV 拡張 DLL は、AP から受信した Eapol-key パケットの処理を担当します。 DLL への呼び出しにより、オペレーティング システムにこれらのパケットを渡す必要がありますいない[ **Dot11ExtProcessOneXPacket**](https://msdn.microsoft.com/library/windows/hardware/ff547541)します。

     

-   802.1 X 認証操作が完了したら、オペレーティング システムの呼び出し、 [ *Dot11ExtIhvOneXIndicateResult* ](https://msdn.microsoft.com/library/windows/hardware/ff547482) IHV ハンドラー関数。 この関数が呼び出されると、IHV 拡張機能の DLL は暗号キーの派生に使用する Eapol-key パケットなど、AP から受信したすべての EAPOL パケットの処理を担当します。

-   オペレーティング システムがする MPPE-送信-キーの値を渡します 802.1 X 認証操作が正常に完了している場合、 [ **DOT11\_MSONEX\_結果\_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff548698)によって示される構造体、 *pDot11MsOneXResultParams*パラメーターの[ *Dot11ExtIhvOneXIndicateResult*](https://msdn.microsoft.com/library/windows/hardware/ff547482)します。 指す MPPE-送信-キー値、 **pbMPPESendKey** DOT11 のメンバー\_MSONEX\_結果\_PARAMS は、認証プロセスは派生し、IHV 拡張機能の DLL によって使用時にAP に Eapol-key パケットを送信します。 このキーは暗号化されており、呼び出すことによって復号化する必要があります、 **CryptUnprotectData** Windows SDK に記載されている関数。

-   暗号キーを派生させるために使用されるアルゴリズムは、独立系ハードウェア ベンダー (IHV) の実装によって異なります。 IHV 拡張機能の DLL は、IEEE 802.11i の句 8.5 で定義されているアルゴリズムなどの標準キー派生アルゴリズムをサポートできる、同様に 2004 standard では、独自のキー派生アルゴリズムをサポートできます。

-   キー派生後、IHV 拡張機能の DLL は、ワイヤレス LAN (WLAN) アダプターを管理するネイティブの 802.11 ミニポート ドライバーに暗号キーをダウンロードするには、次の関数を呼び出すことができます。

    -   [**Dot11ExtSetDefaultKey**](https://msdn.microsoft.com/library/windows/hardware/ff547578)

    -   [**Dot11ExtSetDefaultKeyId**](https://msdn.microsoft.com/library/windows/hardware/ff547584)

    -   [**Dot11ExtSetKeyMappingKey**](https://msdn.microsoft.com/library/windows/hardware/ff547597)

-   IHV 拡張機能の DLL が呼び出すことにより、後の関連付け操作を完了、 [ **Dot11ExtPostAssociateCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff547530)関数。 後の関連付け操作が完了すると、IHV 拡張機能の DLL は、ユーザーを再認証する必要がある、DLL と判断した場合別の 802.1 X 認証操作を開始できます。

次の図は、IHV 拡張機能の DLL は、後の関連付け操作中に 802.1 X 認証操作を開始したときにイベントの順序を示します。

![一連の ihv 拡張機能の dll は、後の関連付け操作中に、802.1 x 認証の操作を開始したときにイベントを示す図](images/ihv-ext-802.1x.png)

 

 





