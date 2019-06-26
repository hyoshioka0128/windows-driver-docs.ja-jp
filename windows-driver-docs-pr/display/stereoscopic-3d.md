---
title: ステレオスコピック 3D
description: Windows 8 では、ゲームやビデオの再生などのステレオスコ ピック 3-D シナリオの一貫性のある API とデバイスのドライバー インターフェイス (DDI) プラットフォームを提供します。
ms.assetid: 2F83E5C6-E333-4BF6-A133-C65A23DAEF62
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 715a46065d20246bcd534749e35d04f881f8fa05
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363690"
---
# <a name="stereoscopic-3d"></a>ステレオスコピック 3D


Windows 8 では、ゲームやビデオの再生などのステレオスコ ピック 3-D シナリオの一貫性のある API とデバイスのドライバー インターフェイス (DDI) プラットフォームを提供します。

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
<td align="left">省略可能</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit" data-raw-source="[WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)">WHCK</a>要件とテスト</td>
<td align="left"><p><strong>Device.Graphics... ProcessingStereoscopicVideoContent</strong></p>
<p><strong>Device.Display.Monitor.Stereoscopic3DModes</strong></p></td>
</tr>
</tbody>
</table>

 

ステレオスコ ピック 3-D レンダリングがステレオスコ ピックがすべてのコンポーネントを持つシステムでのみ有効に 3 D 対応します。 これらのコンポーネントには、3 D 対応ディスプレイ ハードウェア、ハードウェアのグラフィックス、周辺機器、およびソフトウェア アプリケーションが含まれます。 グラフィックス スタックのステレオの設計では、特定の視覚エフェクトまたは使用される表示テクノロジは、オペレーティング システムに依存しません。 ディスプレイ ドライバーは、グラフィック表示に直接通信し、拡張表示 Identification Data (EDID) 構造を標準化されたディスプレイの機能に関する知識を備えています。 ドライバーは、このような画面がシステムに接続されていることを認識している場合にのみ、ステレオの機能を列挙します。

ディスプレイとユーザー モードのミニポート ドライバーでは、ステレオの機能を実装するには、新しいまたは更新された Ddi 以下の一覧を参照してください。

ステレオスコ ピック ディスプレイの設定の一部である、**画面の解像度**コントロール パネル で、次のようにします。

![ステレオスコ ピック ディスプレイの設定](images/stereo3ddisplaysetting.jpg)

**ステレオを有効にする**設定は、次の状態のチェック ボックス。

-   **使用できない**(淡色表示または非表示)。非対応のステレオでのレンダリング システムが表示されます。
-   設定**有効**(オン)。ステレオ ディスプレイでレンダリングできるシステムの既定の設定は、このステレオ オンデマンドのことを意味します。 既定では、デスクトップ ウィンドウ マネージャー (DWM) は、mono のモードです。 ステレオ アプリ場合にのみ、ステレオのモードに切り替えます。 DWM は、ユーザー (オンデマンド) によって起動されます。 DWM は、このチェック ボックスをオンにすると mono またはステレオのいずれかのモードであることができますに注意してください。
-   設定**無効**(オフ)。DWM は、ある場合、ユーザーは mono モードではオフこの設定します。 ステレオ アプリケーションは、ここで mono のモードに存在します。

## <a name="span-idstereoscopic3-dkernel-modesupportspanspan-idstereoscopic3-dkernel-modesupportspanspan-idstereoscopic3-dkernel-modesupportspanstereoscopic-3-d-kernel-mode-support"></a><span id="Stereoscopic_3-D_kernel-mode_support"></span><span id="stereoscopic_3-d_kernel-mode_support"></span><span id="STEREOSCOPIC_3-D_KERNEL-MODE_SUPPORT"></span>ステレオスコ ピック 3d のカーネル モードのサポート


VidPN ステレオスコ ピック 3-D レンダリングをサポートするために Windows 8 のこれら Ddi が更新されます。

-   [**D3D11DDIARG\_CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createresource)
-   [**D3DDDI\_ALLOCATIONINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddi_allocationinfo)
-   [**D3DKMDT\_VIDPN\_SOURCE\_MODE\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ne-d3dkmdt-_d3dkmdt_vidpn_source_mode_type)
-   [**D3DKMT\_PRESENTFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_presentflags)
-   [**DXGI\_DDI\_ARG\_ROTATE\_RESOURCE\_IDENTITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_arg_rotate_resource_identities)
-   [**DXGK\_PRESENTFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_presentflags)
-   [**DXGK\_SETVIDPNSOURCEADDRESS\_FLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_setvidpnsourceaddress_flags)
-   [**DXGKARG\_OPENALLOCATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_openallocation)

## <a name="span-idstereoscopic3-dswapchainddisspanspan-idstereoscopic3-dswapchainddisspanspan-idstereoscopic3-dswapchainddisspanstereoscopic-3-d-swapchain-ddis"></a><span id="Stereoscopic_3-D_swapchain_DDIs"></span><span id="stereoscopic_3-d_swapchain_ddis"></span><span id="STEREOSCOPIC_3-D_SWAPCHAIN_DDIS"></span>ステレオスコ ピック 3-D スワップ Ddi


これらの Ddi は、新しいステレオスコ ピック 3-D スワップをサポートするために Windows 8 向けに更新されました。

-   [*BltDXGI*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)
-   [*Blt1DXGI*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions)
-   [*CreateResource(D3D10)* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource)
-   [*CreateResource(D3D11)* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource)
-   [*RotateResourceIdentitiesDXGI*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)
-   [**D3DDDI\_ALLOCATIONINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddi_allocationinfo)
-   [**D3D10DDIARG\_CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createresource)
-   [**D3D11DDIARG\_CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createresource)
-   [**DXGI\_DDI\_ARG\_ROTATE\_RESOURCE\_IDENTITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_arg_rotate_resource_identities)
-   [**DXGI\_DDI\_存在\_フラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_present_flags)
-   [**DXGI\_DDI\_プライマリ\_DESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_primary_desc)

## <a name="span-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>ハードウェア認定要件


システム ビルダーは、正しく機能するために、上記の設定を使用して、ステレオのドライバー パッケージをテストすることが推奨されます。

Microsoft DirectX 10 対応するハードウェアでのみ以降、ステレオの 3-D 機能を有効にできます。 ただし、Microsoft direct3d11 の Api は、DirectX 9.x と 10.x ハードウェアで動作、および WDDM 1.2 ドライバーをすべて direct3d11 をサポートする必要があります、Direct3D 11APIs がすべての Windows 8 ハードウェアで動作できるようにする完全にテストします。

ステレオスコ ピック 3-D オプションおよび WDDM 1.2 機能は、すべての Windows 8 ハードウェアで direct3d11 API のサポートが必要です。 したがって、WDDM 1.2 ドライバー (完全なグラフィックスとレンダリング デバイス) では、テクスチャ配列のプロセス間を共有するためのサポートを追加して direct3d11 の Api をサポートする必要があります。 この要件は、ステレオのアプリが mono のモードでの障害を持っていないことを確認します。

この機能を実装するときにハードウェア デバイスが満たす必要のある要件の詳細については、関連するを参照してください[WHCK ドキュメント](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)で**Device.Graphics... 処理ステレオスコ ピック ビデオ コンテンツ** **Device.Display.Monitor.Stereoscopic 3D モード**します。

参照してください[WDDM 1.2 機能](wddm-v1-2-features.md)に Windows 8 で追加された機能の説明。

 

 





