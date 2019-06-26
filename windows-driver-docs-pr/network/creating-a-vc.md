---
title: VC の作成
description: VC の作成
ms.assetid: 29d7f2b3-0514-46f8-8b12-02275b404a2a
keywords:
- 仮想接続 WDK いる CoNDIS、作成します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1db840bf352b9fedc60d407ca29ccf37488b90b2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374942"
---
# <a name="creating-a-vc"></a>VC の作成





発信通話を行う前に、接続指向のクライアントは仮想の接続 (VC) に作成を開始します。 接続指向のクライアントに着信する前に、コール マネージャーまたは MCM ドライバー VC の作成を開始します。 VC をセットアップしてアクティブにした後は、クライアント データを送信または VC で受信されます。

コール マネージャーまたは MCM ドライバーでは、ネットワーク スイッチなどのネットワーク コンポーネントとのシグナリング メッセージの交換を VC の作成を開始することできますも。

### <a name="client-initiated-creation-of-a-vc"></a>VC のクライアントが開始した作成

前に[呼び出しを行う](making-a-call.md)で[ **NdisClMakeCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclmakecall)、接続指向のクライアントが呼び出す[ **NdisCoCreateVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscocreatevc) VC の作成を開始します。

次の図は、マネージャー、VC の作成を開始する呼び出しのクライアントを示します。

![vc の作成を開始するコール マネージャーのクライアントを示す図](images/cm-05.png)

次の図は、VC の作成を開始する MCM ドライバーのクライアントを示します。

![vc の作成を開始する、mcm ドライバーのクライアントを示す図](images/fig1-05.png)

コール マネージャーの接続指向のクライアントを呼び出すと**NdisCoCreateVc**、NDIS 呼び出しを同期操作として、 [ **ProtocolCoCreateVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_co_create_vc)関数の呼び出しマネージャーと[ **MiniportCoCreateVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_create_vc)基になるミニポート ドライバーの機能 (このトピックでは、最初の図を参照してください)。 NDIS 渡します、 *NdisVcHandle*両方に VC を表す*ProtocolCoCreateVc*と*MiniportCoCreateVc*します。 場合に呼び出し**NdisCoCreateVc**が成功すると、NDIS を返します、 *NdisVcHandle*に**NdisCoCreateVc**します。

*ProtocolCoCreateVc*割り当て、コール マネージャーがアクティブになる VC の後続の処理を実行する必要があります構造、動的リソースを初期化します。 *MiniportCoCreateVc*割り当て、VC に関する状態情報を維持するために、ミニポート ドライバーを必要とするすべてのリソースを初期化します。 両方*ProtocolCoCreateVc*と*MiniportCoCreateVc*格納、 *NdisVcHandle*します。

ときに、MCM のドライバーへの呼び出しのクライアントが接続指向**NdisCoCreateVc**を呼び出す、MCM ドライバーの NDIS と*ProtocolCoCreateVc*関数 (VC (MCM ドライバーの Client-Initiated 作成を参照してください。Present))。 この場合、 *ProtocolCoCreateVc* VC のために必要な割り当てとリソースの初期化を実行します。 呼び出し (内部またはそれ以外の場合) がない*MiniportCoCreateVc*MCM ドライバーはそのような関数を指定しないためです。

### <a name="call-manager-initiated-creation-of-a-vc"></a>VC の作成を管理者が開始した呼び出し

前に[着信呼び出しを示す](indicating-an-incoming-call.md)接続指向でクライアントに[ **NdisCmDispatchIncomingCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmdispatchincomingcall)、コール マネージャーを呼び出す**NdisCoCreateVc** VC の作成を開始する (次の図を参照してください)。

![vc の作成を開始するコール マネージャーを示す図](images/cm-06.png)

コール マネージャーを呼び出すと[ **NdisCoCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscocreatevc)、NDIS 呼び出しを同期操作として、 [ **ProtocolCoCreateVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_co_create_vc)の関数、接続指向のクライアントを呼び出しが受信されない、SAP に登録されているだけでなく[ **MiniportCoCreateVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_create_vc)の基になるミニポート関数。 NDIS 渡します、 *NdisVcHandle*両方に VC を表す*ProtocolCoCreateVc*と*MiniportCoCreateVc*します。 場合に呼び出し**NdisCoCreateVc**が成功すると、NDIS を返します、 *NdisVcHandle*に**NdisCoCreateVc**します。

### <a name="mcm-driver-initiated-creation-of-a-vc"></a>VC の MCM のドライバーが開始した作成

前に[着信呼び出しを示す](indicating-an-incoming-call.md)接続指向でクライアントに[ **NdisMCmDispatchIncomingCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmdispatchincomingcall)、MCM、ドライバーは呼び出し[ **NdisMCmCreateVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmcreatevc) VC の作成を開始する (次の図を参照してください)。

![vc の作成を開始する、mcm ドライバーを示す図](images/fig1-06.png)

MCM にドライバーを呼び出すと**NdisMCmCreateVc**、NDIS 呼び出しの前に、同期操作として、 **NdisMCmCreateVc**から制御が戻る、 [ **ProtocolCoCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_co_create_vc)登録呼び出しが受信されない SAP 接続指向のクライアントの関数。 NDIS 渡します、 *NdisVcHandle* VC を表す*ProtocolCoCreateVc*します。 場合に呼び出し**NdisMCmCreateVc**が成功すると、NDIS を返します、 *NdisVcHandle*に**NdisMCmCreateVc**します。

*ProtocolCoCreateVc*割り当て、任意の動的リソースと VC の後続の処理を実行するクライアントを必要とする構造体を初期化します。 *ProtocolCoCreateVc*も格納、 *NdisVcHandle*します。

MCM ドライバーでは、ネットワーク コンポーネントとのシグナリング メッセージを交換するため、VC を作成するときに使用しないことに注意してください。 **Ndis * Xxx*** VC を作成するため呼び出し。 実際には、MCM、ドライバーは使いません**Ndis * Xxx*** を作成する呼び出しは、アクティブ化、非アクティブ化、または、このような VCs を削除します。 代わりに、MCM、ドライバーはこれらの操作を内部的に実行します。 このような VCs は NDIS に対して非透過的ではそのためです。

 

 





