---
title: OPM と表示モード
description: OPM と表示モード
ms.assetid: d412a32b-7afd-4f48-9b8e-7cf66533349f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af790b4c698e9a8285d8b63d69d1612a79f16efe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840495"
---
# <a name="opm-and-display-modes"></a>OPM と表示モード


表示ミニポートドライバーは、現在使用されている表示モードに関係なく、保護された出力に関連付けられている物理コネクタでサポートされているすべての保護の種類を報告する必要があります。 表示ミニポートドライバーは、 [**DxgkDdiOPMGetInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_information)または[**DxgkDdiOPMGetCOPPCompatibleInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_copp_compatible_information)関数の呼び出しを dxgkmdt\_OPM\_取得\_サポートされている場合に、サポートされている保護の種類を報告 @no\_、 [**Dxgkmdt\_OPM\_GET\_INFO\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_get_info_parameters)構造体の**guidinformation**メンバーで設定されている種類の保護。\_ サポートされている保護の種類の取得の詳細については、「保護された[出力に関する情報の取得](retrieving-information-about-a-protected-output.md)」または「[保護された出力に関する Copp と互換性のある情報の取得](retrieving-copp-compatible-information-about-a-protected-output.md)

現在の解像度が特定の保護の種類に対して高すぎる場合、ディスプレイミニポートドライバーの[**DxgkDdiOPMConfigureProtectedOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)関数を呼び出して保護の種類の保護レベルを設定すると、ドライバーからエラーが返されます。 次のシナリオでは、ドライバーの*DxgkDdiOPMConfigureProtectedOutput*関数が成功を返し、エラーが発生した場合の例を示します。

-   保護された出力が S-Video 出力コネクタに関連付けられている場合、DXGKMDT\_OPM と共にディスプレイミニポートドライバーの*DxgkDdiOPMGetCOPPCompatibleInformation*関数を呼び出すと、サポートされている\_保護を取得\_\_\_TYPES set は、アナログコンテンツ保護 (ACP) の種類 (DXGKMDT\_OPM\_PROTECTION\_TYPE\_ACP) のサポートを示す必要があります。 その後、ドライバーの*DxgkDdiOPMConfigureProtectedOutput*関数を呼び出して、このコネクタで ACP 型のレベルを設定した場合、ドライバーは、s-ビデオの出力解像度が固定されています。これは、デスクトップの解像度 (表示モード) が高くなる可能性があります。

-   保護された出力がコンポーネントの出力コネクタに関連付けられている場合、DXGKMDT\_OPM によるミニポートドライバーの*DxgkDdiOPMGetCOPPCompatibleInformation*関数の表示は、サポートされている\_保護を取得\_\_@noまた、型セットは、ACP 型のサポートも示す必要があります。\_ ただし、ディスプレイの解像度が720p または1080i の場合、ドライバーの*DxgkDdiOPMConfigureProtectedOutput*関数を呼び出して、この出力で ACP 型のレベルを設定すると、ドライバーは OPM\_の状態\_を返し\_解決\_高エラーコード\_すぎます。 720p または1080i が解像度を超えているため、ACP 型の保護レベルをコンポーネント出力コネクタに設定できません。

 

 





