---
title: VC を非アクティブ化
description: VC を非アクティブ化
ms.assetid: 094e339c-b5a7-4894-9a3d-145231311647
keywords:
- 仮想接続 WDK いる CoNDIS、非アクティブ化
- 仮想接続を非アクティブ化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d023e8d5b173156a0efd438c052984685315659
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532855"
---
# <a name="deactivating-a-vc"></a>VC を非アクティブ化





コール マネージャーを呼び出す[ **NdisCmDeactivateVc** ](https://msdn.microsoft.com/library/windows/hardware/ff561657)呼び出し (参照を廃棄するネットワーク コンポーネントとのパケット交換後に通常か、発信または着信呼び出しを閉じるときの基本的な手順として[の呼び出しを閉じる要求をクライアントが開始した](client-initiated-request-to-close-a-call.md)と[受信要求の呼び出しを閉じます](incoming-request-to-close-a-call.md))。 MCM ドライバーは、同じ動作が呼び出すことによって[ **NdisMCmDeactivateVc**](https://msdn.microsoft.com/library/windows/hardware/ff562818)します。

呼び出し**NdisCmDeactivateVc** NDIS ミニポート ドライバーの基になるを呼び出すと、 [ **MiniportCoDeactivateVc** ](https://msdn.microsoft.com/library/windows/hardware/ff559356)関数 (次の図を参照してください)。 *MiniportCoDeactivateVc*この VC 間でのすべての通信を終了するには、そのネットワーク アダプターと通信 (たとえば、クリア受信または送信バッファー アダプター)。

![vc の非アクティブ化を開始するコール マネージャーを示す図](images/cm-08.png)

VC が非アクティブ化、前に、ミニポート ドライバーは、VC の保留中の転送を完了する必要があります。 つまり、ミニポート ドライバーは、進行中のすべての送信が完了したことが示されて、パケットに返されるまで、すべての受信まで待つ必要があります。 ミニポート ドライバーを示すことはできません、VC を非アクティブ化後に受信または送信の VC に送信します。

なお*MiniportCoDeactivateVc* VC は削除されません。 作成者 (クライアント、コール マネージャー、または MCM ドライバー) を許可しない特定の VC の呼び出しを再利用[ **NdisCoDeleteVc** ](https://msdn.microsoft.com/library/windows/hardware/ff561698)に[その VC destroy](deleting-a-vc.md)します。 非アクティブ化された VC は、[再アクティブ化](activating-a-vc.md)接続指向のクライアント、コール マネージャー、または、MCM ドライバーによって。

*MiniportCoDeactivateVc*同期または非同期で完了できます。 呼び出し[ **NdisMCoDeactivateVcComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563559)します。 NDIS を呼び出すと、 [ **ProtocolCmDeactivateVcComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff570242) VC の非アクティブ化要求されたコール マネージャーの関数。 非アクティブ化の完了は、アクティブ化で使用される VC のすべての呼び出しのパラメーターが無効になったことを意味します。 再アクティブ化の呼び出しのパラメーターの新しいセットを除く、VC のさらに、使用が禁止されています。

MCM ドライバーの呼び出しを**NdisMCmDeactivateVc** NDIS に VC を非アクティブ化または確立の VC の呼び出しのパラメーターを変更したこと通知 (次の図を参照してください)。 NDIS は、MCM ドライバーを呼び出すことにより、非アクティブ化のシーケンスを完了*ProtocolCmDeactivateVcComplete*関数。

![vc の非アクティブ化を開始する、mcm ドライバーを示す図](images/fig1-08.png)

MCM にドライバーを呼び出しません**NdisMCmDeactivateVc** MCM ドライバーと、スイッチなどのネットワーク コンポーネント間のシグナリング メッセージを交換するための VCs を非アクティブ化します。 MCM にドライバーを非アクティブ化シグナリング VC 内部的にいずれを呼び出さずに**Ndis * Xxx*** 関数。

 

 





