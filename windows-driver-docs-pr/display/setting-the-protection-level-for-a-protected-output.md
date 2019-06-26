---
title: 保護されている出力の保護レベルの設定
description: 保護されている出力の保護レベルの設定
ms.assetid: 2f041190-8001-4e79-8398-8b642884f751
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a218a007d0fbf7599b294555b779d6d8f1568852
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365542"
---
# <a name="setting-the-protection-level-for-a-protected-output"></a>保護されている出力の保護レベルの設定


OPM 構成では、保護された出力を保護の種類の保護レベルを設定できます。 レベルを設定する、保護、ディスプレイのミニポート ドライバーの[ **DxgkDdiOPMConfigureProtectedOutput** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)関数へのポインターを受け取る、 [ **DXGKMDT\_OPM\_構成\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_configure_parameters)構造体、 **guidSetting**メンバー設定、DXGKMDT\_OPM\_セット\_保護\_レベル GUID と**abParameters**メンバーへのポインターに設定する[ **DXGKMDT\_OPM\_設定\_保護\_レベル\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_set_protection_level_parameters)セットと、保護を設定するレベルに保護の種類を指定する構造体。 指定した保護の種類は、次の保護レベルを設定できます。

-   DXGKMDT の\_OPM\_保護\_型\_ACP がで指定された、 **ulProtectionType** DXGKMDT のメンバー\_OPM\_設定\_保護\_レベル\_から保護レベル値のいずれかのパラメーター、 [ **DXGKMDT\_OPM\_ACP\_保護\_レベル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_acp_protection_level)で列挙型を指定することができます、 **ulProtectionLevel** DXGKMDT のメンバー\_OPM\_設定\_保護\_レベル\_パラメーター。

-   DXGKMDT の\_OPM\_保護\_型\_CGMSA がで指定された、 **ulProtectionType** DXGKMDT のメンバー\_OPM\_設定\_保護\_レベル\_から保護レベル値のいずれかのパラメーター、 [ **DXGKMDT\_OPM\_CGMSA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_cgmsa)列挙型指定することができます、 **ulProtectionLevel** DXGKMDT のメンバー\_OPM\_設定\_保護\_レベル\_パラメーター。

-   DXGKMDT の\_OPM\_保護\_型\_HDCP または DXGKMDT\_OPM\_保護\_型\_COPP\_互換性のある\_HDCP がで指定された、 **ulProtectionType** DXGKMDT のメンバー\_OPM\_設定\_保護\_レベル\_のいずれかのパラメーター、保護レベルの値から、 [ **DXGKMDT\_OPM\_HDCP\_保護\_レベル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_hdcp_protection_level)で列挙型を指定することができます、**ulProtectionLevel** DXGKMDT のメンバー\_OPM\_設定\_保護\_レベル\_パラメーター。

-   DXGKMDT の\_OPM\_保護\_型\_DPCP がで指定された、 **ulProtectionType** DXGKMDT のメンバー\_OPM\_設定\_保護\_レベル\_から保護レベル値のいずれかのパラメーター、 [ **DXGKMDT\_OPM\_DPCP\_保護\_レベル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ne-d3dkmdt-_dxgkmdt_dpcp_protection_level)で列挙型を指定することができます、 **ulProtectionLevel** DXGKMDT のメンバー\_OPM\_設定\_保護\_レベル\_パラメーター。

**注**   、DXGKMDT\_OPM\_設定\_保護\_レベル\_ACCORDING\_TO\_CSS\_DVD の GUID はの新機能Windows 7 をドライバーに新しい CSS 規則に従った HDCP が有効にすることを示すために使用されます。 設定、DXGKMDT\_OPM\_設定\_保護\_レベル\_ACCORDING\_TO\_CSS\_DVD コマンドは既存の DXGKMDT の設定と同じ\_OPM\_設定\_保護\_レベルのコマンドを除くその DXGKMDT\_OPM\_設定\_保護\_レベル\_に従って\_TO\_CSS\_DVD に要求された保護を有効にする絶対要件がありません。

 

 

 





