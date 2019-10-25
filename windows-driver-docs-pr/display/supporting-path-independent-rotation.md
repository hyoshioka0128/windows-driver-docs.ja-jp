---
title: パスに依存しない回転のサポート
description: Windows 8.1 更新プログラム以降、オペレーティングシステムでは、縦方向の表示の複製がサポートされており、最も多くの解像度が表示されます。
ms.assetid: 136CEDA5-2839-4E6E-A032-1A9222C769C6
ms.date: 10/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8943554eb1bbae99acffbc0f814a16cebe0017e5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829384"
---
# <a name="span-iddisplaysupporting_path-independent_rotationspansupporting-path-independent-rotation"></a><span id="display.supporting_path-independent_rotation"></span>パスに依存しないローテーションのサポート


Windows 8.1 更新プログラム以降、オペレーティングシステムでは、縦方向の表示の複製がサポートされており、最も多くの解像度が表示されます。 表示ミニポートドライバーでは、 [**D3DKMDT\_VIDPN\_存在\_パス\_\_ローテーション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_rotation_support)の適切なオフセット値を設定する必要があります。これは、*プライマリ複製パス*と*セカンダリ複製パス*のサポート構造で、次のようになります。「[ディスプレイミニポートドライバーでの回転のサポート](supporting-rotation-in-a-display-miniport-driver.md)」で説明されています。

これらのデバイスドライバーインターフェイス (DDIs) は Windows 8.1 更新プログラムで新しく追加されたものです。

-   D3DKMDT_VPPR_GET_CONTENT_ROTATION
-   D3DKMDT_VPPR_GET_CONTENT_ROTATION_PART
-   D3DKMDT_VPPR_GET_OFFSET_ROTATION

これらの DDIs は Windows 8.1 Update で更新されます。

-   [**D3DKMDT\_VIDPN\_\_パス\_ローテーション\_サポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_rotation_support)

-   [**D3DKMDT\_VIDPN\_存在\_パス\_ローテーション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_vidpn_present_path_rotation)

## <a name="span-idcloning_a_portrait-first_devicespanspan-idcloning_a_portrait-first_devicespanspan-idcloning_a_portrait-first_devicespancloning-a-portrait-first-device"></a><span id="Cloning_a_portrait-first_device"></span><span id="cloning_a_portrait-first_device"></span><span id="CLONING_A_PORTRAIT-FIRST_DEVICE"></span>縦優先デバイスの複製


縦優先のデバイスのドライバーが横向きのモニターに複製するように要求された場合、プライマリ複製パスの解像度に一致するソースモード (*x*、*y*) の解像度をレポートする必要があります。 次に、セカンダリ複製パスで90と270度のオフセット値 ([**D3DKMDT\_VIDPN\_\_パス\_ローテーション\_サポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_rotation_support)をサポートします。**Offset90**または。**Offset270**は**TRUE**)。 そのため、 [**D3DKMDT\_vidpn\_使用して、\_パス\_ローテーション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_vidpn_present_path_rotation)列挙値が90または270°のオフセットを示すように vidpn をコミットすると、(*x*,*y*) の解像度が反転されます。特定のパス。

既定では、オペレーティングシステムは、内部表示パネルとしてセカンダリ複製パスを選択します。 内部パネルが縦優先の場合、オペレーティングシステムでは、 [**D3DKMDT\_VIDPN\_\_パス\_ローテーション\_サポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_rotation_support)が必要です。**Offset270**は、横モードで内部表示パネルに表示するために、このパスに設定されます。 セカンダリ複製パスに横向きの外部モニターがある場合、オペレーティングシステムは、 **\_パス\_ローテーション\_サポート**するために、ドライバーが D3DKMDT\_VIDPN\_サポートすることを前提としています。**Offset90**ですが、これはまれなシナリオである可能性があります。

## <a name="span-idexample_clone_scenariosspanspan-idexample_clone_scenariosspanspan-idexample_clone_scenariosspanexample-clone-scenarios"></a><span id="Example_clone_scenarios"></span><span id="example_clone_scenarios"></span><span id="EXAMPLE_CLONE_SCENARIOS"></span>複製のシナリオ例


ここでは、ネイティブの解像度が 800 (幅) x 1280 ピクセル (高さ) の縦向きのデバイスが複製モードで、高さが1080ピクセルの横向き (横向き) のテレビに接続されている一般的なシナリオを示します。 この情報は、ドライバーによってオペレーティングシステムに報告されます。

<span id="source_mode"></span><span id="SOURCE_MODE"></span>ソースモード  
1280 x 800

<span id="TV_target_mode"></span><span id="tv_target_mode"></span><span id="TV_TARGET_MODE"></span>TV ターゲットモード  
1920 x 1080 (縦横比で保持されるスケーリング)

<span id="device_target_mode"></span><span id="DEVICE_TARGET_MODE"></span>デバイスターゲットモード  
800 x 1280 (id のスケーリング)

<span id="primary_clone_path__TV_"></span><span id="primary_clone_path__tv_"></span><span id="PRIMARY_CLONE_PATH__TV_"></span>プライマリ複製パス (テレビ)  
ドライバーでサポートされているのは、 [**D3DKMDT\_VIDPN\_存在\_パス\_ローテーション\_サポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_rotation_support)のみです。**Offset0**、および通常のローテーションサポート

<span id="secondary_clone_path__device_"></span><span id="SECONDARY_CLONE_PATH__DEVICE_"></span>セカンダリ複製パス (デバイス)  
ドライバーでサポートされているのは、 [**D3DKMDT\_VIDPN\_存在\_パス\_ローテーション\_サポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_rotation_support)のみです。**Offset270**、および通常のローテーションサポート

<span></span>  

次に、 [*DxgkDdiCommitVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_commitvidpn)関数への呼び出しによって、 [**D3DKMDT\_VIDPN\_存在\_パス\_ローテーション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_vidpn_present_path_rotation)列挙型のパス設定と共にが返されます。

<span id="primary_clone_path__TV_"></span><span id="primary_clone_path__tv_"></span><span id="PRIMARY_CLONE_PATH__TV_"></span>プライマリ複製パス (テレビ)  
**D3DKMDT\_VPPR\_ID**

<span id="secondary_clone_path__device_"></span><span id="SECONDARY_CLONE_PATH__DEVICE_"></span>セカンダリ複製パス (デバイス)  
**D3DKMDT\_VPPR\_ID\_OFFSET270**

オペレーティングシステムは、指定されたコンテンツを270度回転させるようにドライバーに要求します。

コントロールパネルの [**画面**の**向き**] ドロップダウンボックスで [**横] (反転)** オプションを選択した場合、 [*DxgkDdiCommitVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_commitvidpn)関数の呼び出しは、D3DKMDT からのこれらのパス設定と共に返され[ **\_VIDPN\_\_パス\_ローテーション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_vidpn_present_path_rotation)列挙体が存在します。

<span id="primary_clone_path__TV_"></span><span id="primary_clone_path__tv_"></span><span id="PRIMARY_CLONE_PATH__TV_"></span>プライマリ複製パス (テレビ)  
**D3DKMDT\_VPPR\_ROTATE180**

<span id="secondary_clone_path__device_"></span><span id="SECONDARY_CLONE_PATH__DEVICE_"></span>セカンダリ複製パス (デバイス)  
**D3DKMDT\_VPPR\_ROTATE180\_OFFSET270**

デスクトップウィンドウマネージャー (DWM) で既にコンテンツ180°がローテーションされている場合でも、ドライバーはセカンダリ複製パスで別の270度回転する必要があります。 それ以外の場合、ドライバーは、デバイスの TV と90度のコンテンツを180°回転させる必要があります。 コンテンツを回転させるには、ドライバーで[**DXGK\_のフラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_presentflags)構造体の**回転**メンバーを設定する必要があることに注意してください。

 

 





