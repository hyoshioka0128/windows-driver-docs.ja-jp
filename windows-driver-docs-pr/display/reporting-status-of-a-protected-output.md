---
title: 保護されている出力の状態のレポート
description: 保護されている出力の状態のレポート
ms.assetid: 9945ae9c-1c11-4266-8a5c-d0ffe5ba4b5f
keywords:
- OPM WDK 表示、保護された出力の状態
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a0547458402743eca135b179cece5caf6155bfd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829602"
---
# <a name="reporting-status-of-a-protected-output"></a>保護されている出力の状態のレポート


外部イベントは、コネクタに適用されている保護の性質を変更したり、コネクタの種類を変更したりすることができます。 ディスプレイミニポートドライバーは、ドライバーが[**DxgkDdiOPMGetInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_information)または[**DxgkDdiOPMGetCOPPCompatibleInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_copp_compatible_information)関数の呼び出しを受信するたびに、これらのイベントを OPM アプリケーションに報告する必要があります。 表示ミニポートドライバーは、次に*DxgkDdiOPMGetInformation*または*DxgkDdiOPMGetCOPPCompatibleInformation*を呼び出したときに、イベントが発生した後にのみ、 [**DXGKMDT\_OPM\_status**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_status)列挙から指定された状態フラグを返すことによって、次の外部イベントを報告する必要があります。

<span id="Connection_working_properly"></span><span id="connection_working_properly"></span><span id="CONNECTION_WORKING_PROPERLY"></span>接続が正常に動作しています  
コンピューターとディスプレイデバイス間の接続が正常に機能している場合は、表示ミニポートドライバーは、dxgkmdt [ **\_OPM\_STANDARD\_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_standard_information)、 [**DXGKMDT\_OPM\_実際\_出力\_形式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_actual_output_format)、 [**DXGKMDT\_OPM\_ACP\_および\_CGMSA\_シグナリング**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_acp_and_cgmsa_signaling)の**ulstatusflags**メンバーで、dxgkmdt\_OPM\_status\_通常の状態フラグを設定する必要があります。、または[**Dxgkmdt\_OPM\_接続されている\_HDCP\_デバイス\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_connected_hdcp_device_information)構造です。

<span id="Connection_integrity"></span><span id="connection_integrity"></span><span id="CONNECTION_INTEGRITY"></span>接続の整合性  
コンピューターとディスプレイデバイスが切断された場合、表示ミニポートドライバーは dxgkmdt\_OPM\_STATUS\_LINK\_LOST gkmdt\_OPM の**Ulstatusflags**メンバーに設定する必要があります。これは、dxgkmdt\_\_実際の\_出力\_形式、DXGKMDT\_OPM\_ACP\_、\_CGMSA\_シグナリング、または DXGKMDT\_OPM\_接続されている\_HDCP\_デバイス\_情報構造です。\_\_

<span id="Connector_reconfigurations"></span><span id="connector_reconfigurations"></span><span id="CONNECTOR_RECONFIGURATIONS"></span>コネクタの再構成  
エンドユーザーが物理コネクタの構成を変更すると、表示ミニポートドライバーは、dxgkmdt\_OPM\_STATUS\_再ネゴシエーション\_必要な状態フラグを設定する必要が**あります。** これには、DXGKMDT\_OPM\_\_の出力\_形式、DXGKMDT\_OPM\_ACP\_および\_CGMSA\_シグナリング、または DXGKMDT\_OPM\_接続されている\_HDCP\_デバイス\_情報構造です。\_\_\_

<span id="Tampering"></span><span id="tampering"></span><span id="TAMPERING"></span>改ざん  
グラフィックスアダプターまたはアダプターのディスプレイミニポートドライバーの改ざんが発生した場合は、表示ミニポートドライバーは、dxgkmdt\_OPM\_STATUS\_改ざん\_検出**された**状態フラグを設定する必要があります。これは、DXGKMDT\_OPM\_\_の出力\_形式、DXGKMDT\_OPM\_ACP\_および\_CGMSA\_シグナリング、または DXGKMDT\_OPM\_接続されている\_HDCP\_デバイス\_情報構造です。\_\_\_

<span id="Revoked_HDCP_device"></span><span id="revoked_hdcp_device"></span><span id="REVOKED_HDCP_DEVICE"></span>無効になった HDCP デバイス  
失効した高帯域幅デジタル Content Protection (HDCP) デバイスが直接または間接的にコネクタに接続されていて、HDCP が有効になっている場合、ディスプレイミニポートドライバーは DXGKMDT\_OPM\_状態\_失効\_HDCP に設定する必要があり @no__DXGKMDT\_OPM\_標準\_情報または DXGKMDT\_OPM\_実際\_出力\_形式構造の**Ulstatusflags**メンバーの t_4_ デバイス\_接続状態フラグ。\_ HDCP が有効になっていない場合、ドライバーはこの状態フラグを設定する必要はありません。 ドライバーは、 [**DxgkDdiOPMGetInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_information)関数を呼び出したときにのみこの状態値を設定して、HDCP が有効かどうかを判断します。

ディスプレイミニポートドライバーは、DXGKMDT\_OPM\_標準\_情報へのポインターを返します。 DXGKMDT\_OPM\_実際の\_出力\_形式、DXGKMDT\_OPM\_ACP\_および\_CGMSA\_シグナリング、または dxgkmdt\_OPM\_、dxgkmdt\_OPM\_要求された\_\_デバイス\_情報構造を、Dxgkmdt\_ [**要求された情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_requested_information)の構造。 DXGKMDT\_OPM へのポインター\_要求された\_情報は、 *DxgkDdiOPMGetInformation*または*DxgkDdiOPMGetCOPPCompatibleInformation*の*requestedinformation*パラメーターを通じて返されます。

たとえば、A と B という2つのメディア再生アプリケーションを考えてみます。各アプリケーションは、OPM を介して、コンピューターをディスプレイモニターに接続するコネクタの HDCP 保護レベルを制御します。 各アプリケーションは、固有の保護された出力を制御します。 コネクタが切断された場合、次回、いずれかのアプリケーションが保護された出力に対して*DxgkDdiOPMGetInformation*または*DxgkDdiOPMGetCOPPCompatibleInformation*要求を開始したときに、ディスプレイミニポートドライバーは dxgkmdt を返します。\_OPM\_状態\_リンク\_失われた状態フラグ。

アプリケーション A が、保護された出力に対して*DxgkDdiOPMGetInformation*または*DxgkDdiOPMGetCOPPCompatibleInformation*の呼び出しを開始するための最初のものであると仮定します。 次に、アプリケーション A は DXGKMDT\_OPM\_STATUS\_LINK\_LOST フラグを受け取り、それに従って動作します。 アプリケーション A が後続の*DxgkDdiOPMGetInformation*または*DxgkDdiOPMGetCOPPCompatibleInformation*呼び出しを開始した場合は、コネクタがない限り、dxgkmdt\_OPM\_STATUS\_LINK\_LOST フラグを受け取ることはできません。もう一度切断します。 アプリケーション B は、保護された出力に対して*DxgkDdiOPMGetInformation*または*DxgkDdiOPMGetCOPPCompatibleInformation*の呼び出しを開始すると、dxgkmdt\_OPM\_STATUS\_LINK\_LOST フラグを受け取り、機能します。適切. ここでも、アプリケーション B は DXGKMDT\_OPM\_STATUS\_リンク\_失われたフラグを再度、コネクタが再び接続されるまで受信しません。

 

 





