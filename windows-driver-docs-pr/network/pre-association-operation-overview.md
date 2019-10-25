---
title: 関連付け前の操作の概要
description: 関連付け前の操作の概要
ms.assetid: c33cf228-720f-4204-820c-0fb9a288bc6e
keywords:
- 事前関連付け操作 WDK ネイティブ 802.11 IHV 拡張 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e5b5e16c906ef21e769e2cc2db6cadf96b98b4b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843496"
---
# <a name="pre-association-operation-overview"></a>関連付け前の操作の概要




 

ユーザーが基本サービスセット (BSS) のネットワーク接続用のプロファイルを選択した後、オペレーティングシステムは[*Dot11ExtIhvPerformPreAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate)関数を呼び出して、関連付け前の操作を開始します。 この関数が呼び出されると、IHV 拡張 DLL は次のことを実行します。

-   IHV が定義した接続とセキュリティプロファイルの拡張機能を検証します。

    IHV 拡張 DLL によってプロファイルが正しくないと判断された場合は、Winerror.h で定義されている適切なエラーコードが返されます。 この場合、オペレーティングシステムは、ネットワークプロファイルを使用できないことをユーザーに通知します。

-   接続とセキュリティプロファイルに対する IHV 定義の拡張機能に基づいて、関連付け前の操作を開始します。

    関連付け前の操作が開始された後は、 [*Dot11ExtIhvPerformPreAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate)の呼び出しから非同期的に完了する必要があります。

IHV 拡張 DLL は、 [**Dot11ExtPreAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_pre_associate_completion)を呼び出すことによって、関連付け前の操作を完了します。 この呼び出しの後、オペレーティングシステムは、 [OID\_\_DOT11](https://docs.microsoft.com/windows-hardware/drivers/network/oid-dot11-connect-request)の set 要求を発行して接続操作を開始します。これにより、ネイティブ802.11 ミニポートドライバーに接続\_要求が発行され、WLAN アダプターが管理されます。

次の図は、関連付け前の操作中に必要な手順を示しています。

![関連付け前の操作中に必要な手順を示す図](images/ihv-ext-preassoc.png)

[*Dot11ExtIhvPerformPreAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate)が呼び出されると、オペレーティングシステムは、次のパラメーターを使用して、IHV によって定義された拡張機能を接続とセキュリティプロファイルに渡します。

<a href="" id="pihvprofileparams"></a>*pIhvProfileParams*  
このパラメーターには、 [**DOT11EXT\_IHV\_PROFILE\_PARAMS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihvtypes/ns-wlanihvtypes-_dot11ext_ihv_profile_params)構造体へのポインターが渡されます。これは、ネットワークプロファイルが適用される基本サービスセット (BSS) ネットワークの属性を指定します。 たとえば、 **DOT11EXT\_IHV\_PROFILE\_PARAMS**構造体は、BSS ネットワークのサービスセット識別子 (SSID) と種類を指定します。

<a href="" id="pihvconnprofile"></a>*pIhvConnProfile*  
このパラメーターには、接続プロファイルの設定を含む、 [**DOT11EXT\_IHV\_接続\_プロファイル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_ihv_connectivity_profile)構造へのポインターが渡されます。 オペレーティングシステムは、IHV によって定義された接続プロファイルにのみ拡張機能を渡し、ユーザーが選択します。

<a href="" id="pihvsecprofile"></a>*pIhvSecProfile*  
このパラメーターには、セキュリティプロファイルの設定を含む[**DOT11EXT\_IHV\_security\_profile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_ihv_security_profile)構造体へのポインターが渡されます。 オペレーティングシステムは、IHV によって定義されたセキュリティプロファイルにのみ拡張機能を渡し、ユーザーが選択します。

<a href="" id="pconnectablebssid"></a>*P/Tablebssid*  
このパラメーターには、 [**DOT11\_bss\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlclient/ns-wlclient-_dot11_bss_list)構造体へのポインターが渡されます。これには、DLL が実行する bss ネットワークのサービスセット識別子 (SSID) の1つ以上の802.11 ビーコンまたはプローブ応答フレームが含まれています。関連付け前の操作です。

関連付け前の操作を実行すると、IHV 拡張 DLL は次のことを実行できます。

-   [**Dot11ExtNicSpecificExtension**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_nic_specific_extension)関数を呼び出して、ネイティブ802.11 ミニポートドライバーへのネットワーク接続に関する独自の構成要求を発行します。

    IHV 拡張 DLL では、 *Pihvconnprofile*パラメーターと*Pihvconnprofile*パラメーターを使用して、ユーザーが選択した独自の接続設定を特定できます。

    IHV 拡張 DLL は、 *P/Tablebssid*パラメーターを使用して、BSS ネットワークの属性を決定し、それに応じて独自のネットワーク設定を構成できます。

-   BSS ネットワーク接続で使用する専用の認証アルゴリズムと暗号アルゴリズムを使用して WLAN アダプターを構成します。

    *PszXmlFragmentIhvSecurity*パラメーターを使用すると、IHV 拡張 DLL は、ユーザーが選択した独自のセキュリティアルゴリズムを特定できます。

    セキュリティアルゴリズムを設定するには、次の IHV 拡張関数を呼び出すことができます。

    -   [**Dot11ExtSetAuthAlgorithm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_auth_algorithm)
    -   [**Dot11ExtSetUnicastCipherAlgorithm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_unicast_cipher_algorithm)
    -   [**Dot11ExtSetMulticastCipherAlgorithm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_multicast_cipher_algorithm)
-   [**Dot11ExtSendUIRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_ui_request)関数を呼び出して、IHV UI Extensions DLL によって、ユーザーの資格情報などのセキュリティパラメーターの入力をユーザーに求めるように要求します。

-   [**Dot11ExtSetEtherTypeHandling**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling)関数を呼び出して、DLL が受信するセキュリティパケットの IEEE EtherTypes の一覧を登録します。 リストが登録されると、オペレーティングシステムは、EtherType が一覧内のエントリと一致するすべてのパケットに対して[*Dot11ExtIhvReceivePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_receive_packet) IHV ハンドラー関数を呼び出します。

    また、IHV Extensions DLL は、ペイロードの暗号化解除から除外される EtherTypes の一覧を指定することもできます。 EtherTypes の登録の詳細については、「 [IEEE EtherType の処理](ieee-ethertype-handling.md)」を参照してください。

-   [**Dot11ExtSetProfileCustomUserData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_profile_custom_user_data)関数を呼び出して、ユーザーと現在の BSS ネットワークプロファイルに固有のデータをレジストリに保存します。

-   [**Dot11ExtGetProfileCustomUserData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_get_profile_custom_user_data)関数を呼び出して、ユーザーと現在の BSS ネットワークプロファイルに固有のレジストリからデータを取得します。

IHV 拡張機能の詳細については、「[ネイティブ 802.11 Ihv 拡張関数](https://docs.microsoft.com/windows-hardware/drivers/network/native-802-11-ihv-extensibility-functions)」を参照してください。

BSS ネットワークでの接続操作の詳細については、「[接続操作](connection-operations.md)」を参照してください。

 

 





