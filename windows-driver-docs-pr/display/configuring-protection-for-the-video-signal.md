---
title: ビデオ信号の保護の構成
description: ビデオ信号の保護の構成
ms.assetid: 557fc95b-1cf5-4b6d-b256-fe2db29ec0fa
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2775ba5c7876497edb6c5859c2b456b0ba63da2a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839793"
---
# <a name="configuring-protection-for-the-video-signal"></a>ビデオ信号の保護の構成


OPM 構成では、保護された出力に関連付けられている物理コネクタを通過するビデオ信号の保護を構成できます。 シグナル保護を設定するために、ディスプレイミニポートドライバーの[**DxgkDdiOPMConfigureProtectedOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)関数は、 [**Dxgkmdt\_OPM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_configure_parameters)へのポインターを受信し\_**guidsetting**メンバーを使用して\_PARAMETERS 構造を構成します。DXGKMDT\_OPM\_SET\_ACP\_を設定し、\_CGMSA\_シグナリング GUID と**Abparameters**メンバーを[**DXGKMDT\_OPM\_set\_のポインターに設定します。および\_CGMSA\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_set_acp_and_cgmsa_signaling_parameters)シグナルを保護する方法を指定するシグナル\_パラメーター構造を示します。

 

 





