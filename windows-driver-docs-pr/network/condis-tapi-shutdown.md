---
title: CoNDIS TAPI のシャットダウン
description: CoNDIS TAPI のシャットダウン
ms.assetid: 97baf489-9a9b-48c8-b0f8-79beea33bc38
keywords:
- いる CoNDIS WAN ドライバー WDK ネットワーク、TAPI サービス
- 電話サービス WDK の WAN、シャット ダウン
- いる CoNDIS TAPI WDK ネットワー キング、シャット ダウン
- いる CoNDIS TAPI WDK ネットワーク、操作を閉じる
- シャット ダウンの WDK ネットワーク
- WDK いる CoNDIS WAN で呼び出している CoNDIS TAPI 操作の終了
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 527003ff083868dbbe8346cf66d7c3d6d9f61498
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385096"
---
# <a name="condis-tapi-shutdown"></a>CoNDIS TAPI のシャットダウン





いる CoNDIS WAN ミニポート ドライバーがアプリケーションにその TAPI 機能を列挙した後、TAPI セッションが開始します。 セッション内で 1 つまたは複数の行を開くことができるし、1 つまたは複数の呼び出しが確立されていることができます。 行が開いている間、多くの呼び出しは、確立されていると、終了または削除します。 セッションの 1 つまたは複数の行は何度も終了開くから遷移でに移動できます。 ミニポート ドライバーがこのような遷移を処理する方法については、このセクションで説明します。

### <a name="closing-a-call"></a>呼び出しを閉じる

ローカル ノードまたはリモート ノードのいずれか、プロセスの呼び出しを終了できます。 呼び出し閉じることができます、ローカル ノードのいずれかの呼び出しに、ハンドルを持つ最後のアプリケーションが、ハンドルを閉じたためではおそらくまたはため、ミニポート ドライバーの[ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)または[*MiniportResetEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_reset)が呼び出されました。 リモート ノードがインプロセスで通話、ハングした場合、ミニポート ドライバーは呼び出しを破棄する上位層を伝える必要があります。

ローカル ノードのアプリケーションでは、呼び出しを終了する場合は、通話を切断にする必要があります。 TAPI を呼び出すアプリケーションの結果として、呼び出しが切断されている**lineDrop**関数。 この TAPI 関数呼び出しの原因を呼び出す NDPROXY ドライバー、 [ **NdisClCloseCall** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclclosecall)関数し、呼び出しの VC を表すハンドルを渡します。 NDIS を呼び出している CoNDIS WAN ミニポート ドライバーの[ **ProtocolCmCloseCall** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cm_close_call)関数。 ミニポート ドライバーは、NDIS を返す必要があります\_状態\_NDPROXY ミニポート ドライバーが完了できるようにする PENDING **NdisClCloseCall**非同期的にします。

ミニポート ドライバーの*ProtocolCmCloseCall*ローカル ノードとリモート ノード間の接続を終了するネットワーク コントロール デバイスと通信する必要があります。 ミニポート ドライバーに呼び出す必要がありますし、 [ **NdisMCmDeactivateVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmdeactivatevc)関数の呼び出しに使用される VC の非アクティブ化を開始します。

ミニポート ドライバーが、接続を終了した後、 *ProtocolCmCloseCall*呼び出すことができます、 [ **NdisMCmCloseCallComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmclosecallcomplete)関数が呼び出しのクロージャを完了します。

ミニポート ドライバーを呼び出し、プロセス内の呼び出しをリモートのノードがハングした場合、 [ **NdisCmDispatchIncomingCloseCall** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmdispatchincomingclosecall) NDISWAN および NDPROXY 着信通話を壊さずに通知する関数。

### <a name="closing-a-line"></a>行の終了

開いているハンドルと行に最後のアプリケーションがハンドルを閉じるときに、行は閉じられます。 TAPI を呼び出すアプリケーションの結果として、行が閉じられた**lineClose**関数。 この TAPI 関数の呼び出しにより、NDPROXY ドライバーで、前のセクションで説明されていると、その行のすべての呼び出しのクロージャを開始します。 ミニポート ドライバーは、これらの呼び出しを削除し、その状態をクリーンアップする必要があります。

### <a name="closing-a-session"></a>セッションを閉じる

セッションの終了を開始するには、上位層またはいる CoNDIS WAN ミニポート ドライバーのいずれか。 最後のクライアント プロセスは、上位レベルのテレフォニー モジュールから切り離されたが、各登録済みアダプターのとのセッションを終了する必要がありますを NDPROXY ドライバーが通知されます。 そのため、NDPROXY ドライバーを呼び出すには、 [ **NdisClCloseAddressFamily** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclcloseaddressfamily)関数し、TAPI アドレス ファミリにハンドルを渡します。 NDIS ミニポート ドライバーに呼び出されます[ **ProtocolCmCloseAf** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cm_close_af)関数。 ミニポート ドライバーは、指定したアダプター上で進行中は、関連するアクティビティを終了し、関連するリソースを解放する必要があります。 呼び出した後**NdisClCloseAddressFamily**クライアントは、TAPI のアドレス ファミリが無効のハンドルを検討してください。

ドライバーが開始したセッションの終了は、ミニポート ドライバーでアンロードされている場合に発生することがその*MiniportHaltEx*関数。 通常、ミニポート ドライバー NDPROXY、未処理の要求を完了し、すべての呼び出しは、終了する NDISWAN に通知します。 ミニポート ドライバーは、後でもう一度再読み込みが、前述した同じ初期化プロセスに通過はします。

いる CoNDIS WAN ミニポート ドライバーは、すべてのクライアントとドライバーの完全な再初期化が必要になるいくつかの動的再構成を無駄にする場合、セッションの終了を開始も可能性があります。 たとえば、アダプターの場合、その場で回線デバイス (サポートされている行のデバイスの数など) のモデリングが変更されました。

 

 





