---
title: HDCP SRM バージョンの設定
description: HDCP SRM バージョンの設定
ms.assetid: 23f99f8f-7d13-4868-84fb-49245a81958b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bef223ebad9ccb791cdac6f5b2b1b57610b972ef
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365544"
---
# <a name="setting-the-hdcp-srm-version"></a>HDCP SRM バージョンの設定


OPM 構成では、バージョンの高帯域幅デジタル コンテンツの保護 (HDCP) システム Renewability メッセージ (SRM) の保護された出力を設定できます。 バージョンを設定する、ディスプレイのミニポート ドライバーの[ **DxgkDdiOPMConfigureProtectedOutput** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)関数へのポインターを受け取る、 [ **DXGKMDT\_OPM\_構成\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_configure_parameters)構造体、 **guidSetting**メンバー設定、DXGKMDT\_OPM\_設定\_HDCP\_SRM GUID と**abParameters**メンバーへのポインターに設定する[ **DXGKMDT\_OPM\_設定\_HDCP\_SRM\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_set_hdcp_srm_parameters)構造体。 DXGKMDT\_OPM\_設定\_HDCP\_SRM\_パラメーター構造体には、バージョン番号を指定する ULONG が含まれています。 最下位ビット (ビット 0 ~ 15) には、リトル エンディアン形式で SRM のバージョン番号が含まれます。 SRM バージョン番号の詳細については、次を参照してください。、 [HDCP 仕様のリビジョン 1.1](https://go.microsoft.com/fwlink/p/?linkid=38728)します。

 

 





