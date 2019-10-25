---
title: HDCP SRM バージョンの設定
description: HDCP SRM バージョンの設定
ms.assetid: 23f99f8f-7d13-4868-84fb-49245a81958b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99169cffde19a73b054a300fed8566be6289f0e5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829498"
---
# <a name="setting-the-hdcp-srm-version"></a>HDCP SRM バージョンの設定


OPM 構成では、保護された出力に対して高帯域幅デジタル Content Protection (HDCP) システムの Renewability メッセージ (SRM) のバージョンを設定できます。 バージョンを設定するために、表示ミニポートドライバーの[**DxgkDdiOPMConfigureProtectedOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)関数は、 [**Dxgkmdt\_OPM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_configure_parameters)へのポインターを受け取ります。 **guidsetting**メンバーをに設定して\_PARAMETERS 構造を構成\_DXGKMDT\_OPM\_\_HDCP\_SRM GUID を設定し、 **Abparameters**メンバーを[**DXGKMDT\_OPM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_set_hdcp_srm_parameters)へのポインターに設定します。これにより、\_HDCP\_\_のパラメーター構造が設定されます。 DXGKMDT\_OPM\_SET\_HDCP\_SRM\_PARAMETERS 構造体には、バージョン番号を指定する ULONG が含まれています。 最下位ビット (ビット 0 ~ 15) には、低エンディアン形式での、SRM のバージョン番号が含まれています。 SRM のバージョン番号の詳細については、「 [HDCP 仕様のリビジョン 1.1](https://go.microsoft.com/fwlink/p/?linkid=38728)」を参照してください。

 

 





