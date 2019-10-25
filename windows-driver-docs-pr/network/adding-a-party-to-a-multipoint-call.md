---
title: マルチポイント呼び出しへのパーティーの追加
description: マルチポイント呼び出しへのパーティーの追加
ms.assetid: 2d6b8ebe-8028-46d0-91bd-7f95b0375cc4
keywords:
- パーティ WDK
- マルチポイント呼び出し WDK CoNDIS
- multipoint 呼び出しへのパーティの追加
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a11818e7a81ad772ae78ffe392e258bdb63e90f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838249"
---
# <a name="adding-a-party-to-a-multipoint-call"></a>マルチポイント呼び出しへのパーティーの追加





クライアントは、 [**NdisClAddParty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscladdparty)を使用して、multipoint 呼び出しにパーティを追加するように要求します。 クライアントは、既存の multipoint 呼び出しにのみパーティを追加できます。つまり、クライアントが*Protocolpartycontext*を指定して[**NdisClMakeCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclmakecall)に渡す呼び出し (「[呼び出しを行う](making-a-call.md)」を参照してください)。

次の図は、multipoint 呼び出しにパーティを追加することを要求する呼び出しマネージャーのクライアントを示しています。

![multipoint 呼び出しにパーティを追加するよう要求している呼び出しマネージャーのクライアントを示す図](images/cm-17.png)

次の図は、multipoint 呼び出しにパーティを追加するように要求している MCM ドライバーのクライアントを示しています。

![multipoint 呼び出しにパーティを追加するように要求している mcm ドライバーのクライアントを示す図](images/fig1-17.png)

**NdisClAddParty**を呼び出す前に、クライアントは、追加するパーティのコンテキスト領域を割り当てて初期化する必要があります。 クライアントは、通常、このようなコンテキスト領域へのポインターを*Protocolpartycontext*として渡し、 **NdisClAddParty**を呼び出すと、そのコンテキスト領域内の変数へのポインターを*ndispartyhandle*パラメーターとして渡します。

クライアントは、 *NdisVcHandle*と*protocolpartycontext*に加えて、呼び出しパラメーター (バッファーされた[**CO\_呼び出し\_Parameters**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545384(v=vs.85))構造体) を**NdisClAddParty**に渡します。 基になるネットワークメディアは、クライアントが multipoint VC でパーティごとのトラフィックパラメーターを指定できるかどうかを判断します。

**NdisClAddParty**を呼び出すと、NDIS は、指定された*NdisVcHandle*をクライアントが共有する call manager または Mcm ドライバーの[**protocolcmaddparty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_add_party)関数にこの要求を転送します。 NDIS は、次のものを*Protocolcmaddparty*に渡します。

-   呼び出しの VC を示す*CallMgrVcContext* 。

-   クライアントが**NdisClAddParty**に渡す呼び出しパラメーターを格納している\_パラメーター構造体への CO\_呼び出しへのポインター。

-   追加するパーティを識別する*Ndispartyhandle* 。

*Protocolcmaddparty*は、呼び出しに追加するパーティに必要な動的リソースを割り当て、初期化します。 *Protocolcmaddparty*から、呼び出しマネージャーまたは mcm ドライバーは、必要に応じてネットワークコントロールデバイスやその他のメディア固有のエージェントと通信し、指定されたパーティを multipoint 呼び出しに追加します。

クライアントが、multipoint VC に対して既に確立されているパラメーターと一致しない呼び出しパラメーターを渡した場合、呼び出しマネージャーまたは MCM ドライバーは次のようになります。

-   基になるネットワークメディアが multipoint VCs でこの機能をサポートしている場合は、パーティ間のトラフィックパラメーターを設定します。

-   クライアントから提供されたトラフィックパラメーターを、VC 用に最初に確立されたものにリセットします。

-   VC と、現在接続されているすべてのパーティの呼び出しパラメーターを変更します。

-   クライアントがパーティを追加しようとして失敗します。

*Protocolcmaddparty*は、mcm ドライバーの場合、呼び出しマネージャーまたは[**NdisMCmAddPartyComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmaddpartycomplete)の場合、同期的に、または[**NdisCmAddPartyComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmaddpartycomplete)を使用して非同期的に完了できます。 呼び出しマネージャーまたは MCM ドライバーが操作を同期的または非同期的に完了するかどうかは、バッファーされた呼び出しパラメーターを NDIS に渡します。

**Ndis (M) CmAddPartyComplete**を呼び出すと、ndis によってクライアントの[**Protocolcladdpartycomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_add_party_complete)関数が呼び出されます。 クライアントによるパーティの追加要求が成功し、シグナリングプロトコルで呼び出しパラメーターを変更することが許可されている場合は、 *Protocolcladdpartycomplete*は、\_\_パラメーターの呼び出しをテストする必要があります。バッファーされた CO\_呼び出しパラメーターが変更されたかどうかを判断するために\_PARAMETERS 構造体を呼び出します。 シグナリングプロトコルは、\_パラメーターを使用できないようにするために、クライアントが変更を検出したとき\_にクライアントが実行できる処理を決定します。 通常、クライアントはこの場合、 [**NdisClDropParty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscldropparty)を呼び出します (「 [Multipoint 呼び出しからのパーティの削除](dropping-a-party-from-a-multipoint-call.md)」を参照してください)。

 

 





