---
title: 接続の状態を示す
description: 接続の状態を示す
ms.assetid: 8a511c14-6b09-47fe-90de-6a90dab93171
keywords:
- WMI の WDK にネットワーク接続、メディア接続の状態
- ミニポート ドライバー WDK ネットワー キング、メディア接続の状態
- NDIS ミニポート ドライバー WDK、メディア接続の状態
- 接続状態の WDK ネットワーク
- メディア接続 WDK ネットワーク
- NDIS_STATUS_MEDIA_CONNECT
- NDIS_STATUS_MEDIA_DISCONNECT
- WDK の NDIS ミニポートのステータス情報
- 状態インジケーターの WDK ネットワー キング、メディアの接続
- スリープ状態の WDK ネットワーク
- WDK ネットワークの状態を解除
- WDK ネットワークの状態をリセットします。
- WDK ネットワークの状態を停止します。
- WDK ネットワークの状態を初期化しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e20ba3d0a83831cf1482f79da792e21b10a3b921
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532878"
---
# <a name="indicating-connection-status"></a>接続の状態を示す





ミニポート ドライバーは呼び出し[ **NdisMIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563600)または[ **NdisMCoIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563562)メディア接続の変更を示す状態です。 ミニポート ドライバーを通過する次の状態インジケーターのいずれかの**NdisM (Co) IndicateStatus**:

<a href="" id="ndis-status-media-connect"></a>NDIS\_状態\_メディア\_接続  
接続を切断からのメディア接続状態変更を示します。 メディアの状態の接続、切断されたアダプターがネットワーク接続を行うと、変更が発生します。 たとえば、(ワイヤレス アダプター) の範囲内に入ることや、ユーザーは、ネットワーク ケーブルを接続するときに、アダプターが接続します。

<a href="" id="ndis-status-media-disconnect"></a>NDIS\_状態\_メディア\_切断  
接続を切断する接続からのメディア接続の状態変更を示します。 メディア切断状態の変更は、接続されているアダプターがネットワーク接続を失ったときに発生します。 たとえば、アダプターでは、(ワイヤレス アダプター) の範囲外であるか、ユーザーからネットワーク ケーブルを切り離しために、接続が失われます。

未指定の場合、ミニポート ドライバーは、状態の変更を検出した後、2 秒以内メディア接続状態の変更を示す必要があります。

ミニポート ドライバーでは、(次の一覧を参照してください) の特定の操作を実行中にメディア接続の状態を確認できます。 状態、同じように、操作を開始する前に、操作が完了した後である場合、ミニポート ドライバーが操作中に発生した、状態の変更を報告する必要はありません。

次の一覧には、メディア、ミニポート ドライバーの接続状態の変更を示す追加の要件について説明します。

<a href="" id="resetting"></a>リセットします。  
NDIS 呼び出し[ *MiniportResetEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559432)ミニポート ドライバーをリセットします。 同期または非同期、ミニポート ドライバーでは、リセットを完了できます。

リセットした後にメディア接続の状態が異なる場合、ドライバーは、リセットを完了した後、2 秒以内状態を示します。

メディア接続の状態と判断されるまで、ミニポート ドライバーは、リセット操作を完了できません。

<a href="" id="halting"></a>停止します。  
NDIS を呼び出すと、ミニポート ドライバーは、メディア接続状態の変更を示していない必要があります[ *MiniportHaltEx*](https://msdn.microsoft.com/library/windows/hardware/ff559388)します。

<a href="" id="initializing"></a>初期化  
NDIS ミニポート ドライバーを呼び出す[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)アダプターを初期化します。 アダプターの初期化中に、ミニポート ドライバーは次のガイドラインに従う必要があります。

-   返された後、ミニポート ドライバーがメディア接続の状態を表していない場合*MiniportInitializeEx*、NDIS の値を使用して、 **MediaConnectState**のメンバー、 [ **NDIS\_ミニポート\_アダプター\_全般\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)メディア接続状態を確認する構造体。 ミニポート ドライバーがドライバーを呼び出すときに、この構造体に NDIS を提供[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)からその*MiniportInitializeEx*関数。

    **注**  場合、 **MediaConnectState** MediaConnectStateUnknown にメンバーが設定されている、アダプターが切断されている場合は、NDIS が続行されます。

     

-   NDIS 呼び出した後、アダプターが接続されている場合*MiniportInitializeEx*、ミニポート ドライバーが NDIS を示す\_状態\_メディア\_から戻った後に5秒以内のCONNECT*MiniportInitializeEx*します。

-   NDIS 呼び出した後、アダプターが切断された場合*MiniportInitializeEx*、ミニポート ドライバーは、NDIS を示す必要があります\_状態\_メディア\_から戻った後に2秒以内の切断*MiniportInitializeEx*します。

-   ミニポート ドライバーが処理する必要があります、初期化中に[OID\_GEN\_メディア\_CONNECT\_状態](https://msdn.microsoft.com/library/windows/hardware/ff569604)または[OID\_GEN\_CO\_メディア\_CONNECT\_状態](https://msdn.microsoft.com/library/windows/hardware/ff569455)非同期的に要求します。 ミニポート ドライバーは、接続の状態と判断された後までには、このような要求を完了できません。

-   メディアの接続状態の決定は、初期化を遅延しない必要があります。 必要に応じてのかどうか、ミニポート ドライバーする必要があります内で接続の状態を確認するプロセスを開始*MiniportInitializeEx*、後で、プロセスを完了します。 たとえば、ミニポート ドライバーは、アダプターの接続の状態をポーリングするタイマーを設定する可能性があります。

-   逆シリアル化されたミニポート ドライバーには、初期化中に、メディアが切断がシリアル化されたミニポート ドライバーがない必要がありますを指定できます。

<a href="" id="sleeping"></a>スリープ状態  
受信すると、ミニポート ドライバーがネットワーク スリープ状態に入る、 [OID\_PNP\_設定\_POWER](https://msdn.microsoft.com/library/windows/hardware/ff569780) D1、d2 に切り替わり、または D3 のデバイスの電源状態を設定する要求。

ミニポート ドライバーである必要がありますがスリープ状態に入ると、またはスリープ状態になっている、メディア接続状態の変更は示されません。

<a href="" id="waking"></a>ウェイク アップ  
OID の受信時に、ミニポート ドライバーがスリープ状態から再開\_PNP\_設定\_D0 にデバイスの電源状態を設定する電源要求。

スリープ状態の前に、アダプターのメディア接続の状態、状態と同じがスリープ解除した後であった場合ミニポート ドライバーがメディア接続状態の変更を示していません。 接続の状態が変更された場合、ミニポート ドライバーは、スリープ解除後の 2 つの数秒以内新しい接続の状態を示す必要があります。

ミニポート ドライバー、スリープ中に OID を処理する必要があります\_GEN\_メディア\_CONNECT\_状態または OID\_GEN\_CO\_メディア\_CONNECT\_状態を非同期的に要求します。 ミニポート ドライバーは、接続の状態と判断された後までには、このような要求を完了できません。

 

 





