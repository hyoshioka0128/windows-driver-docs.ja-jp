---
title: CCD DDIs
description: CCD DDIs
ms.assetid: dde0e0b0-d6d0-4ca7-ae7e-427a650c080f
keywords:
- ミニポートドライバー WDK ディスプレイ、接続、構成ディスプレイ (CCD)
- ディスプレイ (CCD) WDK ディスプレイの接続と構成
- CCD (接続と構成の表示) WDK ディスプレイ
ms.date: 10/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 03ab7e2702ffec0f4e556f5e1ae0ad4a570b137b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839815"
---
# <a name="ccd-ddis"></a>CCD DDIs


Windows 7 で導入された接続と構成の表示 (CCD) 機能により、ディスプレイデバイスのディスプレイミニポートドライバーの制御が向上しました。 

## <a name="ccd-ddis-for-display-miniport-drivers"></a>ミニポートドライバーを表示するための CCD DDIs

次の参照トピックでは、ミニポートドライバーを表示する開発者が使用できる CCD デバイスドライバーインターフェイス (DDIs) について説明します。

<span id="System-Implemented_Functions"></span><span id="system-implemented_functions"></span><span id="SYSTEM-IMPLEMENTED_FUNCTIONS"></span>**システム実装関数**  

|||
|:--|:--|
|[**DXGK\_MONITOR\_INTERFACE\_V2::p fnGetAdditionalMonitorModeSet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_monitor_getadditionalmonitormodeset)|[**DXGK\_MONITOR\_INTERFACE\_V2::p fnReleaseAdditionalMonitorModeSet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_monitor_releaseadditionalmonitormodeset)|

<span id="Driver-Implemented_Function"></span><span id="driver-implemented_function"></span><span id="DRIVER-IMPLEMENTED_FUNCTION"></span>**ドライバーによって実装された関数**

次の関数は、CCD をサポートする表示ミニポートドライバーによって実装される必要があります。

[**DxgkDdiQueryVidPnHWCapability**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryvidpnhwcapability)

<span id="Structures"></span><span id="structures"></span><span id="STRUCTURES"></span>**構成**

|||
|:--|:--|
|[**D3DKMDT\_VIDPN\_HW\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_hw_capability)|[**D3DKMDT\_VIDPN\_\_パス\_スケーリング\_サポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_scaling_support)|
|[**D3DKMT\_POLLDISPLAYCHILDREN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_polldisplaychildren)|[**D3DKMT\_RENDERFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_renderflags)|
|[**DISPLAYID\_詳細な\_タイミング\_型\_I\_縦横\_比**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_displayid_detailed_timing_type_i_aspect_ratio)|[**DXGKARG\_QUERYVIDPNHWCAPABILITY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_queryvidpnhwcapability)|
|[**DXGK\_MONITOR\_INTERFACE\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_monitor_interface_v2)|[**DXGK\_のプレゼンテーションキャップ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_presentationcaps)|
|[**DXGK\_TARGETMODE\_詳細\_タイミング**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgk_targetmode_detail_timing)||

<span id="Enumerations"></span><span id="enumerations"></span><span id="ENUMERATIONS"></span>**列挙**

|||
|:--|:--|
|[**D3DKMDT\_VIDPN\_\_パス\_スケーリング**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_vidpn_present_path_scaling)|[**DISPLAYID\_詳細な\_タイミング\_型\_I\_縦横\_比**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_displayid_detailed_timing_type_i_aspect_ratio)|
|[**DISPLAYID\_詳細な\_タイミング\_型\_\_モードのスキャン\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_displayid_detailed_timing_type_i_scanning_mode)|[**DISPLAYID\_詳細な\_タイミング\_タイプ\_I\_ステレオ\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_displayid_detailed_timing_type_i_stereo_mode)|
|[**DISPLAYID\_詳細な\_タイミング\_タイプ\_I\_同期\_極性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_displayid_detailed_timing_type_i_sync_polarity)||


ディスプレイミニポートドライバーに CCD を実装する方法の詳細については、次のトピックを参照してください。

[追加のモニターターゲットモードの取得](obtaining-additional-monitor-target-modes.md)

[縦横比とカスタムスケーリングモードの使用](using-aspect-ratio-and-custom-scaling-modes.md)

[VidPN トポロジを推奨するシステム呼び出し](system-calls-to-recommend-vidpn-topology.md)

[ACPI キーボードショートカットのロジック](acpi-keyboard-shortcut-logic.md)

[VidPN ハードウェア機能のクエリ](querying-vidpnhardware-capabilities.md)


