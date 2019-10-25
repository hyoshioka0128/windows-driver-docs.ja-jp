---
title: ステレオスコピック 3D
description: Windows 8 は、ゲームやビデオの再生などのステレオスコピック3-d シナリオ用の一貫した API およびデバイスドライバーインターフェイス (DDI) プラットフォームを提供します。
ms.assetid: 2F83E5C6-E333-4BF6-A133-C65A23DAEF62
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b95d9d73c92ba16b4b90245beba517a21851b4cc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825716"
---
# <a name="stereoscopic-3d"></a>ステレオスコピック 3D


Windows 8 は、ゲームやビデオの再生などのステレオスコピック3-d シナリオ用の一貫した API およびデバイスドライバーインターフェイス (DDI) プラットフォームを提供します。

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
<td align="left">オプション</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit" data-raw-source="[WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)">必要条件</a>とテスト</td>
<td align="left"><p><strong>ProcessingStereoscopicVideoContent のヲ</strong></p>
<p><strong>デバイス. Stereoscopic3DModes</strong></p></td>
</tr>
</tbody>
</table>

 

ステレオスコピック3-d レンダリングは、ステレオスコピックに対応しているすべてのコンポーネントが含まれるシステムでのみ有効です。 これらのコンポーネントには、3-d 対応ディスプレイハードウェア、グラフィックスハードウェア、周辺機器、およびソフトウェアアプリケーションが含まれます。 グラフィックススタックのステレオデザインは、使用されている特定の視覚エフェクトまたは表示テクノロジがオペレーティングシステムに依存しないようにするためのものです。 ディスプレイドライバーは、グラフィックスディスプレイと直接通信し、標準化された拡張表示識別データ (EDID) 構造によって表示機能に関する知識を持ちます。 ドライバーは、そのようなディスプレイがシステムに接続されていることを認識している場合にのみ、ステレオ機能を列挙します。

ディスプレイのミニポートとユーザーモードドライバーにステレオ機能を実装するには、以下の新しい DDIs または更新されたの一覧を参照してください。

ステレオスコピックの表示設定は、次に示すように、コントロールパネルの **[画面解像度]** に含まれています。

![ステレオスコピックの表示設定](images/stereo3ddisplaysetting.jpg)

[**ステレオを有効に**する] 設定は、次の状態のチェックボックスです。

-   **使用**不可 (グレー表示または非表示): ステレオでレンダリングできないシステムの場合。
-   **[有効]** (オン) に設定します。これは、ステレオで表示できるシステムの既定の設定であり、ステレオオンデマンドを意味します。 既定では、デスクトップウィンドウマネージャー (DWM) は mono モードです。 DWM は、ユーザーが (オンデマンドで) ステレオアプリを起動した場合にのみ、ステレオモードに切り替わります。 このチェックボックスがオンになっている場合は、DWM が mono モードまたはステレオモードであることに注意してください。
-   **[無効]** (オフ) に設定します。ユーザーがこの設定をオフにした場合、DWM は mono モードになります。 ステレオアプリケーションは、この場合に mono モードで表示されます。

## <a name="span-idstereoscopic_3-d_kernel-mode_supportspanspan-idstereoscopic_3-d_kernel-mode_supportspanspan-idstereoscopic_3-d_kernel-mode_supportspanstereoscopic-3-d-kernel-mode-support"></a><span id="Stereoscopic_3-D_kernel-mode_support"></span><span id="stereoscopic_3-d_kernel-mode_support"></span><span id="STEREOSCOPIC_3-D_KERNEL-MODE_SUPPORT"></span>ステレオスコピック3-d カーネルモードのサポート


これらの DDIs は、Windows 8 向けに更新され、VidPN でのステレオスコピックのレンダリングをサポートします。

-   [**D3D11DDIARG\_CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createresource)
-   [**D3DDDI\_の割り当て情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_allocationinfo)
-   [**D3DKMDT\_VIDPN\_ソース\_モード\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_vidpn_source_mode_type)
-   [**D3DKMT\_のフラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_presentflags)
-   [**DXGI\_DDI\_ARG\_\_リソース\_ID のローテーション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_arg_rotate_resource_identities)
-   [**DXGK\_のフラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_presentflags)
-   [**DXGK\_SETVIDPNSOURCEADDRESS\_フラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_setvidpnsourceaddress_flags)
-   [**DXGKARG\_OPENALLOCATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_openallocation)

## <a name="span-idstereoscopic_3-d_swapchain_ddisspanspan-idstereoscopic_3-d_swapchain_ddisspanspan-idstereoscopic_3-d_swapchain_ddisspanstereoscopic-3-d-swapchain-ddis"></a><span id="Stereoscopic_3-D_swapchain_DDIs"></span><span id="stereoscopic_3-d_swapchain_ddis"></span><span id="STEREOSCOPIC_3-D_SWAPCHAIN_DDIS"></span>ステレオスコピック3-d スワップチェーン DDIs


これらの DDIs は、Windows 8 でステレオスコピック swapswapチェーンをサポートするために新しく追加または更新されました。

-   [*BltDXGI*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)
-   [*Blt1DXGI*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions)
-   [*CreateResource (D3D10)* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource)
-   [*CreateResource (D3D11)* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource)
-   [*RotateResourceIdentitiesDXGI*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)
-   [**D3DDDI\_の割り当て情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_allocationinfo)
-   [**D3D10DDIARG\_CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createresource)
-   [**D3D11DDIARG\_CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createresource)
-   [**DXGI\_DDI\_ARG\_\_リソース\_ID のローテーション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_arg_rotate_resource_identities)
-   [**DXGI\_DDI\_\_フラグを表示します**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_present_flags)
-   [**DXGI\_DDI\_プライマリ\_DESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_primary_desc)

## <a name="span-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>ハードウェア認定の要件


システムビルダーでは、適切な機能を確保するために、上記の設定を使用して、ステレオドライバーパッケージをテストすることをお勧めします。

ステレオ3-d 機能は、Microsoft DirectX 10 対応ハードウェア以上でのみ有効にすることができます。 ただし、Microsoft Direct3D 11 Api は DirectX 1.x および 10 .x ハードウェアで動作するため、すべての WDDM 1.2 ドライバーは Direct3D 11 をサポートし、完全にテストして、Direct3D 11APIs がすべての Windows 8 ハードウェアで動作するようにする必要があります。

ステレオスコピック3-d はオプションの WDDM 1.2 機能ですが、すべての Windows 8 ハードウェアで Direct3D 11 API をサポートする必要があります。 そのため、WDDM 1.2 ドライバー (完全なグラフィックスおよびレンダーデバイス) は、テクスチャ配列のプロセス間共有のサポートを追加することによって、Direct3D 11 Api をサポートする必要があります。 この要件は、ステレオアプリに mono モードでエラーが発生しないようにするためです。

ハードウェアデバイスがこの機能を実装するときに満たす必要がある要件の詳細については、デバイスに関連する[Whck のドキュメント](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)を参照してください **。グラフィックの参照処理のビデオコンテンツ**と**ステレオスコピック3D モードを表示**します。

Windows 8 で追加された機能の確認については、「 [WDDM 1.2 の機能](wddm-v1-2-features.md)」を参照してください。

 

 





