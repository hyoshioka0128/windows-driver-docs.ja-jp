---
title: マルチポイント呼び出しへのパーティーの追加
description: マルチポイント呼び出しへのパーティーの追加
ms.assetid: 2d6b8ebe-8028-46d0-91bd-7f95b0375cc4
keywords:
- パーティ WDK いる CoNDIS
- multipoint 呼び出し WDK いる CoNDIS
- multipoint 呼び出しへのパーティの追加
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 680a652a4a6538948dfce38eb495a887769a6547
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362913"
---
# <a name="adding-a-party-to-a-multipoint-call"></a>マルチポイント呼び出しへのパーティーの追加





クライアントを使用して通話を multipoint にパーティを追加する要求[ **NdisClAddParty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscladdparty)します。 クライアントは、既存の multipoint 呼び出し - つまり、呼び出しにのみ、パーティを追加できます、クライアントが指定したため、 *ProtocolPartyContext*に[ **NdisClMakeCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclmakecall)(を参照してください。[呼び出しを行う](making-a-call.md))。

次の図は、multipoint の呼び出しにパーティを追加する要求マネージャーの呼び出しのクライアントを示します。

![multipoint の呼び出しにパーティを追加する要求のコール マネージャーのクライアントを示す図](images/cm-17.png)

次の図は、multipoint の呼び出しにパーティを追加する要求、MCM ドライバーのクライアントを示します。

![multipoint の呼び出しにパーティを追加する要求、mcm ドライバーのクライアントを示す図](images/fig1-17.png)

呼び出す前に**NdisClAddParty**クライアントの割り当てし、パーティを追加するには、そのコンテキスト領域を初期化する必要があります。 クライアントのよくとして、このようなコンテキスト エリアにポインターを渡す、 *ProtocolPartyContext*としては、そのコンテキスト領域内の変数へのポインター、 *NdisPartyHandle*の呼び出し時にパラメーター **NdisClAddParty**します。

加え、 *NdisVcHandle*と*ProtocolPartyContext*、クライアントは呼び出しのパラメーターを渡します (をバッファー [ **CO\_呼び出す\_パラメーター** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545384(v=vs.85))構造) に**NdisClAddParty**します。 基になるネットワーク中は、クライアントが multipoint VC にパーティごとのトラフィック パラメーターを指定できるかどうかを判断します。

呼び出し**NdisClAddParty**によりこの要求を転送する NDIS、 [ **ProtocolCmAddParty** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cm_add_party)コール マネージャーまたはクライアントが共有する MCM ドライバーの機能は、指定された*NdisVcHandle*します。 NDIS 渡すには、次の*ProtocolCmAddParty*:

-   A *CallMgrVcContext*呼び出しの VC を示します。

-   CO へのポインター\_呼び出す\_パラメーター構造体をクライアントに渡す呼び出しのパラメーターを含む**NdisClAddParty**します。

-   *NdisPartyHandle*を追加するパーティを識別します。

*ProtocolCmAddParty*割り当て、呼び出しに追加されるパーティのために必要なすべての動的リソースを初期化します。 *ProtocolCmAddParty*、コール マネージャーまたは MCM ドライバー、multipoint の呼び出しに指定したパーティを追加する、必要に応じてネットワーク デバイスの制御、またはその他のメディア固有エージェントと通信します。

場合は、クライアントは、パラメーター multipoint VC、コール マネージャーまたは MCM のドライバーを既に確立されているものと一致しないことなどの呼び出しで渡されます。

-   基になるネットワーク中は、multipoint VCs でこの機能をサポートしている場合は、パーティごとのトラフィックのパラメーターを設定します。

-   VC を最初に確立されたものには、トラフィックのクライアントが指定したパラメーターをリセットします。

-   VC およびに現在接続されているすべてのパーティは、呼び出しのパラメーターを変更します。

-   パーティを追加するクライアントの試みは失敗します。

*ProtocolCmAddParty*で同期的に、多くの場合、非同期的に完了できる[ **NdisCmAddPartyComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmaddpartycomplete)の場合は、コール マネージャーまたは[ **NdisMCmAddPartyComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmaddpartycomplete)MCM、ドライバーの場合。 コール マネージャーまたは MCM ドライバーに同期的または非同期的に操作が完了したら、かどうかは、NDIS にバッファー内の呼び出しのパラメーターを渡します。

呼び出し**Ndis (M) CmAddPartyComplete**を呼び出すクライアントの NDIS と[ **ProtocolClAddPartyComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cl_add_party_complete)関数。 呼び出しのパラメーターを変更するには、コール マネージャーまたは MCM ドライバー信号のプロトコルを許可する場合、パーティを追加するクライアントの要求が成功した場合と*ProtocolClAddPartyComplete*呼び出しをテストする必要があります\_パラメーター\_バッファー内の CO で変更されたフラグ\_呼び出す\_パラメーター構造体の呼び出しのパラメーターが変更されたかどうかを判断します。 信号のプロトコルが、クライアントが実行できる内容を決定します CO への変更が見つかった場合は\_呼び出す\_許容できないパラメーターです。 通常、クライアントが呼び出す[ **NdisClDropParty** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscldropparty)ここで (を参照してください[Multipoint 呼び出しからパーティを削除する](dropping-a-party-from-a-multipoint-call.md))。

 

 





