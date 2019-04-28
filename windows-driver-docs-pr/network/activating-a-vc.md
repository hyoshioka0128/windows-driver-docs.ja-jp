---
title: VC のアクティブ化
description: VC のアクティブ化
ms.assetid: 93bac975-3c9c-424b-a815-b1589b703fb5
keywords:
- 仮想接続 WDK いる CoNDIS、アクティブ化します。
- 仮想接続をアクティブ化します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef37c5890defea210427ea7e1a37e026030a2a2d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367952"
---
# <a name="activating-a-vc"></a>VC のアクティブ化





仮想接続 (VC) が作成された後 (を参照してください[作成 VC](creating-a-vc.md))、データを送信または受信を前に、アクティブにする必要があります。 コール マネージャーは、呼び出すことによって、VC のアクティブ化を開始[ **NdisCmActivateVc**](https://msdn.microsoft.com/library/windows/hardware/ff561649)(次の図を参照してください)。

![vc のアクティブ化を開始するコール マネージャーを示す図](images/cm-07.png)

MCM ドライバーは、呼び出すことによって、VC のアクティブ化を開始します[ **NdisMCmActivateVc**](https://msdn.microsoft.com/library/windows/hardware/ff562792)(次の図を参照してください)。

![vc のアクティブ化を開始する、mcm ドライバーを示す図](images/fig1-07.png)

その VC の呼び出しのパラメーターの変更が正常にネゴシエート ローカル クライアントまたはリモート パーティの場合、コール マネージャーまたは MCM ドライバーすると、active の VC の再アクティブ化が開始する可能性があります (を参照してください[Client-Initiated の要求の呼び出しを閉じます](client-initiated-request-to-close-a-call.md)と[呼び出しのパラメーターを変更する着信要求](incoming-request-to-change-call-parameters.md))。 コール マネージャーまたは MCM のドライバーを呼び出すことができます**Ndis (M) CmActivateVc**を既にアクティブな呼び出しの呼び出しのパラメーターを変更する 1 つの VC の回数。

クライアント主導の発信呼び出しでは、コール マネージャーまたは MCM ドライバーは、通常の呼び出し**Ndis (M) CmActivateVc**リモート ターゲットでネゴシエートされたアグリーメントを呼び出し、または成功したことを確認のパケット交換直後スイッチでは、呼び出しセットアップします。 コール マネージャーまたは MCM ドライバー呼び出し**Ndis (M) CmActivateVc**で NDIS (とクライアント) の送信呼び出しの完了を通知する前に**Ndis (M) CmMakeCallComplete**(を参照してください[呼び出しを行う](making-a-call.md)). ドライバーの通常の呼び出しの着信呼び出し、コール マネージャーまたは MCM **Ndis (M) CmActivateVc**呼び出し後に**NdisCo (MCm) CreateVc**正常にし、その前に呼び出す**Ndis(M)CmDispatchIncomingCall**(を参照してください[着信呼び出しを示す](indicating-an-incoming-call.md))。

呼び出しをコール マネージャーの**NdisCmActivateVc** NDIS を呼び出すと、 [ **MiniportCoActivateVc** ](https://msdn.microsoft.com/library/windows/hardware/ff559351)基になるミニポート ドライバーの機能。 *MiniportCoActivateVc*アダプターが、要求された呼び出しをサポートできることを確認するには、この VC の呼び出しのパラメーターを検証する必要があります。 呼び出しのパラメーターが、許容される場合は*MiniportCoActivateVc*仮想接続経由でデータを送信または受信するアダプターを準備する必要に応じて、アダプターと通信 (たとえば、プログラミングがバッファーを受信する)。 要求された呼び出しのパラメーターをサポートできない場合、ミニポート ドライバー、要求は失敗します。

*MiniportCoActivateVc*同期または非同期で完了できます。 呼び出し[ **NdisMCoActivateVcComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563558)と呼び出しを上司に NDIS [ **ProtocolCmActivateVcComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff570238)関数。 *ProtocolCmActivateVcComplete*によって返される状態を確認する必要があります**NdisMCoActivateVcComplete**仮想接続が正常にアクティブになったことを確認します。 ミニポート ドライバーが正常にアクティブ化していない、VC 場合、コール マネージャーは、VC 経由での通信を試行する必要があります。 *ProtocolCmActivateVcComplete*もネットワーク メディアが仮想の接続が NDIS に制御を返すまでにデータ転送の準備完了であることを確認するために必要な処理を完了する必要があります。

MCM ドライバーの呼び出しを**NdisMCmActivateVc** vc を新しく作成されたメディアと呼び出しのパラメーターを設定または確立の VC の呼び出しのパラメーターを変更したことは、NDIS を通知します。 このアクションでは、MCM ドライバーが行ったこと、NIC、VC 上の転送の準備ができて、NDIS に通知します。 NDIS は、MCM ドライバーを呼び出すことでアクティブ化のシーケンスを完了*ProtocolCmActivateVcComplete*関数。

MCM にドライバーを呼び出す**NdisMCmActivateVc** VCs など、MCM ドライバーとネットワーク コンポーネント間のシグナリング メッセージを交換するためのライセンス認証が、転送やクライアントのデータを受信するための VCs のみをアクティブ化する、スイッチです。 MCM にドライバーをアクティブにシグナリング VC 内部的にいずれを呼び出さずに**Ndis * Xxx*** 関数。 独自の目的でシグナル通知の MCM にドライバーを設定する任意の VC を NDIS に対して非透過的したがってです。

 

 





