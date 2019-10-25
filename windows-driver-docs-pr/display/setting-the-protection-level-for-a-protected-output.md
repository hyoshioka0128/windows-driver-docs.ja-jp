---
title: 保護されている出力の保護レベルの設定
description: 保護されている出力の保護レベルの設定
ms.assetid: 2f041190-8001-4e79-8398-8b642884f751
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4b50189dce5f913e75fa8cdd9cbe6c26472cbbb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829500"
---
# <a name="setting-the-protection-level-for-a-protected-output"></a>保護されている出力の保護レベルの設定


OPM 構成では、保護された出力で保護の種類の保護レベルを設定できます。 保護レベルを設定するために、ディスプレイミニポートドライバーの[**DxgkDdiOPMConfigureProtectedOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)関数は、 [**Dxgkmdt\_OPM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_configure_parameters)へのポインターを受信し\_**guidsetting**を使用して\_PARAMETERS 構造を構成します。DXGKMDT\_\_OPM に設定されたメンバーは、\_PROTECTION\_LEVEL GUID、 **Abparameters**メンバーが DXGKMDT\_OPM へのポインターに設定され\_[**保護\_レベルに設定され\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_set_protection_level_parameters)設定する保護の種類と保護を設定するレベルを指定するパラメーター構造。 次の保護レベルは、指定された保護の種類に対して設定できます。

-   DXGKMDT\_OPM\_PROTECTION\_TYPE\_は、DXGKMDT の**Ulprotectiontype**メンバーに指定された ACP\_保護\_レベル\_パラメーター、保護レベルの1つを設定します。[**dxgkmdt\_OPM\_ACP\_protection\_レベル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_acp_protection_level)列挙型の値は、DXGKMDT\_OPM\_SET\_Protection の**ulprotectionlevel**メンバーで指定でき\_レベル\_パラメーター。

-   DXGKMDT\_OPM\_PROTECTION の場合は、DXGKMDT の**Ulprotectiontype**メンバーに指定されている CGMSA\_TYPE\_保護\_レベル\_パラメーター (保護レベルの1つ) を設定\_ます。[**dxgkmdt\_OPM\_CGMSA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_cgmsa)列挙型の値は、dxgkmdt Mdt の**ulprotectionlevel**メンバーで指定できます。 OPM\_設定\_保護\_レベル\_パラメーターです。

-   DXGKMDT\_OPM\_PROTECTION\_タイプ\_HDCP または DXGKMDT\_OPM\_PROTECTION\_、DXGKMDT の**Ulprotectiontype**メンバーで指定されている\_と互換性のある\_を入力\__t_11_ OPM\_\_保護\_レベル\_パラメーターを設定します。 [**Dxgkmdt\_OPM\_HDCP\_protection\_LEVEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_hdcp_protection_level)列挙子の保護レベルの値の1つを指定できます。DXGKMDT の**Ulprotectionlevel**メンバー\_OPM\_\_保護\_レベル\_パラメーターを設定します。

-   DXGKMDT\_OPM\_PROTECTION の場合は、DXGKMDT の**Ulprotectiontype**メンバーに指定されている\_OPM\_\_の\_保護\_レベル\_パラメーター、保護レベルのいずれかを設定します。[**dxgkmdt\_OPM\_の cp\_protection\_LEVEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_dpcp_protection_level)列挙型の値は、DXGKMDT\_OPM\_SET\_Protection の**ulprotectionlevel**メンバーで指定でき\_レベル\_パラメーター。

   DXGKMDT\_OPM\_\_CSS\_に従って\_PROTECTION\_レベル\_を設定する**ことに注意**してください\_DVD GUID は Windows 7 の新機能であり、ドライバーが HDCP を有効にする必要があることを示すために使用されます。新しい CSS 規則に従います。 DXGKMDT\_OPM\_SET\_PROTECTION\_レベル\_に従って\_CSS\_DVD コマンドに設定することは、既存の DXGKMDT\_OPM\_SET\_PROTECTION を設定することと同じです。\_レベルのコマンドでは、DXGKMDT\_OPM\_設定されています。ただし、\_CSS\_に従って\_保護\_レベル\_、要求された保護を有効にするための絶対的な要件はありません。

 

 

 





