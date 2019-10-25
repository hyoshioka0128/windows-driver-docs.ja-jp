---
title: VC の非アクティブ化
description: VC の非アクティブ化
ms.assetid: 094e339c-b5a7-4894-9a3d-145231311647
keywords:
- 仮想接続 WDK、非アクティブ化
- 仮想接続の非アクティブ化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1788ca5b11d8f557ccc7e720b6488fb798441b2b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838175"
---
# <a name="deactivating-a-vc"></a>VC の非アクティブ化





呼び出しマネージャーは、発信または着信呼び出しを終了するための重要な手順として[**NdisCmDeactivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdeactivatevc)を呼び出します。通常は、呼び出しを破棄するネットワークコンポーネントを[使用して](client-initiated-request-to-close-a-call.md)パケット交換を行った後、[呼び出しを閉じるための受信要求](incoming-request-to-close-a-call.md)。 MCM ドライバーは、 [**NdisMCmDeactivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdeactivatevc)を呼び出すことによって同じことを行います。

**NdisCmDeactivateVc**を呼び出すと、NDIS は、基になるミニポートドライバーの[**MiniportCoDeactivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_deactivate_vc)関数を呼び出します (次の図を参照)。 *MiniportCoDeactivateVc*は、ネットワークアダプターと通信し、この VC 間のすべての通信を終了します (たとえば、アダプターで受信バッファーまたは送信バッファーをクリアします)。

![呼び出しマネージャーが vc 非アクティブ化を開始することを示す図](images/cm-08.png)

VC を非アクティブ化する前に、ミニポートドライバーが VC で保留中の転送を完了する必要があります。 つまり、ミニポートドライバーは、進行中のすべての送信を完了し、指定されたすべての受信パケットが返されるまで待機する必要があります。 VC を非アクティブ化した後、VC での受信または送信送信をミニポートドライバーで示すことはできません。

*MiniportCoDeactivateVc*では VC が削除されないことに注意してください。 再利用されない特定の VC の creator (クライアント、呼び出しマネージャー、または MCM ドライバー) は、 [**NdisCoDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscodeletevc)を呼び出して[その vc を破棄](deleting-a-vc.md)します。 非アクティブ化された VC は、接続指向クライアント、コールマネージャー、または MCM ドライバーによって再[アクティブ](activating-a-vc.md)化できます。

*MiniportCoDeactivateVc*は同期的または非同期的に完了できます。 [**NdisMCoDeactivateVcComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcodeactivatevccomplete)の呼び出し。 最初に VC 非アクティブ化を要求したコールマネージャーの[**ProtocolCmDeactivateVcComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_deactivate_vc_complete)関数を、NDIS によって呼び出します。 非アクティブ化の完了は、アクティブ化で使用される VC のすべての呼び出しパラメーターが無効になったことを意味します。 新しい呼び出しパラメーターのセットで再アクティブ化する場合を除き、VC のその他の使用は禁止されています。

MCM ドライバーの**NdisMCmDeactivateVc**への呼び出しは、vc を非アクティブ化したか、確立された vc の呼び出しパラメーターを変更したことを NDIS に通知します (次の図を参照してください)。 NDIS は、MCM ドライバーの*ProtocolCmDeactivateVcComplete*関数を呼び出すことによって、非アクティブ化シーケンスを完了します。

![vc 非アクティブ化を開始する mcm ドライバーを示す図](images/fig1-08.png)

Mcm ドライバーは**NdisMCmDeactivateVc**を呼び出して、mcm ドライバーとネットワークコンポーネント (スイッチなど) との間での信号メッセージの交換に使用される VCs を非アクティブ化します。 MCM ドライバーは、 **Ndis * Xxx*** 関数を呼び出さずに、シグナリング VC を内部的に非アクティブにします。

 

 





