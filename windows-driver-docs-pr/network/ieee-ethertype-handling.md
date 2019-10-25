---
title: IEEE EtherType 処理
description: IEEE EtherType 処理
ms.assetid: ddd7244b-05a0-4ee8-b9aa-300015fbe3bd
keywords:
- 送信操作 WDK ネイティブ 802.11 IHV 拡張 DLL
- 受信操作 WDK ネイティブ 802.11 IHV 拡張 DLL
- IEEE EtherType が WDK ネイティブ 802.11 IHV 拡張 DLL を処理する
- EtherType の WDK ネイティブ 802.11 IHV 拡張 DLL の処理
- プライバシーに関する例外 WDK ネイティブ 802.11 IHV Extensions DLL
- 暗号化解除 WDK ネイティブ 802.11 IHV 拡張 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c6da1de936ce6e6b25235b451fa2b001c5538a9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823814"
---
# <a name="ieee-ethertype-handling"></a>IEEE EtherType 処理




 

IHV 拡張 DLL では、ワイヤレス LAN (WLAN) アダプターによって受信されたパケットを特別に処理するための IEEE EtherTypes の一覧を指定できます。 次の種類の EtherType 処理を指定できます。

<a href="" id="privacy-exemptions"></a>**プライバシーの除外**  
IHV 拡張 DLL では、受信パケットのパケット暗号化解除の除外を指定できます。 たとえば、DLL は、指定された EtherType を持つパケットを、その WLAN アダプターで一致する暗号キーが構成されている場合でも、暗号化されていないものとして受信できることを指定できます。

<a href="" id="ethertype-registration"></a>**EtherType の登録**  
IHV Extensions DLL は、処理して使用する EtherTypes を登録できます。 オペレーティングシステムは、 [*Dot11ExtIhvReceivePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_receive_packet)関数の呼び出しによって、登録された EtherType と一致するパケットを DLL に転送します。

IHV 拡張 DLL では、 [**Dot11ExtSetEtherTypeHandling**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling)関数の呼び出しによって、EtherType 処理が指定されています。 この関数を呼び出す場合、IHV 拡張 DLL は次のガイドラインに従う必要があります。

-   IHV Extensions DLL は、事前関連付け操作を完了する前に、いつでも[**Dot11ExtSetEtherTypeHandling**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling)を呼び出すことができます。 この操作の詳細については、「[事前関連付け操作](pre-association-operations.md)」を参照してください。

-   IHV 拡張 DLL は、0個以上の[**DOT11\_プライバシー\_の除外**](https://docs.microsoft.com/windows-hardware/drivers/ddi/windot11/ns-windot11-dot11_privacy_exemption)構造の配列を通じて、プライバシーの除外の一覧を指定します。 IHV 拡張 DLL が[**Dot11ExtSetEtherTypeHandling**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling)を呼び出さない場合、オペレーティングシステムは、アクセスポイント (AP) との802.11 の関連付けについて、既定でプライバシー除外リストになります。
    **注**  Windows Vista では、IHV 拡張 DLL は、インフラストラクチャの基本サービスセット (BSS) ネットワークのみをサポートしています。

     

-   IHV Extensions DLL は、受け取った0個以上の EtherTypes のリストを登録します。 通常、DLL は、関連付け後の操作中に処理するセキュリティパケットの EtherTypes を登録します。 この操作の詳細については、「[関連付け後の操作](post-association-operations.md)」を参照してください。

    IHV 拡張 DLL が[**Dot11ExtSetEtherTypeHandling**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling)を呼び出さない場合、オペレーティングシステムは既定では、任意の802.11 の AP との関連付けについて、登録済みの EtherTypes の空の一覧になります。

-   [**Dot11ExtPreAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_pre_associate_completion)を呼び出して、IHV 拡張 DLL が事前関連付け操作を完了した後、 [**Dot11ExtSetEtherTypeHandling**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling)の呼び出しで指定されたプライバシーの除外と EtherType の登録の一覧は、基本サービスセット (BSS) ネットワークに接続している間に、WLAN アダプターによって行われたすべての802.11 アソシエーションに適用されます。

-   オペレーティングシステムは、 [*Dot11ExtIhvAdapterReset*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_adapter_reset)を呼び出す前に、プライバシーの除外と EtherType の登録の一覧をクリアします。

 

 





