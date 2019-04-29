---
title: 呼び出しを閉じるための着信要求
description: 呼び出しを閉じるための着信要求
ms.assetid: ecdcb74d-6151-4e2b-8fe7-95f455f4deb4
keywords:
- close の呼び出しを受信した要求の WDK いる CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5093c65717a634b159e8812c4324dc4df6d61c37
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327803"
---
# <a name="incoming-request-to-close-a-call"></a>呼び出しを閉じるための着信要求





リモート クライアントは、呼び出しを終了するとき、ローカル コール マネージャーまたは MCM ドライバーがローカル クライアントにこの着信要求を示す必要があります。 コール マネージャーは、このような要求を示すために[ **NdisCmDispatchIncomingCloseCall** ](https://msdn.microsoft.com/library/windows/hardware/ff561670)で、 *CloseStatus* NDIS に設定\_状態\_成功した場合 (次の図を参照してください)。

![呼び出しを閉じますコール マネージャーにより、受信要求を示す図 ](images/cm-22.png)

MCM にドライバーを呼び出す[ **NdisMCmDispatchIncomingCloseCall** ](https://msdn.microsoft.com/library/windows/hardware/ff563541)受信要求の呼び出しを終了することを示す (次の図を参照してください)。

![呼び出しを閉じます mcm ドライバーを通じて、受信要求を示す図 ](images/fig1-22.png)

コール マネージャーまたは MCM ドライバーも呼び出せる**Ndis (M) CmDispatchIncomingCloseCall**:

-   その[ **ProtocolCmIncomingCallComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff570245)接続指向クライアントが着信呼び出しに応答呼び出しのパラメーターの許容の変更を要求するいると判断した場合の関数コール マネージャーまたは MCM ドライバーで示される以前 (を参照してください[呼び出しパラメーターの変更を受信した要求](incoming-request-to-change-call-parameters.md))。

-   ネットワークの異常な状態では、アクティブな呼び出しを壊さずコール マネージャーを強制場合します。

呼び出し**Ndis (M) CmDispatchIncomingCloseCall** NDIS を呼び出すと、 [ **ProtocolClIncomingCloseCall** ](https://msdn.microsoft.com/library/windows/hardware/ff570230)は接続指向のクライアントの機能接続します。 *ProtocolClIncomingCloseCall*接続が切断されているが、独自のクライアントまたはクライアントの通知など、任意のプロトコルにより決定された操作を実行する必要があります。 呼び出しの場合、終了するは、クライアントによって作成された multipoint VC *ProtocolClIncomingCloseCall*呼び出す必要があります[ **NdisClDropParty** ](https://msdn.microsoft.com/library/windows/hardware/ff561629) 1 つまたは複数回、1 つのパーティのみVC 上に残ります (を参照してください[Multipoint 呼び出しからパーティを削除する](dropping-a-party-from-a-multipoint-call.md))。

*ProtocolClIncomingCloseCall*呼び出す必要がありますし、 [ **NdisClCloseCall**](https://msdn.microsoft.com/library/windows/hardware/ff561627)(の場合は、VC がクライアントによって作成された multipoint VC VC の最後のパーティを識別するハンドル) を確認する、クライアントは、送信、またはこの特定の VC 上のデータを受信することが不要になった試みます。 コール マネージャーまたは MCM ドライバーは、この VC を作成した場合*ProtocolClIncomingCloseCall*呼び出した後、制御を返す必要があります**NdisClCloseCall**します。 コール マネージャーまたは MCM ドライバー、VC を無効する必要があります (を参照してください[VC を非アクティブ化](deactivating-a-vc.md))。

クライアントがこの発信呼び出しの VC を最初に作成する場合と*CloseStatus*は NDIS\_状態\_成功すると、 *ProtocolClIncomingCloseCall* VC を破棄できます必要に応じて[ **NdisCoDeleteVc**](https://msdn.microsoft.com/library/windows/hardware/ff561698)(を参照してください[VC を削除する](deleting-a-vc.md)) または別の呼び出しの VC を再利用します。 場合*CloseStatus* NDIS でない\_状態\_成功すると、 *ProtocolClIncomingCloseCall*呼び出す必要があります**NdisCoDeleteVc**します。

場合は、コール マネージャーまたは MCM ドライバー最初に作成されたこの VC の着信通話をコール マネージャーまたは MCM ドライバーが必要に応じて[削除 VC](deleting-a-vc.md)それぞれ呼び出すことによって**NdisCoDeleteVc**または[**NdisMCmDeleteVc**](https://msdn.microsoft.com/library/windows/hardware/ff562819)します。

 

 





