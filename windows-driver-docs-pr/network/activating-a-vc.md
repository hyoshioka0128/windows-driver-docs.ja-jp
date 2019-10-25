---
title: VC のアクティブ化
description: VC のアクティブ化
ms.assetid: 93bac975-3c9c-424b-a815-b1589b703fb5
keywords:
- 仮想接続 WDK、アクティブ化
- 仮想接続のアクティブ化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a5b77ca8cf0aaedb3edea176733cec882defff7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838257"
---
# <a name="activating-a-vc"></a>VC のアクティブ化





仮想接続 (VC) が作成された後 ( [vc の作成](creating-a-vc.md)に関するを参照)、データを送受信する前にアクティブ化する必要があります。 呼び出しマネージャーは、 [**NdisCmActivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmactivatevc)を呼び出すことによって VC のアクティブ化を開始します (次の図を参照してください)。

![vc アクティベーションを開始する呼び出しマネージャーを示す図](images/cm-07.png)

MCM ドライバーは、 [**NdisMCmActivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmactivatevc)を呼び出すことによって VC のアクティベーションを開始します (次の図を参照してください)。

![vc アクティベーションを開始する mcm ドライバーを示す図](images/fig1-07.png)

ローカルクライアントまたはリモートパーティがその VC の呼び出しパラメーターの変更を正常にネゴシエートした場合、呼び出しマネージャーまたは MCM ドライバーがアクティブ VC の再アクティブ化を開始することができます (「[クライアントが開始した要求を閉じるための呼び出し](client-initiated-request-to-close-a-call.md)と[受信要求を変更する」を参照してください)。パラメーター](incoming-request-to-change-call-parameters.md))。 呼び出しマネージャーまたは MCM ドライバーは、1つの VC が既にアクティブな呼び出しの呼び出しパラメーターを変更するために、 **Ndis (M) CmActivateVc**を何度も呼び出すことができます。

クライアントによって開始された発信呼び出しの場合、コールマネージャーまたは MCM ドライバーは、通常、呼び出しのリモートターゲットとネゴシエートされたアグリーメントを確認するか、または成功した呼び出しの設定を使用して、パケット交換の直後に**Ndis (M) CmActivateVc**を呼び出します。切り替わり. 呼び出しマネージャーまたは MCM ドライバーは、ndis ( **m) CmMakeCallComplete**の発信呼び出し完了を ndis (およびクライアント) に通知する前に、 **ndis (m) CmActivateVc**を呼び出します (「[呼び出しを行う](making-a-call.md)」を参照してください)。 着信呼び出しの場合、通常、コールマネージャーまたは MCM ドライバーは、 **Ndisco (mcm) CreateVc**を正常に呼び出し、 **ndis (m) CmDispatchIncomingCall**を呼び出す前に、 **ndis (m) CmActivateVc**を呼び出します (「[着信呼び出しを示す」を参照してください)。](indicating-an-incoming-call.md)).

**NdisCmActivateVc**への呼び出しマネージャーの呼び出しにより、NDIS は、基になるミニポートドライバーの[**MiniportCoActivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_activate_vc)関数を呼び出します。 *MiniportCoActivateVc*は、要求された呼び出しをアダプターがサポートしていることを確認するために、この VC の呼び出しパラメーターを検証する必要があります。 呼び出しパラメーターが許容される場合、 *MiniportCoActivateVc*は必要に応じてアダプターと通信し、仮想接続を介してデータを受信または送信するようにアダプターを準備します (たとえば、受信バッファーをプログラミングします)。 要求された呼び出しパラメーターがサポートされていない場合、ミニポートドライバーは要求に失敗します。

*MiniportCoActivateVc*は同期的または非同期的に完了できます。 [**NdisMCoActivateVcComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoactivatevccomplete)を呼び出すと、NDIS が呼び出しマネージャーの[**ProtocolCmActivateVcComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_activate_vc_complete)関数を呼び出します。 *ProtocolCmActivateVcComplete*は、仮想接続が正常にアクティブ化されたことを確認するために、 **NdisMCoActivateVcComplete**によって返される状態を確認する必要があります。 ミニポートドライバーが VC を正常にアクティブ化できなかった場合、呼び出しマネージャーは VC 経由での通信を試行することはできません。 また、 *ProtocolCmActivateVcComplete*は、ネットワークメディアによって要求された処理を完了してから、NDIS に制御を返す前に、仮想接続がデータ転送の準備ができていることを確認する必要があります。

MCM ドライバーの**NdisMCmActivateVc**への呼び出しは、新しく作成された vc で call パラメーターと media パラメーターを設定したこと、または確立された vc で呼び出しパラメーターを変更したことを NDIS に通知します。 この操作は、MCM ドライバーが VC での転送の準備ができている NIC を NDIS に通知します。 NDIS は、MCM ドライバーの*ProtocolCmActivateVcComplete*関数を呼び出すことによって、アクティベーションシーケンスを完了します。

MCM ドライバーは**NdisMCmActivateVc**を呼び出して、クライアントデータの送受信に使用される vcs のみをアクティブにします。ただし、mcm ドライバーとネットワークコンポーネント (スイッチなど) の間での通信に使用される vcs をアクティブにすることはできません。 MCM ドライバーは、 **Ndis * Xxx*** 関数を呼び出さずに、シグナリング VC を内部でアクティブにします。 そのため、MCM ドライバーが独自のシグナリング用に設定した VC は、NDIS に対して不透明になります。

 

 





