---
title: COPP 状態イベント
description: COPP 状態イベント
ms.assetid: e9d6bb04-9abd-4864-b359-3c8331843968
keywords:
- コピー防止 WDK COPP、状態
- ビデオコピー防止 WDK COPP、状態
- COPP WDK DirectX VA、状態
- 保護されたビデオ WDK COPP、状態
- 状態情報 WDK COPP
- 状態イベント WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd9dcca28682b652527a9fa05123df56521cd61e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839783"
---
# <a name="copp-status-events"></a>COPP 状態イベント


## <span id="ddk_copp_status_events_gg"></span><span id="DDK_COPP_STATUS_EVENTS_GG"></span>


このセクションは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。

外部イベントは、コネクタに適用されている保護の性質を変更したり、コネクタの種類を変更したりすることができます。 ビデオミニポートドライバーは、ドライバーが[*COPPQueryStatus*](https://docs.microsoft.com/windows-hardware/drivers/display/coppquerystatus)関数の呼び出しを受信するたびに、これらのイベントを copp アプリケーションに報告する必要があります。 ビデオミニポートドライバーは、イベントが発生した後に*COPPQueryStatus*を次に呼び出したときにのみ、指定したフラグを返すことによって、次の外部イベントを報告する必要があります。

-   接続の整合性: コンピューターとディスプレイデバイス間の接続が切断された場合、ビデオミニポートドライバーは、 [**DXVA\_COPPStatusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusdata)構造体の**dwFlags**メンバーで Copp\_linklost フラグを設定する必要があります。、 [**DXVA\_COPPStatusDisplayData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusdisplaydata)構造体、 [**DXVA\_Coppstattordcpkeydata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatushdcpkeydata)構造体、または[**DXVA\_COPPStatusSignalingCmdData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatussignalingcmddata)構造体。

-   コネクタの再構成: ユーザーが物理コネクタの構成を変更する場合、ビデオミニポートドライバーは DXVA\_COPPStatusData、DXVA の**dwFlags**メンバーで copp\_RenegotiationRequired フラグを設定する必要があります。\_COPPStatusDisplayData、DXVA\_Coppstattordcpkeydata、または DXVA\_COPPStatusSignalingCmdData 構造体。

ビデオミニポートドライバーは、DXVA\_COPPStatusData、DXVA\_COPPStatusDisplayData、DXVA\_Coppstattordcpkeydata、または DXVA\_COPPStatusSignalingCmdData 構造体の**Coppstatus**配列メンバー[**DXVA\_COPPStatusOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusoutput)構造体。 DXVA\_COPPStatusOutput へのポインターは、 [*COPPQueryStatus*](https://docs.microsoft.com/windows-hardware/drivers/display/coppquerystatus)の*poutput*パラメーターを通じて返されます。

たとえば、A と B という2つのメディア再生アプリケーションを考えてみます。各アプリケーションは、コンピューターをディスプレイモニターに接続するコネクタの HDCP 保護レベルで、それぞれが COPP を介して制御します。 各アプリケーションは、独自の一意の COPP DirectX VA デバイスを制御します。 コネクタが切断された場合、次にいずれかのアプリケーションが COPP デバイスへの[*COPPQueryStatus*](https://docs.microsoft.com/windows-hardware/drivers/display/coppquerystatus)要求を開始したときに、ビデオミニポートドライバーが copp\_linklost フラグを返します。

アプリケーション A が、その COPP デバイスで[*COPPQueryStatus*](https://docs.microsoft.com/windows-hardware/drivers/display/coppquerystatus)の呼び出しを開始することを前提としています。 次に、アプリケーション A は、COPP\_LinkLost フラグを受け取り、それに応じて動作します。 アプリケーション A が後続の*COPPQueryStatus*呼び出しを開始した場合、コネクタが再接続されない限り、copp\_linklost フラグを受け取ることはできません。 アプリケーション B は、その COPP デバイスで*COPPQueryStatus*への呼び出しを開始すると、copp\_linklost フラグを受け取り、それに応じて動作します。 もう一度、アプリケーション B は、コネクタが再接続されるまで、COPP\_LinkLost フラグを再び受信する必要はありません。

 

 





