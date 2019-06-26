---
title: 関連付け前の操作の概要
description: 関連付け前の操作の概要
ms.assetid: c33cf228-720f-4204-820c-0fb9a288bc6e
keywords:
- 前の関連付け操作 WDK ネイティブ 802.11 IHV 拡張 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 571970eac72647cdecf1deab235bc0f50f3ae6fa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385488"
---
# <a name="pre-association-operation-overview"></a>関連付け前の操作の概要




 

オペレーティング システムの呼び出し、ユーザーが基本的なサービスのセット (BSS) ネットワーク接続のプロファイルを選択した後、 [ *Dot11ExtIhvPerformPreAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate)関数は前の関連付けを開始するには操作です。 この関数が呼び出されると、IHV 拡張機能の DLL は、次を行います。

-   接続とセキュリティ プロファイルを IHV で定義された拡張機能を確認します。

    IHV 拡張機能の DLL は、プロファイルが正しくないことを判断した場合は、Winerror.h で定義されている、該当するエラー コードを返します。 このような状況では、オペレーティング システムは、ネットワーク プロファイルを使用できないことをユーザーに通知します。

-   接続とセキュリティ プロファイルを IHV で定義された拡張機能に基づく関連付け前の操作を開始します。

    前の関連付け操作が開始された後に完了する必要が非同期的にへの呼び出しから[ *Dot11ExtIhvPerformPreAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate)します。

IHV 拡張機能の DLL を呼び出すことによって、関連付け前操作が完了すると[ **Dot11ExtPreAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_pre_associate_completion)します。 この呼び出しでは、次のオペレーティング システムがのセット要求を発行して接続操作を開始[OID\_DOT11\_CONNECT\_要求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-dot11-connect-request)ネイティブ 802.11 ミニポート ドライバーを管理WLAN アダプター。

次の図では、前の関連付け操作中に関連する手順を示します。

![関連付け前の操作中に必要な手順を示す図](images/ihv-ext-preassoc.png)

ときに[ *Dot11ExtIhvPerformPreAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate)を呼び出すと、接続とセキュリティを IHV で定義された拡張機能は、次のパラメーターからプロファイル、オペレーティング システムのパス。

<a href="" id="pihvprofileparams"></a>*pIhvProfileParams*  
このパラメーターへのポインターが渡される、 [ **DOT11EXT\_IHV\_プロファイル\_PARAMS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihvtypes/ns-wlanihvtypes-_dot11ext_ihv_profile_params)構造体は、基本的なサービスの属性を指定します (BSS) を設定します。ネットワーク プロファイルの適用先となるネットワーク。 たとえば、 **DOT11EXT\_IHV\_プロファイル\_PARAMS**構造体は、サービス セット識別子 (SSID) と BSS ネットワークの種類を指定します。

<a href="" id="pihvconnprofile"></a>*pIhvConnProfile*  
このパラメーターへのポインターが渡される、 [ **DOT11EXT\_IHV\_接続\_プロファイル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/ns-wlanihv-_dot11ext_ihv_connectivity_profile)接続プロファイルの設定を含む構造体。 オペレーティング システムは、IHV によって定義され、ユーザーが選択した接続プロファイルにのみ、拡張機能を渡します。

<a href="" id="pihvsecprofile"></a>*pIhvSecProfile*  
このパラメーターへのポインターが渡される、 [ **DOT11EXT\_IHV\_セキュリティ\_プロファイル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/ns-wlanihv-_dot11ext_ihv_security_profile)セキュリティ プロファイルの設定を含む構造体。 オペレーティング システムは、IHV によって定義され、ユーザーが選択したセキュリティ プロファイルにのみ、拡張機能を渡します。

<a href="" id="pconnectablebssid"></a>*pConnectableBssid*  
このパラメーターへのポインターが渡される、 [ **DOT11\_BSS\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlclient/ns-wlclient-_dot11_bss_list)サービス セット識別子 (1 つまたは複数 802.11 ビーコンまたはプローブ応答フレームを含む構造体SSID) を DLL には関連付け前操作を実行する BSS ネットワーク。

関連付け前の操作を実行するときに IHV 拡張機能の DLL は、以下を実行できます。

-   呼び出す、 [ **Dot11ExtNicSpecificExtension** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_nic_specific_extension)ネイティブ 802.11 ミニポート ドライバーにネットワーク接続のための専用の構成要求を発行する関数。

    を通じて、 *pIhvConnProfile*と*pIhvProfileParams*パラメーター、IHV 拡張機能の DLL が独自の接続設定がユーザーによって選択されたを決定することができます。

    を通じて、 *pConnectableBssid*パラメーター、IHV 拡張機能の DLL を調べる BSS ネットワークの属性は、独自のネットワーク設定を構成に応じて。

-   BSS のネットワーク接続経由で使用する独自の認証と暗号アルゴリズムと WLAN のアダプターを構成します。

    を通じて、 *pszXmlFragmentIhvSecurity*独自仕様のセキュリティ アルゴリズムは、ユーザーによって選択されたパラメーター、IHV 拡張機能の DLL を確認できます。

    セキュリティ アルゴリズムを設定するのには、次の IHV 機能拡張関数を呼び出すことができます。

    -   [**Dot11ExtSetAuthAlgorithm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_auth_algorithm)
    -   [**Dot11ExtSetUnicastCipherAlgorithm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_unicast_cipher_algorithm)
    -   [**Dot11ExtSetMulticastCipherAlgorithm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_multicast_cipher_algorithm)
-   呼び出す、 [ **Dot11ExtSendUIRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_send_ui_request) IHV UI 拡張機能の DLL がユーザーの資格情報などのセキュリティ パラメーターをユーザーに促すことを要求する関数。

-   呼び出す、 [ **Dot11ExtSetEtherTypeHandling** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling) DLL を受信するセキュリティ パケットに IEEE EtherTypes の一覧を登録する関数。 オペレーティング システムの呼び出しリストは、登録後、 [ *Dot11ExtIhvReceivePacket* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_receive_packet)が EtherType には、リスト内のエントリが一致するすべてのパケットの IHV ハンドラー関数。

    IHV 拡張機能の DLL には、一連のペイロードの暗号化解除を除外 EtherTypes も指定できます。 EtherTypes の登録の詳細については、次を参照してください。 [IEEE EtherType 処理](ieee-ethertype-handling.md)します。

-   呼び出す、 [ **Dot11ExtSetProfileCustomUserData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_profile_custom_user_data)関数、ユーザーと現在の BSS ネットワーク プロファイルに固有のレジストリにデータを保存します。

-   呼び出す、 [ **Dot11ExtGetProfileCustomUserData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_get_profile_custom_user_data)関数、ユーザーと現在の BSS ネットワーク プロファイルに固有のレジストリからデータを取得します。

IHV 拡張機能の詳細については、次を参照してください。 [802.11 IHV 拡張関数をネイティブ](https://docs.microsoft.com/windows-hardware/drivers/network/native-802-11-ihv-extensibility-functions)します。

BSS ネットワークで接続操作の詳細については、次を参照してください。[接続操作](connection-operations.md)します。

 

 





