---
title: 関連付け前の操作の概要
description: 関連付け前の操作の概要
ms.assetid: c33cf228-720f-4204-820c-0fb9a288bc6e
keywords:
- 前の関連付け操作 WDK ネイティブ 802.11 IHV 拡張 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c06e828d6712816d98a2bb20c1cb4a1f9d0baeac
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571402"
---
# <a name="pre-association-operation-overview"></a>関連付け前の操作の概要




 

オペレーティング システムの呼び出し、ユーザーが基本的なサービスのセット (BSS) ネットワーク接続のプロファイルを選択した後、 [ *Dot11ExtIhvPerformPreAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547499)関数は前の関連付けを開始するには操作です。 この関数が呼び出されると、IHV 拡張機能の DLL は、次を行います。

-   接続とセキュリティ プロファイルを IHV で定義された拡張機能を確認します。

    IHV 拡張機能の DLL は、プロファイルが正しくないことを判断した場合は、Winerror.h で定義されている、該当するエラー コードを返します。 このような状況では、オペレーティング システムは、ネットワーク プロファイルを使用できないことをユーザーに通知します。

-   接続とセキュリティ プロファイルを IHV で定義された拡張機能に基づく関連付け前の操作を開始します。

    前の関連付け操作が開始された後に完了する必要が非同期的にへの呼び出しから[ *Dot11ExtIhvPerformPreAssociate*](https://msdn.microsoft.com/library/windows/hardware/ff547499)します。

IHV 拡張機能の DLL を呼び出すことによって、関連付け前操作が完了すると[ **Dot11ExtPreAssociateCompletion**](https://msdn.microsoft.com/library/windows/hardware/ff547538)します。 この呼び出しでは、次のオペレーティング システムがのセット要求を発行して接続操作を開始[OID\_DOT11\_CONNECT\_要求](https://msdn.microsoft.com/library/windows/hardware/ff569122)ネイティブ 802.11 ミニポート ドライバーを管理WLAN アダプター。

次の図では、前の関連付け操作中に関連する手順を示します。

![関連付け前の操作中に必要な手順を示す図](images/ihv-ext-preassoc.png)

ときに[ *Dot11ExtIhvPerformPreAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547499)を呼び出すと、接続とセキュリティを IHV で定義された拡張機能は、次のパラメーターからプロファイル、オペレーティング システムのパス。

<a href="" id="pihvprofileparams"></a>*pIhvProfileParams*  
このパラメーターへのポインターが渡される、 [ **DOT11EXT\_IHV\_プロファイル\_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff547630)構造体は、基本的なサービスの属性を指定します (BSS) を設定します。ネットワーク プロファイルの適用先となるネットワーク。 たとえば、 **DOT11EXT\_IHV\_プロファイル\_PARAMS**構造体は、サービス セット識別子 (SSID) と BSS ネットワークの種類を指定します。

<a href="" id="pihvconnprofile"></a>*pIhvConnProfile*  
このパラメーターへのポインターが渡される、 [ **DOT11EXT\_IHV\_接続\_プロファイル**](https://msdn.microsoft.com/library/windows/hardware/ff547619)接続プロファイルの設定を含む構造体。 オペレーティング システムは、IHV によって定義され、ユーザーが選択した接続プロファイルにのみ、拡張機能を渡します。

<a href="" id="pihvsecprofile"></a>*pIhvSecProfile*  
このパラメーターへのポインターが渡される、 [ **DOT11EXT\_IHV\_セキュリティ\_プロファイル**](https://msdn.microsoft.com/library/windows/hardware/ff547632)セキュリティ プロファイルの設定を含む構造体。 オペレーティング システムは、IHV によって定義され、ユーザーが選択したセキュリティ プロファイルにのみ、拡張機能を渡します。

<a href="" id="pconnectablebssid"></a>*pConnectableBssid*  
このパラメーターへのポインターが渡される、 [ **DOT11\_BSS\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff547668)サービス セット識別子 (1 つまたは複数 802.11 ビーコンまたはプローブ応答フレームを含む構造体SSID) を DLL には関連付け前操作を実行する BSS ネットワーク。

関連付け前の操作を実行するときに IHV 拡張機能の DLL は、以下を実行できます。

-   呼び出す、 [ **Dot11ExtNicSpecificExtension** ](https://msdn.microsoft.com/library/windows/hardware/ff547526)ネイティブ 802.11 ミニポート ドライバーにネットワーク接続のための専用の構成要求を発行する関数。

    を通じて、 *pIhvConnProfile*と*pIhvProfileParams*パラメーター、IHV 拡張機能の DLL が独自の接続設定がユーザーによって選択されたを決定することができます。

    を通じて、 *pConnectableBssid*パラメーター、IHV 拡張機能の DLL を調べる BSS ネットワークの属性は、独自のネットワーク設定を構成に応じて。

-   BSS のネットワーク接続経由で使用する独自の認証と暗号アルゴリズムと WLAN のアダプターを構成します。

    を通じて、 *pszXmlFragmentIhvSecurity*独自仕様のセキュリティ アルゴリズムは、ユーザーによって選択されたパラメーター、IHV 拡張機能の DLL を確認できます。

    セキュリティ アルゴリズムを設定するのには、次の IHV 機能拡張関数を呼び出すことができます。

    -   [**Dot11ExtSetAuthAlgorithm**](https://msdn.microsoft.com/library/windows/hardware/ff547571)
    -   [**Dot11ExtSetUnicastCipherAlgorithm**](https://msdn.microsoft.com/library/windows/hardware/ff547606)
    -   [**Dot11ExtSetMulticastCipherAlgorithm**](https://msdn.microsoft.com/library/windows/hardware/ff547599)
-   呼び出す、 [ **Dot11ExtSendUIRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff547567) IHV UI 拡張機能の DLL がユーザーの資格情報などのセキュリティ パラメーターをユーザーに促すことを要求する関数。

-   呼び出す、 [ **Dot11ExtSetEtherTypeHandling** ](https://msdn.microsoft.com/library/windows/hardware/ff547587) DLL を受信するセキュリティ パケットに IEEE EtherTypes の一覧を登録する関数。 オペレーティング システムの呼び出しリストは、登録後、 [ *Dot11ExtIhvReceivePacket* ](https://msdn.microsoft.com/library/windows/hardware/ff547513)が EtherType には、リスト内のエントリが一致するすべてのパケットの IHV ハンドラー関数。

    IHV 拡張機能の DLL には、一連のペイロードの暗号化解除を除外 EtherTypes も指定できます。 EtherTypes の登録の詳細については、次を参照してください。 [IEEE EtherType 処理](ieee-ethertype-handling.md)します。

-   呼び出す、 [ **Dot11ExtSetProfileCustomUserData** ](https://msdn.microsoft.com/library/windows/hardware/ff547603)関数、ユーザーと現在の BSS ネットワーク プロファイルに固有のレジストリにデータを保存します。

-   呼び出す、 [ **Dot11ExtGetProfileCustomUserData** ](https://msdn.microsoft.com/library/windows/hardware/ff547430)関数、ユーザーと現在の BSS ネットワーク プロファイルに固有のレジストリからデータを取得します。

IHV 拡張機能の詳細については、次を参照してください。 [802.11 IHV 拡張関数をネイティブ](https://msdn.microsoft.com/library/windows/hardware/ff560609)します。

BSS ネットワークで接続操作の詳細については、次を参照してください。[接続操作](connection-operations.md)します。

 

 





