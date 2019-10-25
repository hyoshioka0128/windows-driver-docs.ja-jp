---
title: 呼び出しの実行
description: 呼び出しの実行
ms.assetid: b5273df1-b99f-415c-a099-16a51f3329ee
keywords:
- WDK セットアップの呼び出し
- WDK の呼び出しを行う
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6956556adad86bef889f2d9fa0b2efb7ce39bce
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844131"
---
# <a name="making-a-call"></a>呼び出しの実行





次の図は、呼び出しマネージャーを使用して発信呼び出しを行うクライアントを示しています。

![呼び出しマネージャーを使用して発信通話を行うクライアントを示す図](images/cm-11.png)

次の図は、MCM ドライバーを使用して発信呼び出しを行うクライアントを示しています。

![mcm ドライバーを使用して発信通話を行うクライアントを示す図](images/fig1-11.png)

発信通話を行う前に、接続指向クライアントで次のことを行う必要があります。

-   型の構造体の呼び出しパラメーターを初期化し[ **\_パラメーターを呼び出し\_** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545384(v=vs.85))します。 呼び出しマネージャーまたは MCM ドライバーは、通常、呼び出しを設定するためにクライアントが指定する呼び出しパラメーターを使用し、ミニポートドライバーで使用するメディアパラメーターを取得します。

-   [**NdisCoCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscocreatevc)を使用して[VC の作成](creating-a-vc.md)を開始します。

**NdisCoCreateVc**が正常に返された場合、クライアントは[**NdisClMakeCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclmakecall)を呼び出して呼び出しを開始します (このセクションの2つの図を参照してください)。

**NdisClMakeCall**を呼び出すと、クライアントは、前に初期化されたパラメーター構造\_CO\_呼び出しへのポインターを渡します。 また、クライアントは、呼び出しのデータを送信する (および受信する) ことになる VC を識別する*NdisVcHandle* ( **NdisCoCreateVc**によって返される) も渡します。 クライアントがマルチポイント呼び出し (複数のリモートパーティの呼び出し) を行う場合は、クライアントによって割り当てられた常駐コンテキスト領域へのハンドルを指定する*Protocolpartycontext*も渡します。この場合、クライアントは、multipoint VC のパーティ。

**NdisClMakeCall**を呼び出すと、NDIS は、この要求を、クライアントが指定された*NdisVcHandle*を共有する呼び出しマネージャーまたは Mcm ドライバーの[**ProtocolCmMakeCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_make_call)関数に転送します。 *ProtocolCmMakeCall*は、クライアントによって設定された入力呼び出しパラメーターを検証する必要があります。

*ProtocolCmMakeCall*は、ネットワークコントロールデバイスとの通信 (シグナリングメッセージ交換) を行い、接続を確立します。 呼び出しマネージャーは、このような exchange を開始するために[**NdisCoSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscosendnetbufferlists)を呼び出します (「 [CONDIS からの NET\_バッファー構造の送信](sending-net-buffer-structures-from-condis-drivers.md)」を参照してください)。 MCM ドライバーは**NdisCoSendNetBufferLists**を呼び出すことはありません。 代わりに、データをネットワーク経由で直接転送します。

呼び出しマネージャーまたは MCM ドライバーは、関連するネットワークコンポーネントとのネゴシエーション中に、クライアントが指定した呼び出しパラメーターを変更できます。また、 **NdisClMakeCall**に最初に与えられたクライアントとは異なるトラフィックパラメーターを返すことができます (「受信要求」を参照してください)。 [呼び出しパラメーターを変更する](incoming-request-to-change-call-parameters.md)場合)。

*ProtocolCmMakeCall*に渡された明示的な*Ndispartyhandle*は、クライアントによって作成された VC が multipoint 呼び出しに使用されることを示します。 呼び出しマネージャーまたは MCM ドライバーは、パーティごとの状態情報を保持し、multipoint 呼び出しを制御するために必要なリソースを割り当てて初期化する必要があります。

呼び出しマネージャーは、その中で必要とされるネットワークハードウェアとのすべての必要な通信を完了した後、 [**NdisCmActivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmactivatevc)を呼び出して、呼び出しデータの送信と受信を行う[VC のアクティベーション](activating-a-vc.md)を開始する必要があります。 MCM ドライバーは[**NdisMCmActivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmactivatevc)を呼び出す必要があります。

基になるミニポートドライバーが VC にデータを転送する準備ができたとき (つまり、VC がアクティブになった後)、呼び出しマネージャーは[**NdisCmMakeCallComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmmakecallcomplete)を呼び出し、mcm ドライバーは[**NdisMCmMakeCallComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmmakecallcomplete)を呼び出します。 この時点で、呼び出しマネージャーまたは MCM ドライバーは、VC の呼び出しパラメーターを確立するためにネットワークとネゴシエートし、基になるミニポートドライバーが VC のアクティブ化を完了している必要があります。

**Ndis (M) CmMakeCallComplete**の呼び出しでは、呼び出しマネージャーまたは mcm ドライバーが、VC の呼び出しパラメーターを\_型の構造体へのポインターとして渡して\_パラメーターを呼び出します。 呼び出しマネージャーがクライアントによって最初に指定された呼び出しパラメーターを変更した場合は、\_パラメーター構造の CO\_呼び出しで\_PARAMETERS\_CHANGED フラグを設定することによって、クライアントに通知できます。

**Ndis (M) CmMakeCallComplete**を呼び出すと、ndis は発信呼び出しを発信したクライアントの[**ProtocolClMakeCallComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_make_call_complete)関数を呼び出します。 *ProtocolClMakeCallComplete*を呼び出すと、呼び出しマネージャーが**NdisClMakeCall**との仮想接続を確立するためのクライアントの要求の処理を完了したことを示します。

クライアントが発信呼び出しを確立しようとしたときに成功した場合、 *ProtocolClMakeCallComplete*は、呼び出し\_PARAMETERS\_CHANGED フラグをチェックして、クライアントによって最初に指定された呼び出しパラメーターがであるかどうかを確認する必要があります。変更. 呼び出しパラメーターが変更されたことを示すフラグが設定されている場合、 *ProtocolClMakeCallComplete*は、返された呼び出しパラメーターを調べて、この接続で許容されるかどうかを判断する必要があります。

呼び出しパラメーターが許容される場合、 *ProtocolClMakeCallComplete*は単に control を返します。 呼び出しパラメーターが受け入れられず、シグナリングプロトコルでこの時点で再ネゴシエーションが許可されている場合、クライアントは[**NdisClModifyCallQoS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclmodifycallqos)を呼び出して、呼び出しパラメーターの変更を要求できます (「[クライアントが開始した呼び出しを閉じる要求](client-initiated-request-to-close-a-call.md)」を参照してください)。 シグナリングプロトコルで、許容できない呼び出しパラメーターの再ネゴシエーションが許可されていない場合、 *ProtocolClMakeCallComplete*は**NdisClCloseCall**で呼び出しを破棄する必要があります (「クライアントが開始した呼び出しを閉じる要求」を参照してください)。

 

 





