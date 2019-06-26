---
title: OPM と表示モード
description: OPM と表示モード
ms.assetid: d412a32b-7afd-4f48-9b8e-7cf66533349f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a12046162847530e6d37a670d0c2842b5268d03f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372757"
---
# <a name="opm-and-display-modes"></a>OPM と表示モード


ディスプレイのミニポート ドライバーには、現在使用されている表示モードに関係なく、保護された出力に関連付けられている物理コネクタでサポートされているすべての保護の種類を報告する必要があります。 呼び出しを受信すると、ディスプレイのミニポート ドライバーがサポートされている保護の種類を報告、 [ **DxgkDdiOPMGetInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_get_information)または[ **DxgkDdiOPMGetCOPPCompatibleInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_get_copp_compatible_information) DXGKMDT で関数を\_OPM\_取得\_サポートされている\_保護\_で設定の種類**guidInformation**のメンバー、 [ **DXGKMDT\_OPM\_取得\_情報\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_get_info_parameters)構造体。 サポートの取得の詳細については、保護の種類を参照してください[の保護されている出力に情報の取得](retrieving-information-about-a-protected-output.md)または[保護されている出力に関する COPP と互換性のある情報を取得する](retrieving-copp-compatible-information-about-a-protected-output.md)します。

現在の解像度が特定の保護の種類の高すぎる場合は、ドライバーはエラーを返す必要がありますとディスプレイ ミニポート ドライバーの[ **DxgkDdiOPMConfigureProtectedOutput** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)関数が呼び出されますその保護の種類の保護レベルを設定します。 場合の例を次のシナリオに与えるドライバーの*DxgkDdiOPMConfigureProtectedOutput*関数が成功した場合に返す必要があり、ときにエラー。

-   保護されている出力はコネクタでは、s-ビデオ出力、ディスプレイのミニポート ドライバーへの呼び出しに関連付けられている*DxgkDdiOPMGetCOPPCompatibleInformation* DXGKMDT で関数を\_OPM\_GET\_サポートされている\_保護\_型のセットは、アナログ コンテンツ保護 (ACP) 型のサポートを示す必要があります (DXGKMDT\_OPM\_保護\_型\_ACP)。 その後場合、ドライバーの*DxgkDdiOPMConfigureProtectedOutput*このコネクタで ACP の種類のレベルを設定する関数は、s-ビデオの出力解像度が固定されていているために、ドライバーは成功を返す必要がありますデスクトップの解像度 (表示モード) も高くします。

-   保護されている出力がコンポーネントの出力のコネクタ、ディスプレイのミニポート ドライバーへの呼び出しを関連付けられる場合*DxgkDdiOPMGetCOPPCompatibleInformation* DXGKMDT で関数を\_OPM\_GET\_サポートされている\_保護\_型セットは、ACP 型のサポートにも指定する必要があります。 ただし場合、ドライバーの*DxgkDdiOPMConfigureProtectedOutput*ディスプレイの解像度が 720 p または 1080 i の場合は、この出力では、ACP 型のレベルを設定する関数は、ドライバーは、状態を返す必要があります\_グラフィック\_OPM\_解決\_すぎます\_高いエラー コード。 720 p または 1080 i は大きすぎるコンポーネント出力のコネクタで ACP の種類の保護レベルを設定する解像度をインストールします。

 

 





