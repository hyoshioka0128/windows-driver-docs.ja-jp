---
title: 保護されている出力の状態のレポート
description: 保護されている出力の状態のレポート
ms.assetid: 9945ae9c-1c11-4266-8a5c-d0ffe5ba4b5f
keywords:
- OPM WDK の表示、保護されている出力のステータス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19b0af73f0c7a7b7ac6c2461cfcaf13c7e6da352
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383257"
---
# <a name="reporting-status-of-a-protected-output"></a>保護されている出力の状態のレポート


外部イベントには、コネクタに適用されるか、さらに、コネクタの種類は変更される保護の種類を変更できます。 ディスプレイのミニポート ドライバーは、ドライバーへの呼び出しを受信するたびに、OPM アプリケーションへのこれらのイベントを報告する必要があります、 [ **DxgkDdiOPMGetInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559725)または[ **DxgkDdiOPMGetCOPPCompatibleInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559720)関数。 ディスプレイのミニポート ドライバーがから、指定された状態フラグを返すことにより、次の外部イベントを報告する必要があります、 [ **DXGKMDT\_OPM\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff560930)列挙型でのみ、次に呼び出す*DxgkDdiOPMGetInformation*または*DxgkDdiOPMGetCOPPCompatibleInformation*イベントが発生した後。

<span id="Connection_working_properly"></span><span id="connection_working_properly"></span><span id="CONNECTION_WORKING_PROPERLY"></span>接続が正常に動作  
コンピューターと、ディスプレイ デバイス間の接続が正常に動作している場合、ディスプレイのミニポート ドライバーが、DXGKMDT を設定する必要があります\_OPM\_状態\_で通常の状態フラグ、 **ulStatusFlags**のメンバー、 [ **DXGKMDT\_OPM\_標準\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff560925)、 [ **DXGKMDT\_OPM\_実際\_出力\_形式**](https://msdn.microsoft.com/library/windows/hardware/ff560840)、 [ **DXGKMDT\_OPM\_ACP\_AND\_CGMSA\_シグナリング**](https://msdn.microsoft.com/library/windows/hardware/ff560830)、または[ **DXGKMDT\_OPM\_接続\_HDCP\_デバイス\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff560854)構造体。

<span id="Connection_integrity"></span><span id="connection_integrity"></span><span id="CONNECTION_INTEGRITY"></span>接続の整合性  
コンピューターと、ディスプレイ デバイスが切断された場合、ディスプレイのミニポート ドライバーが、DXGKMDT を設定する必要があります\_OPM\_状態\_リンク\_状態フラグの紛失、 **ulStatusFlags**、DXGKMDT のメンバー\_OPM\_標準\_情報、DXGKMDT\_OPM\_実際\_出力\_形式、DXGKMDT\_OPM\_ACP\_AND\_CGMSA\_シグナル通知、または DXGKMDT\_OPM\_接続\_HDCP\_デバイス\_情報構造体.

<span id="Connector_reconfigurations"></span><span id="connector_reconfigurations"></span><span id="CONNECTOR_RECONFIGURATIONS"></span>コネクタの再構成  
ディスプレイのミニポート ドライバーが、DXGKMDT を設定する必要があります、エンドユーザーに変更する物理的なコネクタの構成が発生した場合\_OPM\_状態\_再ネゴシエーション\_で必須フラグ、 **ulStatusFlags** 、DXGKMDT のメンバー\_OPM\_標準\_情報、DXGKMDT\_OPM\_実際\_出力\_形式、DXGKMDT\_OPM\_ACP\_AND\_CGMSA\_シグナル通知、または DXGKMDT\_OPM\_接続\_HDCP\_デバイス\_情報の構造体。

<span id="Tampering"></span><span id="tampering"></span><span id="TAMPERING"></span>改ざん  
グラフィックス アダプターまたはアダプターのディスプレイのミニポート ドライバーの改ざんが発生した場合、ディスプレイのミニポート ドライバーが、DXGKMDT を設定する必要があります\_OPM\_状態\_改ざん\_で検出された状態フラグ**ulStatusFlags** 、DXGKMDT のメンバー\_OPM\_標準\_情報、DXGKMDT\_OPM\_実際\_出力\_書式設定、DXGKMDT\_OPM\_ACP\_AND\_CGMSA\_シグナル通知、または DXGKMDT\_OPM\_接続\_HDCP\_デバイス\_情報構造体。

<span id="Revoked_HDCP_device"></span><span id="revoked_hdcp_device"></span><span id="REVOKED_HDCP_DEVICE"></span>失効した HDCP デバイス  
失効した高帯域幅デジタル コンテンツの保護 (HDCP) デバイスが直接または間接的にコネクタに接続をディスプレイのミニポート ドライバーが、DXGKMDT を設定する必要があります HDCP が有効になっている場合場合\_OPM\_状態\_が無効です\_HDCP\_デバイス\_で接続されている状態フラグ、 **ulStatusFlags** 、DXGKMDT のメンバー\_OPM\_標準\_情報または DXGKMDT\_OPM\_実際\_出力\_形式構造体。 HDCP が有効でない場合、ドライバーでは、この状態フラグを設定する必要はありません。 ドライバーでは、この状態値を設定への呼び出しからのみ、 [ **DxgkDdiOPMGetInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559725) HDCP が有効かどうかを判断する関数。

ディスプレイのミニポート ドライバーが、DXGKMDT へのポインターを返します\_OPM\_標準\_情報、DXGKMDT\_OPM\_実際\_出力\_形式、DXGKMDT\_OPM\_ACP\_AND\_CGMSA\_シグナル通知、または DXGKMDT\_OPM\_接続\_HDCP\_デバイス\_情報構造体、 **abRequestedInformation**のメンバー、 [ **DXGKMDT\_OPM\_要求された\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff560910)構造体。 DXGKMDT へのポインター\_OPM\_要求された\_によって情報が返される、 *RequestedInformation*パラメーターの*DxgkDdiOPMGetInformation*または*DxgkDdiOPMGetCOPPCompatibleInformation*します。

たとえば、2 つのメディア A と B の再生アプリケーション各アプリケーションは、OPM、ディスプレイ モニターにコンピューターを接続しているコネクタの HDCP 保護レベルを使用して制御します。 各アプリケーションは、独自の一意の保護された出力を制御します。 次回のどちらのアプリケーションを開始する場合は、コネクタが接続されていない、 *DxgkDdiOPMGetInformation*または*DxgkDdiOPMGetCOPPCompatibleInformation*要求を保護された出力に、ディスプレイのミニポート ドライバーは、DXGKMDT を返す必要があります\_OPM\_状態\_リンク\_失われた状態フラグ。

アプリケーション A は、最初の呼び出しを開始すると想定します*DxgkDdiOPMGetInformation*または*DxgkDdiOPMGetCOPPCompatibleInformation*で保護されている出力します。 アプリケーション A はその受信、DXGKMDT\_OPM\_状態\_リンク\_フラグ、および機能を適宜失われています。 アプリケーション A がそれ以降に開始する場合、 *DxgkDdiOPMGetInformation*または*DxgkDdiOPMGetCOPPCompatibleInformation*を呼び出すには、DXGKMDT を受け取らないように\_OPM\_ステータス\_リンク\_コネクタが再び接続されていない場合を除き、フラグが失われます。 アプリケーション B への呼び出しを開始するときに*DxgkDdiOPMGetInformation*または*DxgkDdiOPMGetCOPPCompatibleInformation* 、保護された出力を受信、DXGKMDT\_OPM\_状態\_リンク\_フラグ、および機能を適宜失われています。 ここでも、アプリケーション B を受け取ってはならない、DXGKMDT\_OPM\_状態\_リンク\_コネクタまで失わのフラグをもう一度がもう一度隔てになります。

 

 





