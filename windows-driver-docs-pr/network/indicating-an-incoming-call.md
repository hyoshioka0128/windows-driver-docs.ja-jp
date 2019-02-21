---
title: 着信呼び出しを示す
description: 着信呼び出しを示す
ms.assetid: ca7f4a1f-47a2-4ac0-b4a2-d0367163135f
keywords:
- WDK いる CoNDIS 通話のセットアップ
- 着信呼び出し WDK いる CoNDIS
- WDK いる CoNDIS の着信呼び出しを示す
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2576b6cbe67185f5e224526094acf25330c55eeb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535802"
---
# <a name="indicating-an-incoming-call"></a>着信呼び出しを示す





ネットワークからメッセージを通知することによってを着信呼び出しがコール マネージャーまたは MCM のドライバーを知らせます。 シグナリング メッセージから、コール マネージャーまたは MCM ドライバーは、着信呼び出しが対応する SAP を含む、呼び出しの呼び出しのパラメーターを抽出します。

次の図は、着信呼び出しを示す、MCM ドライバーを示します。

![着信呼び出しを示すコール マネージャーを示す図](images/cm-13.png)

次の図は、着信呼び出しを示す manager の呼び出しを示します。

![mcm ドライバーを通じて着信呼び出しを示す](images/fig1-13.png)

着信呼び出しのパラメーターが、コール マネージャーまたは MCM ドライバーに許容される場合は、シグナリング プロトコルによって自動的にネゴシエーションが許可されている場合は、リモート側でこれらのパラメーターの変更をネゴシエートする試行できます。 または、着信通話の先となるクライアントは、コール マネージャーまたは MCM ドライバーからの呼び出しを示す値を受信した後、呼び出しのパラメーターをネゴシエートする試行でした (を参照してください[Client-Initiated 要求の変更を呼び出すパラメーター](client-initiated-request-to-change-call-parameters.md)). リモート パーティによる呼び出しの許容される呼び出しのパラメーターをネゴシエートできないのは、コール マネージャーまたは MCM ドライバー場合、呼び出しを拒否する可能性があります。 このような場合で何ができます、シグナリングのプロトコルを決定します。

クライアントに着信呼び出しを示す、する前に、コール マネージャーまたは MCM ドライバーは、呼び出しの先となる SAP を確認する必要があります。 SAP は以前にされている必要があります[登録](registering-a-sap.md)クライアント。 コール マネージャーまたは MCM のドライバーを開始する必要がありますも、 [VC の作成](creating-a-vc.md)を開始し、[この VC のアクティブ化](activating-a-vc.md)します。

コール マネージャーまたは MCM ドライバーは、着信通話の先となる SAP に登録されているクライアントへの着信通話を示します。 コール マネージャーの着信呼び出しを示す[ **NdisCmDispatchIncomingCall**](https://msdn.microsoft.com/library/windows/hardware/ff561664)します。 着信呼び出しを示します、MCM ドライバー [ **NdisMCmDispatchIncomingCall**](https://msdn.microsoft.com/library/windows/hardware/ff562830)します。

呼び出しで**Ndis (M) CmDispatchIncomingCall**、コール マネージャーまたは MCM ドライバーは、次を渡します。

-   *NdisSapHandle*着信呼び出しが対応する SAP を識別します。

-   *NdisVcHandle*着信通話の仮想回線を識別します。

-   型の構造体へのポインター [ **CO\_呼び出す\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff545384)呼び出しの呼び出しのパラメーターを含むです。

呼び出し**Ndis (M) CmDispatchIncomingCall**を呼び出すクライアントの NDIS と[ **ProtocolClIncomingCall** ](https://msdn.microsoft.com/library/windows/hardware/ff570228)をクライアントを受け入れるか拒否している関数要求された接続。 *ProtocolClIncomingCall* SAP、VC を検証し、パラメーターを呼び出す必要があります。

*ProtocolClIncomingCall*同期的に完了できるか、NDIS を返すことができます\_状態\_に非同期で完了し、保留中の[ **NdisClIncomingCallComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff561632). 呼び出し**NdisClIncomingCallComplete**と呼び出しを上司に NDIS または MCM ドライバーの[ **ProtocolCmIncomingCallComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff570245)関数。

NDIS\_の同期の完了によって返されるステータス コード*ProtocolClIncomingCall*またはに指定された**NdisClIncomingCallComplete**クライアントの承認をことを示しますまたは。着信通話の拒否します。 クライアントがバッファー内の CO でも、呼び出しの呼び出しのパラメーターを返します\_呼び出す\_パラメーター構造体。 呼び出しのパラメーターの許容が見つかると、クライアント、信号のプロトコルで許可されている場合変更を要求できる関数のパラメーターに設定して、**フラグ**CO でメンバー\_呼び出す\_パラメーター構造体の呼び出しで\_パラメーター\_CHANGED、改訂版を提供することによってバッファー内の CO でパラメーターを呼び出すと\_呼び出す\_パラメーター構造体。

クライアントは、コール マネージャー、着信呼び出しを受け入れるか、MCM のドライバーを送信する必要がありますがある場合は、呼び出し元のエンティティに呼び出しが受け入れられたことを示すメッセージ シグナル通知します。 コール マネージャーまたは MCM のドライバーを送信する必要がありますそれ以外の場合、呼び出しが拒否されたことを示すメッセージを通知します。 場合は、クライアントは、呼び出しのパラメーター、コール マネージャーまたは MCM ドライバーの送信信号呼び出しのパラメーターの変更を要求するメッセージの変更を要求しています。

クライアントが、通話を承諾したかコール マネージャーが呼び出す関数のパラメーターに変更がリモート側によって受け付け、クライアントが要求の場合[ **NdisCmDispatchCallConnected**](https://msdn.microsoft.com/library/windows/hardware/ff561661)、し、MCM ドライバーを呼び出します[**NdisMCmDispatchCallConnected**](https://msdn.microsoft.com/library/windows/hardware/ff562826)します。 呼び出し**Ndis (M) CmDispatchCallConnected**を呼び出すクライアントの NDIS と*ProtocolClCallConnected*関数。

コール マネージャーまたは MCM のドライバーを呼び出すの呼び出しと呼び出し manager クライアントが拒否された、または着信通話の VC を MCM のドライバーが既にアクティブ化、 **Ndis (M) CmDeactivateVc** VC がアクティブの場合は、VC を非アクティブ化します。 コール マネージャーまたは MCM のドライバーを開始し、 [VC の削除](deleting-a-vc.md)呼び出して[ **NdisCoDeleteVc** ](https://msdn.microsoft.com/library/windows/hardware/ff561698)コール マネージャーの場合、または[ **NdisMCmDeleteVc** ](https://msdn.microsoft.com/library/windows/hardware/ff562819) MCM ドライバーの場合。

コール マネージャーまたは MCM のドライバーが呼び出していませんが、クライアントが通話を承諾した場合は、エンド ツー エンド接続が正常に確立されません (ため、たとえば、リモート パーティは、呼び出しをどれ) **Ndis (M) CmDispatchCallConnected**. 代わりに、呼び出すことが、 **Ndis (M) CmDispatchIncomingCloseCall**、それが原因でを呼び出すクライアントの NDIS *ProtocolClIncomingCloseCall*関数。 クライアントが呼び出す必要がありますし、 [ **NdisClCloseCall** ](https://msdn.microsoft.com/library/windows/hardware/ff561627)呼び出しの終了処理を完了します。 コール マネージャーまたは MCM のドライバーを呼び出して**Ndis (M) CmDeactivateVC**に[VC を非アクティブ化](deactivating-a-vc.md)着信呼び出し用に作成します。 コール マネージャーまたは MCM のドライバーを開始し、 [VC の削除](deleting-a-vc.md)呼び出して[ **NdisCoDeleteVc** ](https://msdn.microsoft.com/library/windows/hardware/ff561698)コール マネージャーの場合、または[ **NdisMCmDeleteVc** ](https://msdn.microsoft.com/library/windows/hardware/ff562819) MCM ドライバーの場合。

 

 





