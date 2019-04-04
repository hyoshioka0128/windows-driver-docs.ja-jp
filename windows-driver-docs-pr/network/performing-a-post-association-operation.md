---
title: 関連付け後の操作の実行
description: 関連付け後の操作の実行
ms.assetid: b029d499-a23d-4f2f-aa28-2e8bfb2a00e5
keywords:
- 後の関連付け操作 WDK ネイティブ 802.11 IHV 拡張 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7fceb3213d631ca3aa10163af8f7efefb18556bb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570747"
---
# <a name="performing-a-post-association-operation"></a>関連付け後の操作の実行




 

ワイヤレス LAN (WLAN) アダプターには、アクセス ポイント (AP) の 802.11 関連付け操作は正常に完了すると、ネイティブ 802.11 ミニポート ドライバーには、ことで、オペレーティング システムを通知する[NDIS\_状態\_DOT11\_アソシエーション\_完了](https://msdn.microsoft.com/library/windows/hardware/ff567319)を示す値。 関連付け操作の詳細については、[関連付け操作](association-operations.md)を参照してください。

**注**  Windows Vista の IHV 拡張機能の DLL は、基本的なサービスのインフラストラクチャ (BSS) ネットワークの設定のみをサポートします。

 

オペレーティング システムが、NDIS を受け取った後\_状態\_DOT11\_アソシエーション\_呼び出しの完了を示す値を[ *Dot11ExtIhvPerformPostAssociate*](https://msdn.microsoft.com/library/windows/hardware/ff547492)に、次の IHV 拡張 DLL を通知する関数。

-   AP との関連付けの新しいデータ ポートを作成します。 IHV 拡張機能の DLL でのデータ ポートの現在の状態が渡される、 *pPortState*のパラメーター、 [ *Dot11ExtIhvPerformPostAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547492)関数。 ポートの状態パラメーターの詳細については、[ **DOT11\_ポート\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff548753)を参照してください。

-   ワイヤレス LAN (WLAN) アダプターと AP 間の関連付けのパラメーター。 IHV 拡張機能の DLL がを通じて関連付けパラメーターに渡される、 *pDot11AssocParams*のパラメーター、 [ *Dot11ExtIhvPerformPostAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547492)関数。 アソシエーション パラメータの詳細については、[ **DOT11\_アソシエーション\_完了\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff547647)を参照してください。

ときに[ *Dot11ExtIhvPerformPostAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547492)は IHV 拡張機能の DLL 呼び出されると、データ ポートを認証する AP と後の関連付け操作を開始します。 この操作を IHV 拡張機能の DLL は、次の方法ことができます。

-   新しいデータ ポートに必要なすべてのリソースを割り当てます。

-   独自のセキュリティ関連のデータ ポートで処理を実行します。 IHV 拡張機能の DLL からのデータ ポートの現在の状態を調べる*pPortState*のパラメーター、 [ *Dot11ExtIhvPerformPostAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547492)関数。

-   呼び出す、 [ **Dot11ExtSendUIRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff547567)ユーザーの資格情報などのセキュリティ パラメーターのユーザー入力を求める IHV UI 拡張機能の DLL を要求する関数。

-   認証を有効になっている認証アルゴリズムを使用する AP と[ **Dot11ExtSetAuthAlgorithm**](https://msdn.microsoft.com/library/windows/hardware/ff547571)します。 拡張 DLL の IHV 呼び出し**Dot11ExtSetAuthAlgorithm**関連付け前の操作中にします。 この操作の詳細については、[関連付け前操作](pre-association-operations.md)を参照してください。

-   呼び出しを通じて AP にセキュリティのパケットを送信、 [ **Dot11ExtSendPacket** ](https://msdn.microsoft.com/library/windows/hardware/ff547563)関数。

    セキュリティ パケットが送信されたときに、オペレーティング システムに通知、IHV 拡張機能の DLL を呼び出すことによって、 [ *Dot11ExtIhvSendPacketCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff547516)関数。

    セキュリティのパケットを送信する詳細については、[送信操作](send-operations.md)を参照してください。

-   AP からセキュリティ パケットを受信します。 オペレーティング システムの呼び出し、 [ *Dot11ExtIhvReceivePacket* ](https://msdn.microsoft.com/library/windows/hardware/ff547513) WLAN アダプターで受信した各セキュリティ パケットの関数。

    受信したセキュリティの各パケットでは、シリアル化され、WLAN アダプターから受信した順序で示されます。 オペレーティング システムのみを呼び出して、 [ *Dot11ExtIhvReceivePacket* ](https://msdn.microsoft.com/library/windows/hardware/ff547513)を IHV で指定された IEEE EtherTypes のリスト内のエントリと一致する受信したセキュリティ パケットを示すために関数呼び出すことによって拡張 DLL を[ **Dot11ExtSetEtherTypeHandling** ](https://msdn.microsoft.com/library/windows/hardware/ff547587)関数。

    セキュリティのパケットの受信の詳細については、[受信操作](receive-operations.md)を参照してください。

-   認証アルゴリズムから派生した暗号キーを使用して、WLAN アダプターを構成します。 WLAN アダプターに暗号キーをダウンロードするは、次の IHV 拡張関数を呼び出すことができます。
    -   [**Dot11ExtSetDefaultKey**](https://msdn.microsoft.com/library/windows/hardware/ff547578)
    -   [**Dot11ExtSetDefaultKeyId**](https://msdn.microsoft.com/library/windows/hardware/ff547584)
    -   [**Dot11ExtSetKeyMappingKey**](https://msdn.microsoft.com/library/windows/hardware/ff547597)
-   呼び出すことによって暗号化されていないパケットを除外する WLAN アダプターを構成、 [ **Dot11ExtSetExcludeUnencrypted** ](https://msdn.microsoft.com/library/windows/hardware/ff547589) IHV 拡張関数。

IHV 拡張機能の DLL を呼び出す必要がありますが、データ ポートの認証された後[ **Dot11ExtPostAssociateCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff547530)後関連操作を完了します。

次の図では、後の関連付け操作中に関連する手順を示します。

![後の関連付け操作中に必要な手順を示す図](images/ihv-ext-postassoc.png)

後の関連付け操作を実行するときに、IHV 拡張機能の DLL はガイドラインに従ってする必要があります。

-   IHV 拡張機能の DLL を呼び出す必要があります[ **Dot11ExtPostAssociateCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff547530)への呼び出しから非同期的に[ *Dot11ExtIhvPerformPostAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547492).

-   後の関連付け操作を完了すると、IHV 拡張機能の DLL を呼び出すことができます[ **Dot11ExtPostAssociateCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff547530)データの認証の状態が変更を移植するたびにします。

-   場合、 [ *Dot11ExtIhvAdapterReset* ](https://msdn.microsoft.com/library/windows/hardware/ff547434)関数が呼び出されると、IHV 拡張機能の DLL が呼び出すことによってすべての保留中の後の関連付け操作を取り消す必要があります[ **Dot11ExtPostAssociateCompletion**](https://msdn.microsoft.com/library/windows/hardware/ff547530)します。 リセット操作の詳細については、[802.11 WLAN アダプターはリセット](802-11-wlan-adapter-reset.md)を参照してください。

-   場合、 [ *Dot11ExtIhvDeinitAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff547452)関数が呼び出されると、IHV 拡張機能の DLL が内部的に保留中のすべての後の関連付け操作を取り消す必要があります。 ただし、これを呼び出してはならないアダプターの初期化後にのみ呼び出すことができる IHV 拡張関数のいずれかを含む[ **Dot11ExtPostAssociateCompletion**](https://msdn.microsoft.com/library/windows/hardware/ff547530)します。 IHV 拡張機能の詳細については、[802.11 IHV 拡張関数をネイティブ](https://msdn.microsoft.com/library/windows/hardware/ff560609)を参照してください。

 

 





