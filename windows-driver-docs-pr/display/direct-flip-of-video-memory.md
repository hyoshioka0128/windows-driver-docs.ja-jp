---
title: ビデオメモリの直接フリップ
description: 直接フリップ機能を使用すると、コンポジションモデルに特別な最適化を行い、電力消費を減らすことができます。
ms.assetid: 00A8FCB1-966A-4176-9840-7EB5BA300C8B
keywords:
- 直接フリップ
- DirectFlip
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7ac411bda8ea878fede52524d61a4ef849a3a34
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839013"
---
# <a name="direct-flip-of-video-memory"></a>ビデオメモリの直接フリップ


直接フリップ機能を使用すると、コンポジションモデルに特別な最適化を行い、電力消費を減らすことができます。 最適化には、次のようなシナリオがあります。

-   ビデオの再生とその他の全画面のシナリオで最適な電力消費を確保するために、ダイレクトフリップを使用すると、最小限のメモリ帯域幅で全画面表示のコンテンツを表示し、全画面アプリ、他のアプリ、およびデスクトップの間でスムーズな移行を行うことができます。environment.
-   ユーザーは、ビデオを表示したり、画面全体をカバーするアプリを実行したりする必要があります。 ユーザーがアプリを入力または終了したとき、またはアプリに通知が表示された場合、モードの変更は不要で、エクスペリエンスはスムーズです。 さらに、ユーザーはモバイルデバイスのバッテリ寿命を延ばすことができます。これは、ビデオなどの全画面アプリでメモリ帯域幅の要件が減るためです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">Windows Display Driver Model (WDDM) の最小バージョン</td>
<td align="left">1.2</td>
</tr>
<tr class="even">
<td align="left">Windows の最小バージョン</td>
<td align="left">8</td>
</tr>
<tr class="odd">
<td align="left">ドライバーの実装—完全なグラフィックス</td>
<td align="left">必須</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit" data-raw-source="[WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)">必要条件</a>とテスト</td>
<td align="left"><p><strong>デバイスのグラフィックのヲ</strong></p></td>
</tr>
</tbody>
</table>

 

## <span id="directflip"></span><span id="DIRECTFLIP"></span>


## <a name="span-iddirectflip_device_driver_interface__ddi_spanspan-iddirectflip_device_driver_interface__ddi_spanspan-iddirectflip_device_driver_interface__ddi_spandirectflip-device-driver-interface-ddi"></a><span id="DirectFlip_device_driver_interface__DDI_"></span><span id="directflip_device_driver_interface__ddi_"></span><span id="DIRECTFLIP_DEVICE_DRIVER_INTERFACE__DDI_"></span>DirectFlip device driver interface (DDI)


Windows 8 では、次の関数と構造が新しく追加または更新されています。

-   [*CheckDirectFlipSupport*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_checkdirectflipsupport)
-   [*CheckDirectFlipSupport (D3D11\_1)* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_checkdirectflipsupport)
-   [*DxgkDdiSetVidPnSourceAddress*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff560767(v=vs.85))
-   [**D3D11\_1\_DDI\_\_直接\_フリップ\_フラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1_ddi_check_direct_flip_flags)
-   [**D3DDDI\_CHECK\_直接\_フリップ\_フラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-d3dddi_check_direct_flip_flags)
-   [**D3DDDIARG\_CHECKDIRECTFLIPSUPPORT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_checkdirectflipsupport)
-   [**D3DKMT\_DIRECTFLIP\_サポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_directflip_support)
-   [**D3DKMT\_QUERYADAPTERINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_queryadapterinfo)
-   [**D3DKMT\_WAITFORVERTICALBLANKEVENT2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_waitforverticalblankevent2)
-   [**D3DKMTWaitForVerticalBlankEvent2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtwaitforverticalblankevent2)
-   [**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)
-   [**DXGK\_SEGMENTFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentflags)
-   [**DXGK\_SETVIDPNSOURCEADDRESS\_フラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_setvidpnsourceaddress_flags)

## <a name="span-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>ハードウェア認定の要件


ハードウェアデバイスがこの機能を実装するときに満たす必要がある要件の詳細については、デバイス上の関連する[whck ドキュメント](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)を参照してください **。**

Windows 8 で追加された機能の確認については、「 [WDDM 1.2 の機能](wddm-v1-2-features.md)」を参照してください。

 

 





