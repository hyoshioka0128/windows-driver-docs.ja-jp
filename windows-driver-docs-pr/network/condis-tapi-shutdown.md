---
title: CoNDIS TAPI のシャットダウン
description: CoNDIS TAPI のシャットダウン
ms.assetid: 97baf489-9a9b-48c8-b0f8-79beea33bc38
keywords:
- CoNDIS WAN ドライバー WDK ネットワーク、TAPI サービス
- 電話 services WDK WAN、シャットダウン
- CoNDIS TAPI WDK ネットワーク、シャットダウン
- CoNDIS TAPI WDK ネットワーク、終了操作
- WDK ネットワークのシャットダウン
- CoNDIS TAPI 操作呼び出しの終了 WDK CONDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68b25741a6ff3e0fd3117ae5056cc53815e52075
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835051"
---
# <a name="condis-tapi-shutdown"></a>CoNDIS TAPI のシャットダウン





TAPI セッションは、CoNDIS WAN ミニポートドライバーによって TAPI 機能がアプリケーションに列挙された後に開始します。 セッション内では、1つまたは複数の行を開いて、1つまたは複数の呼び出しを確立できます。 行が開いているときに、多くの呼び出しを確立し、閉じたり、削除したりできます。 セッション中に、1つまたは複数の行が、オープンから終了に何度も遷移する可能性があります。 ミニポートドライバーがこのような遷移を処理する方法については、このセクションで説明します。

### <a name="closing-a-call"></a>呼び出しを閉じる

インプロセス呼び出しは、ローカルノードまたはリモートノードのいずれかで終了できます。 呼び出しのハンドルを持つ最後のアプリケーションがハンドルを閉じたか、またはミニポートドライバーの[*ミニ Porthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)または[*Miniporthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)が呼び出されたことが原因で、ローカルノードで呼び出しを閉じることができます。 リモートノードがインプロセス呼び出しを停止した場合、ミニポートドライバーは、呼び出しを破棄するように上位層に通知する必要があります。

ローカルノード上のアプリケーションが呼び出しを閉じる場合は、呼び出しを切断する必要があります。 TAPI **lineDrop**関数を呼び出しているアプリケーションの結果として、呼び出しは切断されます。 この TAPI 関数呼び出しによって、NDPROXY ドライバーは[**NdisClCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclclosecall)関数を呼び出し、その呼び出しの VC を表すハンドルを渡します。 さらに、NDIS は、 [**Condis**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_close_call) WAN ミニポートドライバーの機能を呼び出します。 ミニポートドライバーは、NDIS\_ステータス\_を返して NDPROXY に戻します。これにより、ミニポートドライバーは**NdisClCloseCall**を非同期に完了できます。

ミニポートドライバーの*ProtocolCmCloseCall*は、ネットワークコントロールデバイスと通信して、ローカルノードとリモートノード間の接続を終了する必要があります。 その後、ミニポートドライバーは、 [**NdisMCmDeactivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdeactivatevc)関数を呼び出して、呼び出しに使用される VC の非アクティブ化を開始する必要があります。

ミニポートドライバーが接続を終了すると、その*ProtocolCmCloseCall*は[**NdisMCmCloseCallComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmclosecallcomplete)関数を呼び出して呼び出しのクロージャを完成させることができます。

リモートノードがインプロセス呼び出しを切断すると、ミニポートドライバーは[**NdisCmDispatchIncomingCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchincomingclosecall)関数を呼び出して、着信呼び出しを破棄するように NDISWAN と ndproxy に通知します。

### <a name="closing-a-line"></a>行を閉じる

行は、開いているハンドルを持つ最後のアプリケーションがハンドルを閉じたときに閉じられます。 アプリケーションが TAPI **lineClose**関数を呼び出した結果として、線が閉じられます。 この TAPI 関数呼び出しにより、NDPROXY ドライバーは、前のセクションで説明したように、その行のすべての呼び出しのクロージャを開始します。 ミニポートドライバーは、これらの呼び出しを削除し、状態をクリーンアップする必要があります。

### <a name="closing-a-session"></a>セッションを閉じる

セッションの終了は、上位層または CoNDIS WAN ミニポートドライバーのいずれかによって開始できます。 最新のクライアントプロセスが上位レベルのテレフォニーモジュールから切断された後、NDPROXY ドライバーは、登録された各アダプターとのセッションを終了する必要があることを通知します。 これを行うために、NDPROXY ドライバーは[**NdisClCloseAddressFamily**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclcloseaddressfamily)関数を呼び出し、そのハンドルを TAPI アドレスファミリに渡します。 さらに、NDIS はミニポートドライバーの[**Protocolcmcloseaf**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_close_af)関数を呼び出します。 ミニポートドライバーは、指定されたアダプターで進行中の関連アクティビティを終了し、関連するリソースを解放する必要があります。 **NdisClCloseAddressFamily**を呼び出した後、クライアントは、TAPI アドレスファミリのハンドルが無効であると見なす必要があります。

ミニポートドライバーが*Miniporthaltex*関数でアンロードされている場合、ドライバーによって開始されるセッションの終了が発生する可能性があります。 通常、ミニポートドライバーは、未処理の NDPROXY 要求を完了し、すべての呼び出しが終了していることを NDISWAN に通知します。 ミニポートドライバーを後で再度読み込むと、前に説明したのと同じ初期化プロセスが実行されます。

また、すべてのクライアントとドライバーを再初期化する必要がある動的な再構成を無駄した場合に、セッションの終了を開始することもできます。 たとえば、アダプターのラインデバイスモデリング (サポートされているラインデバイスの数など) がその場で変更された場合などです。

 

 





