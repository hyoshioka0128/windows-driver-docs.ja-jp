---
title: ビデオ信号の保護の構成
description: ビデオ信号の保護の構成
ms.assetid: 557fc95b-1cf5-4b6d-b256-fe2db29ec0fa
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c86c7f7eee0adbd833fa30384e7e01516b723ecc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382354"
---
# <a name="configuring-protection-for-the-video-signal"></a>ビデオ信号の保護の構成


OPM 構成では、保護された出力に関連付けられている物理コネクタを経由するビデオ信号の保護を構成できます。 シグナル保護まで、ディスプレイのミニポート ドライバーの設定に[ **DxgkDdiOPMConfigureProtectedOutput** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)関数へのポインターを受け取る、 [ **DXGKMDT\_OPM\_構成\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_configure_parameters)構造体、 **guidSetting**メンバー設定、DXGKMDT\_OPM\_セット\_ACP\_AND\_CGMSA\_シグナリングの GUID と**abParameters**メンバーへのポインターに設定、 [ **DXGKMDT\_OPM\_設定\_ACP\_AND\_CGMSA\_シグナリング\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_set_acp_and_cgmsa_signaling_parameters)信号を保護する方法を指定する構造体。

 

 





