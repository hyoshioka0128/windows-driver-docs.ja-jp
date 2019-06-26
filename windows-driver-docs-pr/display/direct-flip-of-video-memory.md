---
title: ビデオ メモリの直接の反転
description: 電力消費量を削減する最適化を特別な構成モデルの直接の反転機能を使用できます。
ms.assetid: 00A8FCB1-966A-4176-9840-7EB5BA300C8B
keywords:
- 直接の反転
- DirectFlip
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad4c2c2a319d744a82e40d20896e1ec80edbfbed
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384875"
---
# <a name="direct-flip-of-video-memory"></a>ビデオ メモリの直接の反転


電力消費量を削減する最適化を特別な構成モデルの直接の反転機能を使用できます。 最適化は、これらのシナリオを活用できます。

-   ビデオの再生と他の全画面表示のシナリオに最適な電力消費を確実には、直接フリップにより、全画面表示のコンテンツを表示し、全画面表示のアプリ、他のアプリとデスクトップの間の滑らかな遷移をことを確認するメモリ帯域幅の最小値環境。
-   ユーザーのビデオを表示または画面全体をカバーするアプリを実行したいです。 ユーザーに入るか、アプリを終了またはアプリ経由で通知が表示されます、モードの変更は不要ですと、エクスペリエンスはスムーズです。 さらに、ビデオなどの全画面表示アプリのメモリ帯域幅の要件が軽減されるため、ユーザーはモバイル デバイスの拡張のバッテリの寿命を楽しんでいます。

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
<td align="left">ドライバーの実装: 完全なグラフィック</td>
<td align="left">必須</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit" data-raw-source="[WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)">WHCK</a>要件とテスト</td>
<td align="left"><p><strong>Device.Graphics ¦ DirectFlip</strong></p></td>
</tr>
</tbody>
</table>

 

## <span id="directflip"></span><span id="DIRECTFLIP"></span>


## <a name="span-iddirectflipdevicedriverinterfaceddispanspan-iddirectflipdevicedriverinterfaceddispanspan-iddirectflipdevicedriverinterfaceddispandirectflip-device-driver-interface-ddi"></a><span id="DirectFlip_device_driver_interface__DDI_"></span><span id="directflip_device_driver_interface__ddi_"></span><span id="DIRECTFLIP_DEVICE_DRIVER_INTERFACE__DDI_"></span>DirectFlip デバイス ドライバー インターフェイス (DDI)


これらの関数と構造体は、新しい Windows 8 向けに更新されました。

-   [*CheckDirectFlipSupport*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_checkdirectflipsupport)
-   [*CheckDirectFlipSupport(D3D11\_1)* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_checkdirectflipsupport)
-   [*DxgkDdiSetVidPnSourceAddress*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff560767(v=vs.85))
-   [**D3D11\_1\_DDI\_CHECK\_DIRECT\_FLIP\_FLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ne-d3d10umddi-d3d11_1_ddi_check_direct_flip_flags)
-   [**D3DDDI\_確認\_直接\_反転\_フラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ne-d3dumddi-d3dddi_check_direct_flip_flags)
-   [**D3DDDIARG\_CHECKDIRECTFLIPSUPPORT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_checkdirectflipsupport)
-   [**D3DKMT\_DIRECTFLIP\_サポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_directflip_support)
-   [**D3DKMT\_QUERYADAPTERINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_queryadapterinfo)
-   [**D3DKMT\_WAITFORVERTICALBLANKEVENT2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_waitforverticalblankevent2)
-   [**D3DKMTWaitForVerticalBlankEvent2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtwaitforverticalblankevent2)
-   [**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)
-   [**DXGK\_SEGMENTFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_segmentflags)
-   [**DXGK\_SETVIDPNSOURCEADDRESS\_FLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_setvidpnsourceaddress_flags)

## <a name="span-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>ハードウェア認定要件


この機能を実装するときにハードウェア デバイスが満たす必要のある要件については、関連するを参照してください[WHCK ドキュメント](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)で**Device.Graphics... DirectFlip**します。

参照してください[WDDM 1.2 機能](wddm-v1-2-features.md)に Windows 8 で追加された機能の説明。

 

 





