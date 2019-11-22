---
title: VC の作成
description: VC の作成
ms.assetid: 29d7f2b3-0514-46f8-8b12-02275b404a2a
keywords:
- 仮想接続 WDK の作成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 607ad68529c45328a6c01456e83ee9794f3b07d8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835031"
---
# <a name="creating-a-vc"></a>VC の作成





発信呼び出しを行う前に、接続指向クライアントが仮想接続 (VC) の作成を開始します。 接続指向クライアントへの着信呼び出しを示す前に、呼び出しマネージャーまたは MCM ドライバーによって VC の作成が開始されます。 VC がセットアップされ、アクティブ化されると、VC でクライアントデータを送受信できるようになります。

また、呼び出しマネージャーまたは MCM ドライバーは、ネットワークスイッチなどのネットワークコンポーネントとの間でシグナリングメッセージが交換される VC の作成を開始することもできます。

### <a name="client-initiated-creation-of-a-vc"></a>クライアントによって開始される VC の作成

[**NdisClMakeCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclmakecall)を使用して[呼び出しを行う](making-a-call.md)前に、接続指向クライアントは[**NdisCoCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscocreatevc)を呼び出して VC の作成を開始します。

次の図は、VC の作成を開始する呼び出しマネージャーのクライアントを示しています。

![vc の作成を開始するコールマネージャーのクライアントを示す図](images/cm-05.png)

次の図は、VC の作成を開始する MCM ドライバーのクライアントを示しています。

![vc の作成を開始する mcm ドライバーのクライアントを示す図](images/fig1-05.png)

呼び出しマネージャーの接続指向クライアントが**NdisCoCreateVc**を呼び出すと、NDIS は同期操作として、呼び出しマネージャーの[**ProtocolCoCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_create_vc)関数と、基になるミニポートの[**MiniportCoCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_create_vc)関数を呼び出します。ドライバー (このトピックの最初の図を参照してください)。 NDIS は、VC を表す*NdisVcHandle*を*ProtocolCoCreateVc*と*MiniportCoCreateVc*の両方に渡します。 **NdisCoCreateVc**の呼び出しが成功した場合、NDIS は*NdisVcHandle*を**NdisCoCreateVc**に返します。

*ProtocolCoCreateVc*は、アクティブ化される VC に対して後続の操作を実行するために呼び出しマネージャーが必要とする動的リソースおよび構造体を割り当て、初期化します。 *MiniportCoCreateVc*は、ポートポートが VC に関する状態情報を維持するために必要なすべてのリソースを割り当て、初期化します。 *ProtocolCoCreateVc*と*MiniportCoCreateVc*はどちらも*NdisVcHandle*を格納します。

MCM ドライバーの接続指向クライアントでは、 **NdisCoCreateVc**を呼び出すと、NDIS によって mcm ドライバーの*ProtocolCoCreateVc*関数が呼び出されます (クライアントによって開始される VC (Mcm ドライバーが存在する) の作成に関する説明を参照)。 この場合、 *ProtocolCoCreateVc*は、必要なリソースの割り当てと初期化を VC に対して実行します。 MCM ドライバーはこのような機能を提供しないため、 *MiniportCoCreateVc*には呼び出し (internal またはそれ以外) はありません。

### <a name="call-manager-initiated-creation-of-a-vc"></a>呼び出しマネージャーによって開始される VC の作成

[**NdisCmDispatchIncomingCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchincomingcall)を使用して接続指向クライアントへの[着信呼び出しを示す](indicating-an-incoming-call.md)前に、呼び出しマネージャーが**NdisCoCreateVc**を呼び出して VC の作成を開始します (次の図を参照)。

![vc の作成を開始する呼び出しマネージャーを示す図](images/cm-06.png)

呼び出しマネージャーが[**NdisCoCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscocreatevc)を呼び出すと、NDIS は同期操作として、呼び出しを受信する SAP を登録した接続指向クライアントの[**ProtocolCoCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_create_vc)関数と、基になるミニポートの[**MiniportCoCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_create_vc)関数を呼び出します。 NDIS は、VC を表す*NdisVcHandle*を*ProtocolCoCreateVc*と*MiniportCoCreateVc*の両方に渡します。 **NdisCoCreateVc**の呼び出しが成功した場合、NDIS は*NdisVcHandle*を**NdisCoCreateVc**に返します。

### <a name="mcm-driver-initiated-creation-of-a-vc"></a>MCM ドライバーによって開始される VC の作成

[**NdisMCmDispatchIncomingCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdispatchincomingcall)を使用して接続指向クライアントへの[着信呼び出しを示す](indicating-an-incoming-call.md)前に、Mcm ドライバーは[**NdisMCmCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmcreatevc)を呼び出して VC の作成を開始します (次の図を参照)。

![vc の作成を開始する mcm ドライバーを示す図](images/fig1-06.png)

MCM ドライバーが**NdisMCmCreateVc**を呼び出すと、NDIS は**NdisMCmCreateVc**を返す前の同期操作として、呼び出しが行われている SAP を登録した接続指向クライアントの[**ProtocolCoCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_create_vc)関数を呼び出します。受け取ら. NDIS は、VC を表す*NdisVcHandle*を*ProtocolCoCreateVc*に渡します。 **NdisMCmCreateVc**の呼び出しが成功した場合、NDIS は*NdisVcHandle*を**NdisMCmCreateVc**に返します。

*ProtocolCoCreateVc*は、クライアントが VC に対して後続の操作を実行するために必要とする動的なリソースと構造体を割り当て、初期化します。 *ProtocolCoCreateVc*も*NdisVcHandle*を格納します。

MCM ドライバーによってネットワークコンポーネントとのシグナリングメッセージを交換するための VC が作成された場合、VC を作成するために**Ndis * Xxx*** の呼び出しは使用されないことに注意してください。 実際、MCM ドライバーでは、 **Ndis * Xxx*** の呼び出しを使用して、このような VCs の作成、アクティブ化、非アクティブ化、削除を行うことはありません。 代わりに、MCM ドライバーは内部でこれらの操作を実行します。 そのため、このような VCs は NDIS に対して非透過的です。

 

 





