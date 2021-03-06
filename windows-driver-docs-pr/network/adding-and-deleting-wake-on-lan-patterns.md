---
title: Wake On LAN パターンの追加と削除
description: Wake On LAN パターンの追加と削除
ms.assetid: 87e16ba6-0974-4921-b846-97d105e5dd30
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 888bade73f47d6fff88249915d06f739eb135526
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384738"
---
# <a name="adding-and-deleting-wake-on-lan-patterns"></a>Wake On LAN パターンの追加と削除





Wake on LAN (WOL) パターンを追加するには、NDIS プロトコル ドライバーがの OID セット要求を発行[OID\_PM\_追加\_WOL\_パターン](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-add-wol-pattern)します。 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体にはへのポインターが含まれています、 [ **NDIS\_PM\_WOL\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)構造体。 プロトコル ドライバーは、その WOL パケットがネットワーク アダプターでサポートされている場合、WOL パケットを指定する必要があります。 ネットワーク アダプターが、WOL パケットをサポートしていない場合、プロトコル ドライバーには、WOL ビットマップ ウェイク メソッドを使用する必要があります。

NDIS\_PM\_WOL\_パターンには、次の情報が含まれています。

<a href="" id="priority"></a>**優先順位**  
WOL パターンの優先度が含まれています。 上にある、ドライバーより多くの WOL パターンの使用可能なリソースがない場合より高い優先順位 WOL パターンを追加、NDIS リソースを解放する低優先度 WOL パターンが削除されます。 ミニポート ドライバーでは、このメンバーを無視する必要があります。 プロトコル ドライバーは、NDIS から定義済みの範囲内にある任意の優先順位を指定できます\_PM\_WOL\_優先度\_NDIS に最小\_PM\_WOL\_の優先順位\_最も高い。

<a href="" id="wolpackettype"></a>**WoLPacketType**  
含まれています、 [ **NDIS\_PM\_WOL\_パケット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ne-ntddndis-_ndis_pm_wol_packet) WOL パケットの種類を指定する列挙値。

<a href="" id="friendlyname"></a>**FriendlyName**  
含まれています、 [ **NDIS\_PM\_カウント済\_文字列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_counted_string) WOL パケットのユーザーが判読できる説明を含む構造体。

<a href="" id="patternid"></a>**PatternId**  
WOL パターンを識別する NDIS で提供される値が含まれています。 NDIS 送信する前に、 [OID\_PM\_追加\_WOL\_パターン](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-add-wol-pattern)OID NDIS ドライバーは、基になるまで要求または上にあるドライバーへの要求が完了すると、NDIS 設定**PatternId** WOL のパターンが、ネットワーク アダプター間で一意の値にします。

<a href="" id="nextwolpatternoffset"></a>**NextWoLPatternOffset**  
オフセットが含まれています (OID 要求の開始から**InformationBuffer**) のいずれかの[ **NDIS\_PM\_WOL\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)構造体を次の NDIS\_PM\_WOL\_パターンの構造体のリストで、 [OID\_PM\_WOL\_パターン\_ボックスの一覧](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-wol-pattern-list)OID。 OID の詳細については\_PM\_WOL\_パターン\_ ボックスの一覧を参照してください[WOL パターンの現在の設定を取得する](obtaining-the-current-settings-of-wol-patterns.md)します。

<a href="" id="wolpattern"></a>**WoLPattern**  
いずれかが含まれています、 **IPv4TcpSynParameters**、 **IPv6TcpSynParameters**、 **EapolRequestIdMessageParameters**、または**WoLBitMapPattern**共用体の構造体。

<a href="" id="ipv4tcpsynparameters"></a>**IPv4TcpSynParameters**  
IPv4 TCP が含まれています (SYN) 情報を同期します。

<a href="" id="ipv6tcpsynparameters"></a>**IPv6TcpSynParameters**  
IPv6 TCP SYN 情報が含まれています。

<a href="" id="eapolrequestidmessageparameters"></a>**EapolRequestIdMessageParameters**  
LAN (EAPOL) 要求の id のメッセージ パラメーターは、802.1 X EAP が含まれています。

<a href="" id="wolbitmappattern"></a>**WoLBitMapPattern**  
WOL ビットマップのパターンの仕様が含まれています。

NDIS は、すべて WOL パターンにネットワーク アダプターの一意の識別子を割り当てます。 パターン識別子は、ネットワーク アダプターに設定されているパターンのそれぞれに一意の値です。 ただし、パターン識別子はグローバルに一意なすべてのネットワーク アダプターです。 NDIS は、NDIS が送信すると、基になるネットワーク アダプターに識別子を渡します、 [OID\_PM\_追加\_WOL\_パターン](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-add-wol-pattern)ミニポート ドライバーに OID 要求。 WOL パターンの追加が成功した場合は、NDIS WOL パターンを追加するドライバーの上にある識別子を返します。 上位のドライバーでは、以前に追加された WOL パターンを削除するのに識別子を使用します。 パターン識別子は、WOL パターンがネットワーク アダプターから削除されたときにも上にあるドライバーに状態インジケーターに使用されます。

プロトコル ドライバーの OID のセット要求を発行する必要があります[OID\_PM\_削除\_WOL\_パターン](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-remove-wol-pattern)を閉じる前に、ネットワーク アダプターに追加パターンをすべて削除します。そのネットワーク アダプターにバインドします。 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造にはパターン識別子へのポインターが含まれています。

ユーザー モード アプリケーションは、GUID を使用して\_PM\_削除\_WOL\_ネットワーク アダプターから以前に追加された WOL パターンを削除する WMI GUID のパターン。 NDIS の OID のセット要求するには、この WMI 要求を変換する[OID\_PM\_削除\_WOL\_パターン](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-remove-wol-pattern)ネットワーク アダプター。 NDIS は、ネットワーク アダプターを停止する前に、ネットワーク アダプターからアプリケーションを追加する WOL パターンのすべてを削除します。

NDIS では、同じネットワーク アダプターに WOL パターンを追加する複数の NDIS プロトコル ドライバーを許可します。 WOL パターンの要求の数が、ネットワーク アダプターでサポートできるよりも高い WOL パターンの適切なセットが設定されていることを確認するには、プロトコルのドライバーで要求された各 WOL パターンに優先順位を割り当てる、**優先度**メンバーの NDIS\_PM\_WOL\_パターンの構造体。 NDIS は、ネットワーク アダプターは、リソース不足になるため、新規の優先度高 WOL パターンを追加できません、NDIS は低優先度のパターン (ある場合) のいずれかを削除し、優先度の高いパターンを再度追加しようとしています。

**注**  ミニポート ドライバーには、パターンが失敗する要求を追加して、状態を返す\_NDIS\_PM\_WOL\_パターン\_一覧\_に完全な状態コード優先順位を変更、パターンの NDIS を許可します。

 

上にあるドライバーを削除したパターンを設定する NDIS は、低い優先度のパターンのいずれかを削除した場合に通知する[ **NDIS\_状態\_PM\_WOL\_パターン\_REJECTED** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wol-pattern-rejected)状態を示す値。 **StatusBuffer**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)構造体には WOL パターン識別子の ULONG が含まれています、WOL パターンを拒否します。 NDIS WOL パターンの識別子を提供する、 **PatternId**のメンバー、 [ **NDIS\_PM\_WOL\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)構造体。

ワイヤレス ネットワーク アダプターのように、インフラストラクチャの間でローミングして、パターンの負荷を軽減するインフラストラクチャ要素を使用する、新しいインフラストラクチャ要素をサポートするいないと同じ機能と、ミニポート ドライバーを送信する、 [ **NDIS\_状態\_PM\_WOL\_パターン\_REJECTED** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wol-pattern-rejected)適切な状態コードでステータスを示す値。

 

 





