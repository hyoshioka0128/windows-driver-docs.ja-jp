---
title: VC の削除
description: VC の削除
ms.assetid: 6e49fb69-0b22-4f52-9b6d-661e818c1758
keywords:
- 仮想接続 WDK いる CoNDIS、削除します。
- 仮想接続を削除します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfd4ae02529c02b6d9b5b28a7e3db0a719695505
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381476"
---
# <a name="deleting-a-vc"></a>VC の削除





クライアントの接続指向、コール マネージャー、または仮想回線 (VC) の作成を開始した MCM ドライバーのみがその VC の削除を開始できます。 クライアントの発信呼び出しでは、コール マネージャーまたは MCM ドライバー以前に作成した削除 VC が、ネットワーク経由で着信呼び出しの作成以前 VC を削除したがってし、コール マネージャーのシグナルを交換する以前に作成した VC を削除します。ネットワーク経由のメッセージ。 (、MCM ドライバーではシグナリング メッセージを交換するために作成される VC を削除する NDIS を呼び出されません。 MCM ドライバーを削除します NDIS に対して非透過的である内部処理で、このような VC。)

接続指向のクライアントまたは呼び出しマネージャーと VC の削除を開始します。 [ **NdisCoDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscodeletevc)します。

次の図は、マネージャー、VC の削除を開始する呼び出しのクライアントを示します。

![vc の削除を開始するコール マネージャーのクライアントを示す図](images/cm-09.png)

次の図は、VC の削除を開始する MCM ドライバーのクライアントを示します。

![vc の削除を開始する、mcm ドライバーのクライアントを示す図](images/fig1-09.png)

次の図は、マネージャー、VC の削除を開始する呼び出しを示します。

![vc の削除を開始するコール マネージャーを示す図](images/cm-10.png)

クライアントまたは呼び出しのマネージャーを呼び出すと**NdisCoDeleteVc** 、MCM のドライバーを呼び出すときに、または**NdisMCmDeleteVc**必要がある未解決の呼び出しで指定された VC、VC をされている必要がありますは既に[非アクティブ化](deactivating-a-vc.md)します。 これらの要件を満たすためには、次の条件が満たされていることを意味します。

-   クライアントが既に呼び出されて[ **NdisClCloseCall** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclclosecall)で、指定された*NdisVcHandle*とその[close の呼び出しの要求](client-initiated-request-to-close-a-call.md)が完了正常にします。

-   コール マネージャーが既に呼び出されて[ **NdisCmDeactivateVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmdeactivatevc)または MCM ドライバーが既に呼び出されて[ **NdisMCmDeactivateVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmdeactivatevc)で、指定された*NdisVcHandle*非アクティブ化要求が正常に完了して (を参照してください[受信要求の呼び出しを閉じます](incoming-request-to-close-a-call.md))。

クライアントのまたはコール マネージャーの呼び出しを**NdisCoDeleteVc**により呼び出す両方、基になるミニポート ドライバーの NDIS [ **MiniportCoDeleteVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_delete_vc)関数と、 [ **ProtocolCoDeleteVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_co_delete_vc) 、呼び出し元を共有するクライアントまたは呼び出しのマネージャーの機能、 *NdisVcHandle* (上記の 3 つの図を参照してください)。

*MiniportCoDeleteVc* VC VC、として、ミニポート ドライバーのコンテキストに割り当てられたリソースを解放します。 *ProtocolCoDeleteVc*リリース クライアントまたは呼び出し manager 操作を実行し、追跡するために使用するすべてのリソースは、VC の状態します。 両方*MiniportCoDeleteVc*と*ProtocolCoDeleteVc* NDIS を返すことができない関数は同期\_状態\_保留します。

MCM にドライバーと VC の削除を開始する[ **NdisMCmDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmdeletevc)(次の図を参照してください)。

![vc の削除を開始する、mcm ドライバーを示す図 ](images/fig1-10.png)

MCM ドライバーの呼び出しを**NdisMCmDeleteVc** NDIS を呼び出すと、 [ **ProtocolCoDeleteVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_co_delete_vc) MCM ドライバーを共有しているクライアントの機能、 *NdisVcHandle*します。

ときに**NdisCoDeleteVc**または**NdisMCmDeleteVc**コントロールを返します、 *NdisVcHandle*が無効になっています。

 

 





