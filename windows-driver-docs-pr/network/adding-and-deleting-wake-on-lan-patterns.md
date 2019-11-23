---
title: Wake On LAN パターンの追加と削除
description: Wake On LAN パターンの追加と削除
ms.assetid: 87e16ba6-0974-4921-b846-97d105e5dd30
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b3d7f8df00eb410bcf4f3b27e2eb5444cc38e7f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838243"
---
# <a name="adding-and-deleting-wake-on-lan-patterns"></a>Wake On LAN パターンの追加と削除





Wake on LAN (WOL) パターンを追加するために、NDIS プロトコルドライバーは oid\_PM の oid セット要求を発行し、 [\_WOL\_パターン\_追加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-add-wol-pattern)します。 [**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_PM\_WOL\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)構造へのポインターが含まれています。 ネットワークアダプターで WOL パケットがサポートされている場合は、プロトコルドライバーで WOL パケットを指定する必要があります。 ネットワークアダプターで WOL パケットがサポートされていない場合、プロトコルドライバーは WOL ビットマップ wake メソッドを使用する必要があります。

NDIS\_PM\_WOL\_パターンには、次の情報が含まれています。

<a href="" id="priority"></a>**的**  
WOL パターンの優先順位を格納します。 より多くの WOL パターンに使用できるリソースがない場合に、さらに優先順位の厳しい WOL パターンが追加されると、NDIS はリソースを解放するために低優先度の WOL パターンを削除する可能性があります。 ミニポートドライバーは、このメンバーを無視する必要があります。 プロトコルドライバーでは、NDIS\_PM\_WOL\_PRIORITY\_最低でも、NDIS\_PM\_WOL\_PRIORITY\_最高になるように、事前に定義された範囲内の任意の優先順位を指定できます。

<a href="" id="wolpackettype"></a>**WoLPacketType**  
WOL パケットの種類を指定する[**NDIS\_PM\_wol\_packet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_pm_wol_packet)列挙値が含まれています。

<a href="" id="friendlyname"></a>**フレンドリ**  
には、ユーザーが判読できる WOL パケットの説明を含む[**文字列構造\_\_カウントされる NDIS\_PM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_counted_string)が含まれています。

<a href="" id="patternid"></a>**PatternId**  
WOL パターンを識別する、NDIS によって提供される値が含まれています。 NDIS\_\_PM を送信する前に、基になる NDIS ドライバーに[\_WOL\_PATTERN](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-add-wol-pattern) oid 要求を追加するか、またはそれ以降のドライバーへの要求を完了するために、ndis はネットワークアダプターの WOL パターン間で一意の値に**PatternId**を設定します。

<a href="" id="nextwolpatternoffset"></a>**NextWoLPatternOffset**  
1つの[**ndis\_pm\_wol\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)構造の、OID [\_pm\_wol\_pattern\_list](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-wol-pattern-list) oid のリストに含まれる次の NDIS\_PM\_wol\_パターン構造に対するオフセット (oid 要求情報**バッファー**の先頭からのオフセット) を格納します。 OID\_PM\_WOL\_パターン\_リストの詳細については、「 [Wol パターンの現在の設定の取得](obtaining-the-current-settings-of-wol-patterns.md)」を参照してください。

<a href="" id="wolpattern"></a>**WoLPattern**  
共用体の**IPv4TcpSynParameters**、 **IPv6TcpSynParameters**、 **EapolRequestIdMessageParameters**、または**WoLBitMapPattern**構造体のいずれかが含まれています。

<a href="" id="ipv4tcpsynparameters"></a>**IPv4TcpSynParameters**  
IPv4 TCP 同期 (SYN) 情報が含まれています。

<a href="" id="ipv6tcpsynparameters"></a>**IPv6TcpSynParameters**  
IPv6 TCP SYN 情報が含まれています。

<a href="" id="eapolrequestidmessageparameters"></a>**EapolRequestIdMessageParameters**  
802.1 X EAP over LAN (EAPOL) 要求 id メッセージパラメーターを格納します。

<a href="" id="wolbitmappattern"></a>**WoLBitMapPattern**  
WOL ビットマップパターン仕様を含みます。

NDIS は、ネットワークアダプターに固有の識別子をすべての WOL パターンに割り当てます。 パターン識別子は、ネットワークアダプターに設定されているパターンごとに一意の値です。 ただし、パターン識別子は、すべてのネットワークアダプターでグローバルに一意ではありません。 Ndis は、NDIS が\_OID を送信するときに基になるネットワークアダプターに id を渡し、 [\_WOL\_PATTERN](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-add-wol-pattern) oid 要求をミニポートドライバーに追加\_ます。 WOL パターンが正常に追加されると、NDIS は WOL パターンを追加した前のドライバーに識別子を返します。 それまでのドライバーは識別子を使用して、以前に追加された WOL パターンを削除します。 パターン識別子は、WOL パターンがネットワークアダプターから削除されたときに、後続のドライバーの状態を示すためにも使用されます。

プロトコルドライバーは、oid\_PM の OID セット要求を発行し[\_\_WOL\_パターンを削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-remove-wol-pattern)して、ネットワークアダプターに追加したすべてのパターンを削除してから、そのネットワークアダプターへのバインドを閉じる必要があります。 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、パターン識別子へのポインターが含まれています。

ユーザーモードアプリケーションでは、GUID\_PM\_使用して\_WOL\_PATTERN WMI GUID を削除し、以前に追加された WOL パターンをネットワークアダプターから削除します。 NDIS は、この WMI 要求を oid\_PM の oid セット要求に変換し\_ネットワークアダプターの[\_WOL\_パターンを削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-remove-wol-pattern)します。 NDIS は、ネットワークアダプターを停止する前に、アプリケーションがネットワークアダプターから追加した WOL パターンをすべて削除します。

NDIS を使用すると、複数の NDIS プロトコルドライバーで同じネットワークアダプターに WOL パターンを追加できます。 要求された wol パターンの数がネットワークアダプターでサポートできるものよりも大きい場合に、WOL パターンの適切なセットが設定されていることを確認するために、プロトコルドライバーは、NDIS\_PM\_WOL\_パターン構造の**優先順位**メンバーで、要求された各 wol パターンに優先順位を割り当てます。 ネットワークアダプターにリソースが不足しているために、NDIS が新しい優先順位の WOL パターンを追加できない場合、NDIS は優先順位の低いパターン (存在する場合) のいずれかを削除し、優先順位の高いパターンをもう一度追加しようとします。

ミニポートドライバーが、パターンの追加要求を失敗させ、ndis\_PM\_WOL\_パターン\_リスト\_完全な状態コードを\_返すことによって、NDIS でパターンの優先順位を再設定できるように  する必要がある**ことに注意**してください。

 

NDIS が優先順位の低いパターンの1つを削除すると、そのドライバーは、削除されたパターンに[**ndis\_状態\_PM\_WOL\_パターン\_拒否**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wol-pattern-rejected)状態の表示を設定するように通知します。 [**NDIS\_ステータス\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)表示構造体の**statusbuffer**メンバーは、拒否された wol パターンの WOL パターン識別子の ULONG を含みます。 NDIS では、 [**ndis\_PM\_wol\_pattern**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)構造体の**PATTERNID**メンバーに wol パターン識別子が指定されています。

インフラストラクチャ要素を使用して、インフラストラクチャ内をローミングするときに、インフラストラクチャ要素を使用してパターンをオフロードするワイヤレスネットワークアダプターの場合、新しいインフラストラクチャ要素で同じ機能がサポートされていない可能性があります。\_また、適切な状態コードを使用して、 [ **\_PM\_WOL\_パターン\_拒否**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wol-pattern-rejected)された状態が示されます。

 

 





