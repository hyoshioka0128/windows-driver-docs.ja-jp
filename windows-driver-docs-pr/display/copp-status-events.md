---
title: COPP 状態イベント
description: COPP 状態イベント
ms.assetid: e9d6bb04-9abd-4864-b359-3c8331843968
keywords:
- WDK COPP、状態の保護をコピーします。
- ビデオのコピー防止 WDK COPP、状態
- COPP WDK DirectX va なので、状態
- ビデオの WDK COPP、状態の保護
- WDK COPP のステータス情報
- WDK COPP の状態イベント
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5b78dbafc4a5a923982a57983d1dd3062055d2b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361941"
---
# <a name="copp-status-events"></a>COPP 状態イベント


## <span id="ddk_copp_status_events_gg"></span><span id="DDK_COPP_STATUS_EVENTS_GG"></span>


このセクションには、Windows Server 2003 SP1 にのみ以降が適用されますおよび Windows XP SP2 以降。

外部イベントには、コネクタに適用されるか、さらに、コネクタの種類は変更される保護の種類を変更できます。 ビデオのミニポート ドライバーは、ドライバーへの呼び出しを受信するたびに、COPP アプリケーションへのこれらのイベントを報告する必要があります、 [ *COPPQueryStatus* ](https://msdn.microsoft.com/library/windows/hardware/ff539652)関数。 ビデオのミニポート ドライバーには、次の呼び出しでのみ、指定したフラグを返すことによって、次の外部イベントを報告する必要があります*COPPQueryStatus*イベントが発生した後。

-   接続の整合性:ビデオのミニポート ドライバーが、COPP を設定する必要があります、コンピューターと、ディスプレイ デバイス間の接続が接続されていないになると、\_LinkLost フラグ、 **dwFlags**のメンバー、 [ **DXVA\_COPPStatusData** ](https://msdn.microsoft.com/library/windows/hardware/ff563154)構造、 [ **DXVA\_COPPStatusDisplayData** ](https://msdn.microsoft.com/library/windows/hardware/ff563157)構造、 [ **DXVA\_COPPStatusHDCPKeyData** ](https://msdn.microsoft.com/library/windows/hardware/ff563896)構造体、または[ **DXVA\_COPPStatusSignalingCmdData** ](https://msdn.microsoft.com/library/windows/hardware/ff563905)構造体。

-   コネクタの再構成:ユーザーを変更する物理的なコネクタの構成が発生する場合、ビデオのミニポート ドライバーが、COPP を設定する必要があります\_RenegotiationRequired フラグ、 **dwFlags**メンバーは、DXVA の\_COPPStatusData、DXVA\_COPPStatusDisplayData、DXVA\_COPPStatusHDCPKeyData、または DXVA\_COPPStatusSignalingCmdData 構造体。

ビデオのミニポート ドライバーは、DXVA にポインターを返します\_COPPStatusData、DXVA\_COPPStatusDisplayData、DXVA\_COPPStatusHDCPKeyData、または DXVA\_COPPStatusSignalingCmdData 構造、 **COPPStatus**の配列のメンバー、 [ **DXVA\_COPPStatusOutput** ](https://msdn.microsoft.com/library/windows/hardware/ff563903)構造体。 DXVA へのポインター\_COPPStatusOutput がによって返される、 *pOutput*パラメーターの[ *COPPQueryStatus*](https://msdn.microsoft.com/library/windows/hardware/ff539652)します。

たとえば、A と B の COPP、ディスプレイ モニターにコンピューターを接続しているコネクタの HDCP 保護レベルを使用して各制御する 2 つのメディアの再生アプリケーションを検討してください。 各アプリケーションは、独自の一意の COPP DirectX VA デバイスを制御します。 コネクタが接続されていないになるかどうかは、次回のどちらのアプリケーションを開始、 [ *COPPQueryStatus* ](https://msdn.microsoft.com/library/windows/hardware/ff539652)ビデオのミニポート ドライバーは、COPP を返す必要があります、COPP デバイスへの要求\_LinkLost フラグです。

アプリケーション A は、最初の呼び出しを開始すると想定します[ *COPPQueryStatus* ](https://msdn.microsoft.com/library/windows/hardware/ff539652) COPP デバイス上でします。 アプリケーション A はその受信、COPP\_LinkLost フラグし、適宜処理します。 アプリケーション A がそれ以降に開始する場合、 *COPPQueryStatus*を呼び出すには、COPP を受け取らないように\_LinkLost フラグ、コネクタが再び接続されていない場合を除き、します。 アプリケーション B への呼び出しを開始するときに*COPPQueryStatus*その COPP デバイスで受信、COPP\_LinkLost フラグし、適宜処理します。 ここでも、アプリケーション B を受け取ってはならない、COPP\_コネクタまで LinkLost フラグがもう一度隔てになります。

 

 





