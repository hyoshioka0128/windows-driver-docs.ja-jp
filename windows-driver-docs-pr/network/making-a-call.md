---
title: 呼び出しの実行
description: 呼び出しの実行
ms.assetid: b5273df1-b99f-415c-a099-16a51f3329ee
keywords:
- WDK いる CoNDIS 通話のセットアップ
- WDK いる CoNDIS 呼び出しを行う
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 394a69a9582a2c272d167401e9b2059f2690baf0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356183"
---
# <a name="making-a-call"></a>呼び出しの実行





次の図は、manager を呼び出すことによって、発信通話を行うクライアントを示します。

![マネージャーを呼び出すことによって、発信通話を行うクライアントを示す図](images/cm-11.png)

次の図は、MCM ドライバーを通じて発信呼び出しを行うクライアントを示します。

![mcm ドライバーを通じて発信呼び出しを行うクライアントを示す図](images/fig1-11.png)

発信通話を行う前に、接続指向のクライアントが必要です。

-   初期化呼び出しのパラメーター型の構造体で[ **CO\_呼び出す\_パラメーター**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545384(v=vs.85))します。 コール マネージャーまたは MCM ドライバー呼び出しパラメーターを使用して通常の呼び出しを設定して、ミニポート ドライバーで使用するメディア パラメーターを派生する、クライアントを指定します。

-   開始、 [VC の作成](creating-a-vc.md)で[ **NdisCoCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscocreatevc)します。

戻り値に、成功**NdisCoCreateVc**、クライアント呼び出し[ **NdisClMakeCall** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclmakecall)呼び出しを開始する (このセクションでは 2 つの図を参照してください)。

呼び出しで**NdisClMakeCall**、クライアントが、CO へのポインターを渡します\_呼び出す\_パラメーター構造体の前に初期化します。 クライアントにも渡す、 *NdisVcHandle* (によって返される**NdisCoCreateVc**) の呼び出しをクライアントが (送受信など) のデータの VC を識別します。 渡す場合は、クライアントは、通話 multipoint (1 つ以上のリモート側の呼び出し) を*ProtocolPartyContext*クライアントのパーティごとの管理、常駐のコンテキストをクライアントに割り当てられた領域を識別するハンドルを指定します。multipoint VC の初期のパーティの状態です。

呼び出し**NdisClMakeCall**によりこの要求を転送する NDIS、 [ **ProtocolCmMakeCall** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cm_make_call)コール マネージャーまたはクライアントが共有する MCM ドライバーの機能は、指定された*NdisVcHandle*します。 *ProtocolCmMakeCall*クライアントによって設定された入力の呼び出しのパラメーターを検証する必要があります。

*ProtocolCmMakeCall*ネットワーク接続を確立するデバイスの制御 (シグナリング メッセージの交換) と通信します。 コール マネージャーを呼び出す[ **NdisCoSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscosendnetbufferlists)このような交換を開始する (を参照してください[送信 NET\_いる CoNDIS ドライバーからのバッファーの構造体](sending-net-buffer-structures-from-condis-drivers.md))。 MCM にドライバーが呼び出すことはありません**NdisCoSendNetBufferLists**します。 代わりに、ネットワーク経由で直接データを送信します。

関連するネットワーク コンポーネントとネゴシエートするときにクライアントが指定した呼び出しのパラメーターを変更することができ、クライアントが最初に指定したよりも、さまざまなトラフィックのパラメーターを返すことができます、コール マネージャーまたは MCM ドライバー **NdisClMakeCall**(を参照[呼び出しのパラメーターを変更する着信要求](incoming-request-to-change-call-parameters.md))。

明示的な*NdisPartyHandle*に渡される*ProtocolCmMakeCall* multipoint 呼び出しのクライアントによって作成された VC を使用することを示します。 コール マネージャーまたは MCM ドライバーを割り当てるし、パーティごとの状態情報を保持および multipoint の呼び出しを制御するために必要なために必要なリソースを初期化する必要があります。

呼び出す必要がありますが、コール マネージャーはその中に必要なネットワーク、ハードウェアと必要なすべての通信を完了したら、 [ **NdisCmActivateVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmactivatevc)を開始する、 [VC のアクティブ化](activating-a-vc.md)データの送信し、受信などの呼び出しで。 呼び出す必要があります、MCM ドライバー [ **NdisMCmActivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmactivatevc)します。

コール マネージャーは、基になるミニポート ドライバーの VC (、VC がされてアクティブになっている) でデータを転送する準備ができたら[ **NdisCmMakeCallComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmmakecallcomplete)、し、MCM ドライバー呼び出して[ **NdisMCmMakeCallComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmmakecallcomplete)します。 この時点では、コール マネージャーまたは MCM ドライバーは、VC の呼び出しのパラメーターを確立するために、ネットワークとネゴシエートする必要がありますが、基になるミニポート ドライバーに VC のライセンス認証を完了する必要があります。

呼び出しで**Ndis (M) CmMakeCallComplete**、コール マネージャーまたは MCM ドライバー呼び出しにパラメーターを渡します VC のポインターとして共同の種類の構造体\_呼び出す\_パラメーター。 呼び出しを設定して、クライアントを通知できますコール マネージャーが、クライアントによって指定された最初の呼び出しパラメーターを変更する場合\_パラメーター\_CO で変更されたフラグ\_呼び出す\_パラメーター構造体。

呼び出し**Ndis (M) CmMakeCallComplete** NDIS を呼び出すと、 [ **ProtocolClMakeCallComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cl_make_call_complete)発信通話を開始したクライアントの関数。 呼び出し*ProtocolClMakeCallComplete*コール マネージャーの仮想の接続を確立するために、クライアントの要求の処理が完了したことを示します**NdisClMakeCall**します。

クライアントを発信呼び出しが成功すると、確立しようとしている場合*ProtocolClMakeCallComplete*呼び出しを確認する必要があります\_パラメーター\_を決定するフラグを変更されたかどうか最初呼び出しのパラメータークライアントによって指定されるが変更されました。 フラグを設定すると、呼び出しのパラメーターが変更されていることを示す場合*ProtocolClMakeCallComplete*この接続で許容されるかどうかを返された呼び出しのパラメーターを調べる必要があります。

呼び出しのパラメーターが、許容される場合は*ProtocolClMakeCallComplete*単にコントロールを返します。 呼び出しのパラメーターが許容されないし、信号のプロトコルでは、この時点での再ネゴシエーションを許可している場合、クライアントが呼び出すことができる場合[ **NdisClModifyCallQoS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclmodifycallqos)関数のパラメーター (参照に変更を要求するには[呼び出しを閉じる要求を Client-Initiated](client-initiated-request-to-close-a-call.md))。 信号のプロトコルが、許容できない呼び出しのパラメーターの再ネゴシエーションを許可していない場合*ProtocolClMakeCallComplete*の呼び出しを破棄する必要があります**NdisClCloseCall**(Client-Initiated 要求を参照してください呼び出しを閉じます)。

 

 





