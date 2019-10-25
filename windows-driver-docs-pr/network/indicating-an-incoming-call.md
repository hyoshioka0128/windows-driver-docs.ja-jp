---
title: 着信呼び出しの表示
description: 着信呼び出しの表示
ms.assetid: ca7f4a1f-47a2-4ac0-b4a2-d0367163135f
keywords:
- WDK セットアップの呼び出し
- 受信した呼び出し (WDK)
- 受信呼び出しの WDK を示す
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98105b99f67daa32d53988bb141c16a3a85307e7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824727"
---
# <a name="indicating-an-incoming-call"></a>着信呼び出しの表示





通話マネージャーまたは MCM ドライバーは、ネットワークからのメッセージをシグナリングすることによって着信呼び出しに対して警告されます。 これらの通知メッセージから、通話マネージャーまたは MCM ドライバーは、呼び出しの呼び出しパラメーターを抽出します。これには、着信呼び出しの宛先となる SAP も含まれます。

次の図は、着信呼び出しを示す MCM ドライバーを示しています。

![着信呼び出しを示す呼び出しマネージャーを示す図](images/cm-13.png)

次の図は、着信呼び出しを示す呼び出しマネージャーを示しています。

![mcm ドライバー経由の着信呼び出しを示す](images/fig1-13.png)

着信呼び出しパラメーターが呼び出しマネージャーまたは MCM ドライバーで受け入れられない場合、シグナリングプロトコルによってこのようなネゴシエーションが許可されると、これらのパラメーターの変更をリモートパーティとネゴシエートすることができます。 または、着信呼び出しの送信先のクライアントが、呼び出しマネージャーまたは MCM ドライバーからの呼び出しを示す呼び出しパラメーターを受け取った後に、呼び出しパラメーターをネゴシエートしようとすることができます (「[クライアントが開始した要求の呼び出しパラメーターの変更](client-initiated-request-to-change-call-parameters.md)」を参照してください)。 呼び出しマネージャーまたは MCM ドライバーが、リモートパーティとの呼び出しの受け入れ可能な呼び出しパラメーターをネゴシエートできない場合、呼び出しを拒否することがあります。 このような場合に可能なことは、シグナリングプロトコルによって決まります。

クライアントへの着信呼び出しを示す前に、通話マネージャーまたは MCM ドライバーが、呼び出しの送信先となる SAP を識別する必要があります。 SAP は、クライアントによって事前に[登録](registering-a-sap.md)されている必要があります。 また、呼び出しマネージャーまたは MCM ドライバーも[vc の作成](creating-a-vc.md)を開始し、[この vc のアクティブ化](activating-a-vc.md)を開始する必要があります。

呼び出しマネージャーまたは MCM ドライバーは、着信呼び出しの送信先である SAP を登録したクライアントへの着信呼び出しを示します。 呼び出しマネージャーは、 [**NdisCmDispatchIncomingCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchincomingcall)を使用した着信呼び出しを示します。 MCM ドライバーは、 [**NdisMCmDispatchIncomingCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdispatchincomingcall)を使用した着信呼び出しを示します。

**Ndis (M) CmDispatchIncomingCall**の呼び出しでは、呼び出しマネージャーまたは mcm ドライバーは次のものを渡します。

-   受信呼び出しをアドレス指定する SAP を識別する*NdisSapHandle* 。

-   着信呼び出しの仮想回線を識別する*NdisVcHandle* 。

-   型の構造体へのポインターは、呼び出しの呼び出しパラメーターを格納する[ **\_パラメーターを\_呼び出し**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545384(v=vs.85))ます。

**Ndis (M) CmDispatchIncomingCall**を呼び出すと、ndis はクライアントの[**ProtocolClIncomingCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_incoming_call)関数を呼び出します。この関数内で、要求された接続をクライアントが受け入れるか拒否します。 *ProtocolClIncomingCall*は、SAP、VC、および呼び出しパラメーターを検証する必要があります。

*ProtocolClIncomingCall*は同期的に完了できます。また\_\_は、 [**NdisClIncomingCallComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclincomingcallcomplete)を使用して、保留と完了を非同期的に実行することができます。 **NdisClIncomingCallComplete**を呼び出すと、NDIS によって、呼び出しマネージャーまたは mcm ドライバーの[**Protocolcmincomingcallcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_incoming_call_complete)関数が呼び出されます。

*ProtocolClIncomingCall*または**NdisClIncomingCallComplete**に渡された同期完了によって返される NDIS\_状態コードは、クライアントが受信呼び出しを受け入れるか拒否するかを示します。 また、クライアントは、バッファーされた CO\_呼び出し\_PARAMETERS 構造体で、呼び出しの呼び出しパラメーターを返します。 クライアントが呼び出しパラメーターを許容できない場合に検出した場合は、シグナル化プロトコルによって許可されている場合は、呼び出しパラメーターに**Flags**\_\_\_メンバーを設定して、呼び出しパラメーターに変更を要求します変更された\_、変更された呼び出しパラメーターをバッファーされた CO\_呼び出し\_PARAMETERS 構造体に指定することにより、変更されます。

クライアントが着信呼び出しを受け入れる場合は、呼び出しが受け入れられたことを呼び出し元のエンティティに示すために、呼び出しマネージャーまたは MCM ドライバーがシグナリングメッセージを送信する必要があります。 それ以外の場合、呼び出しマネージャーまたは MCM ドライバーは、呼び出しが拒否されたことを示すシグナルメッセージを送信する必要があります。 クライアントが呼び出しパラメーターの変更を要求している場合、呼び出しマネージャーまたは MCM ドライバーは、シグナルメッセージを送信して、呼び出しパラメーターの変更を要求します。

クライアントが呼び出しを受け入れた場合、または呼び出しパラメーターでクライアントの要求された変更がリモートパーティによって受け入れられた場合、呼び出しマネージャーは[**NdisCmDispatchCallConnected**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchcallconnected)を呼び出し、mcm ドライバーは[**NdisMCmDispatchCallConnected**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdispatchcallconnected)を呼び出します。 **Ndis (M) CmDispatchCallConnected**を呼び出すと、ndis によってクライアントの*Protocolclcallconnected*関数が呼び出されます。

クライアントが呼び出しを拒否し、呼び出しマネージャーまたは MCM ドライバーが既に受信呼び出しの VC をアクティブ化している場合、呼び出しマネージャーまたは MCM ドライバーは、vc がアクティブになっている場合に VC を非アクティブ化するために**Ndis (M) CmDeactivateVc**を呼び出します。 呼び出しマネージャーまたは MCM ドライバーは、MCM ドライバーの場合は、呼び出しマネージャーまたは[**NdisMCmDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdeletevc)の場合に[**NdisCoDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscodeletevc)を呼び出すことによって、 [VC の削除](deleting-a-vc.md)を開始できます。

クライアントが呼び出しを受け入れたが、エンドツーエンド接続が正常に確立されなかった場合 (たとえば、リモートパーティが呼び出しを t した場合)、呼び出しマネージャーまたは MCM ドライバーは**Ndis (M) CmDispatchCallConnected**を呼び出しません。 代わりに、ndis **(M) CmDispatchIncomingCloseCall**を呼び出します。これにより、ndis はクライアントの*ProtocolClIncomingCloseCall*関数を呼び出します。 その後、クライアントは[**NdisClCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclclosecall)を呼び出して、呼び出しの破棄を完了する必要があります。 次に、呼び出しマネージャーまたは MCM ドライバーが**Ndis (M) CmDeactivateVC**を呼び出して、着信呼び出し用に作成された[VC を非アクティブ化](deactivating-a-vc.md)します。 呼び出しマネージャーまたは MCM ドライバーは、MCM ドライバーの場合は、呼び出しマネージャーまたは[**NdisMCmDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdeletevc)の場合に[**NdisCoDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscodeletevc)を呼び出すことによって、 [VC の削除](deleting-a-vc.md)を開始できます。

 

 





