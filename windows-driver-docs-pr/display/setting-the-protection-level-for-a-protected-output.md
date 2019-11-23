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


OPM 構成では、保護された出力で保護の種類の保護レベルを設定できます。 保護レベルを設定するために、表示ミニポートドライバーの[**DxgkDdiOPMConfigureProtectedOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)関数は、 [**dxgkmdt\_\_\_OPM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_configure_parameters)へのポインターを受信します。また、 **guidsetting**メンバーを dxgkmdt\_OPM\_set\_protection\_Level GUID に設定し、 **abparameters**メンバーを dxgkmdt\_OPM へのポインターに設定し\_[**保護\_レベル\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_set_protection_level_parameters)設定する保護の種類と保護を設定するレベルを指定する構造体。\_ 次の保護レベルは、指定された保護の種類に対して設定できます。

-   DXGKMDT\_OPM\_PROTECTION\_TYPE\_は、DXGKMDT の**Ulprotectiontype**メンバーに指定されている ACP\_OPM\_保護\_レベル\_パラメーターを設定\_[**dxgkmdt\_OPM\_ACP\_protection\_level**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_acp_protection_level)列挙の保護レベルの値の1つは、DXGKMDT\_OPM\_SET\_Protection\_level の**ulprotectionlevel**メンバーで指定でき\_パラメーター。

-   Dxgkmdt\_OPM\_PROTECTION\_TYPE\_OPM の**Ulprotectiontype**メンバーで指定された OPM\_PROTECTION\_レベル\_パラメーターを設定することにより、 [**DXGKMDT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_cgmsa)\_CGMSA の**ulprotectionlevel**メンバーで指定できます。また、\_保護\_レベル\_パラメーターを設定することもできます。\_\_\_\_\_

-   DXGKMDT\_OPM\_PROTECTION\_TYPE\_HDCP または DXGKMDT\_OPM\_PROTECTION\_TYPE\_COPP\_互換\_、DXGKMDT の**Ulprotectiontype**メンバーで指定された\_OPM\_設定\_保護\_レベル\_パラメーター、 [**Dxgkmdt\_OPM\_HDCP\_protection\_レベル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_hdcp_protection_level)の列挙の保護レベルの値の1つを、DXGKMDT の**Ulprotectionlevel**メンバー\_OPM\_\_保護\_レベル\_パラメーターを設定します。

-   DXGKMDT\_OPM\_PROTECTION の場合は、DXGKMDT の**Ulprotectiontype**メンバーに指定された\_OPM\_\_\_\_保護\_レベル\_パラメーターを設定[**dxgkmdt\_OPM\_の保護**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_dpcp_protection_level)レベルの値の1つは、DXGKMDT\_OPM\_SET\_PROTECTION\_Level の ulprotectionlevel**メンバーで**指定することができます。\_\_\_パラメーター。

   DXGKMDT\_OPM\_\_CSS\_に従って\_保護\_レベル\_設定されている**ことに注意**してください。 DVD GUID は Windows 7 の新機能であり、ドライバーが新しい CSS 規則に従って HDCP を有効にする必要があることを示すために使用されます。\_ DXGKMDT\_OPM\_SET\_PROTECTION\_LEVEL\_に従って\_CSS\_DVD コマンドに設定することは、既存の DXGKMDT\_OPM\_set\_protection\_LEVEL コマンドを設定することと同じです。ただし、\_CSS\_では、要求された保護を有効にするための絶対的な要件はありません。\_\_\_\_\_\_\_

 

 

 





