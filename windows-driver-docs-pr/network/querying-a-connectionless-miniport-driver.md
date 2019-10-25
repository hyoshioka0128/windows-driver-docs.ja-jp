---
title: コネクションレス ミニポート ドライバーのクエリ
description: コネクションレス ミニポート ドライバーのクエリ
ms.assetid: a556d7ba-52ea-443b-994b-4c517e80ac55
keywords:
- コネクションレスドライバー WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f4a0e0fa2ff4479b8c1e19e4aed346f343a8b75
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844901"
---
# <a name="querying-a-connectionless-miniport-driver"></a>コネクションレス ミニポート ドライバーのクエリ





コネクションレスミニポートドライバーによって保持されている Oid を照会するために、バインドされたプロトコルは[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)を呼び出し、要求構造を[ **\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)渡します。この構造では、クエリ対象のオブジェクト (oid) を指定し、それがバッファーを指します。は、要求された情報をどの NDIS が最終的に書き込むかを指定します。

NDIS がミニポートドライバーに応答しない場合、 **NdisOidRequest**を呼び出すと、ndis はミニポートドライバーの[*Miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)関数を呼び出します。これにより、要求された情報が ndis に返されます。 *Miniportoidrequest*は、 [**NdisMOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)の呼び出しを使用して同期的または非同期的に完了できます。

また、NDIS では、ミニポートドライバーの*Miniportoidrequest*関数をそれ自体の代わりに呼び出すこともできます。たとえば、ミニポートドライバーの*MINIPORTINITIALIZEEX*関数から NDIS\_STATUS\_SUCCESS が返された後に、ミニポートに対してクエリを実行します。ドライバーの機能、状態、または統計情報。 次の図は、コネクションレスのミニポートドライバーを照会する方法を示しています。

![コネクションレスミニポートドライバーのクエリを示す図](images/fig5-2.png)

NDIS は、ミニポートドライバーに代わって多くの OID 要求に応答します。 ミニポートドライバーは、初期化中および状態の表示中に OID 値の多くを報告します。 属性で報告される OID 値の詳細については、「 [**NDIS\_ミニポート\_アダプター\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_attributes)、および関連する属性構造体」を参照してください。

\_MAC\_オプションの OID\_GEN で*Miniportoidrequest*を呼び出すと、ミニポートドライバーが実行するオプションの操作を指定するビットマスクを返す必要があります。 フラグのセットには、次のものが含まれます。

-   NDIS\_MAC\_オプション\_データをコピー\_先読み\_ます。 このフラグは、指定されたデータに何らかの方法でアクセスできることをプロトコルドライバーに示します。 ミニポートドライバーがオンボードの共有メモリからデータを示している場合、このフラグを設定することはできません。

-   NDIS\_MAC\_オプション\_\_ループバックはありません。 このフラグが設定されている場合、ミニポートドライバーは、同じコンピューター上の受信側に送られる*Miniportsendnetbufferlists (パケット)* に渡されるパケットをループバックしません。また、ミニポートドライバーが、ループバックを実行するために NDIS を想定します。 NDIS がパケットのループバックを実行する場合、パケットはミニポートドライバーに渡されません。 ミニポートドライバーは、NIC がハードウェアループバックをを実行しない限り、常にこのフラグを設定します。

-   NDIS\_MAC\_オプション\_\_シリアル化されます。 このフラグが設定されている場合、データの転送を含め、以前に受信したパケットが完全に処理されるまで、ミニポートドライバーは新たに受信したパケットを示しません。 [**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)を呼び出してパケットを示すものを除き、ほとんどのミニポートドライバーでは、このフラグを設定します。

ミニポートドライバーは、ndis の内部使用のために予約されている\_予約済みの NDIS\_MAC\_オプションのフラグを使用することはできません。

また、*ミニ Portoidrequest*もメディア固有の OID で照会され、NIC の現在のアドレスを特定します。 たとえば、種類が802.3 の NIC のミニポートドライバーに対して、OID\_802\_3\_現在の\_アドレスを使用してクエリが実行されます。

特定のメディアの種類のミニポートドライバーは、メディア固有の追加の Oid を受け取ります。 たとえば、NIC の種類が802.3 であるミニポートドライバーは、OID\_802.3\_最大\_リスト\_のサイズに照会されます。 詳細については、「 [General Objects](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff546510(v=vs.85))」を参照してください。

 

 





