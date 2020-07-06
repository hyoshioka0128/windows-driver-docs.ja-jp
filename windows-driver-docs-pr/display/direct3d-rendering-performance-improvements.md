---
title: Direct3D レンダリングのパフォーマンスの向上
description: Windows Display Driver Model (WDDM) 1.3 以降のドライバーでは、Microsoft Direct3D レンダリングのパフォーマンスを向上させることができます。これにより、Direct3D 9 ハードウェアはハードウェアコマンドバッファーとカウンターをより適切に使用し、サブリソースに対して効率的にシステムメモリをコピーできるようになります。 これらの機能は、Direct3D バージョン10ハードウェアで使用できる一部の機能を反映していますが、Windows 8.1 以降の新機能です。
ms.assetid: F9AAE489-EC45-4EE6-875E-E084BB3054EE
ms.date: 10/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9b7253019244c327c3ee85a3de88c5c27c7956ad
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968349"
---
# <a name="direct3d-rendering-performance-improvements"></a>Direct3D レンダリングのパフォーマンスの向上


Windows Display Driver Model (WDDM) 1.3 以降のドライバーでは、Microsoft Direct3D レンダリングのパフォーマンスを向上させることができます。これにより、Direct3D 9 ハードウェアはハードウェアコマンドバッファーとカウンターをより適切に使用し、サブリソースに対して効率的にシステムメモリをコピーできるようになります。 これらの機能は、Direct3D バージョン10ハードウェアで使用できる一部の機能を反映していますが、Windows 8.1 以降の新機能です。

新しい Direct3D 11.1 リソースのトリミングとマップの既定のパフォーマンスの向上も利用できます。 マップの既定のシナリオについては、以下の「動作の変更」セクションで説明します。

## <a name="span-idrendering_performance_referencespanspan-idrendering_performance_referencespanspan-idrendering_performance_referencespanrendering-performance-reference"></a><span id="Rendering_performance_reference"></span><span id="rendering_performance_reference"></span><span id="RENDERING_PERFORMANCE_REFERENCE"></span>レンダリングパフォーマンスのリファレンス


このリファレンスセクションでは、ユーザーモードのデバイスドライバーインターフェイス (DDIs) について説明します。

### <a name="direct3d-rendering-performance-functions-implemented-by-the-user-mode-driver"></a>ユーザーモードドライバーによって実装される Direct3D レンダリングパフォーマンス関数

このセクションには、Microsoft Direct3D のレンダリングパフォーマンスの向上をサポートするために、Windows Display Driver Model (WDDM) 1.3 以降のユーザーモード表示ドライバーが実装する関数が含まれています。


**[PFND3DDDI_FLUSH1](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_flush1)**: [PFND3DDDI_CHECKCOUNTERINFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_checkcounterinfo)

**[PFND3DDDI_CHECKCOUNTER](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_checkcounter)**: [PFND3DDDI_UPDATESUBRESOURCEUP](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_updatesubresourceup)


### <a name="direct3d-rendering-performance-structures-and-enumerations"></a>Direct3D レンダリングのパフォーマンス構造と列挙体

これらのユーザーモード構造体と列挙型では、レンダリングのパフォーマンスが向上し、Windows 8.1 が新しく追加または更新されています。 すべては、 [**D3D11 \_ 1 \_ DDI \_ フラッシュ \_ フラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1_ddi_flush_flags)を除く、Direct3D Level 9 ドライバーに適用されます。

-   [**D3DDDI \_フラッシュ \_ フラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-d3dddi_flush_flags)(新規)
-   [**D3DDDIARG \_COPYFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-d3dddiarg_copyflags) (新規)
-   [**D3DDDIARG \_カウンター \_ 情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-d3dddiarg_counter_info)(新規)
-   [**D3DDDIARG \_UPDATESUBRESOURCEUP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-d3dddiarg_updatesubresourceup) (新規)
-   [**D3DDDICAPS \_単純 \_ な \_ インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-d3dddicaps_simple_instancing_support)化のサポート (新規)
-   [*CreateResource2*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource2) ( **CaptureBuffer**フラグ値が設定されている場合、1.3 以降の Direct3D Level 9 ドライバーは、 **E \_ invalidarg**エラーコードを返す必要があります)
-   [**D3D11 \_ 1 \_ DDI \_ フラッシュ \_ フラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1_ddi_flush_flags)(**D3DWDDM1 \_ 3ddi \_ TRIM \_ メモリ**定数が追加されました)
-   [**D3DDDI \_DEVICEFUNCS 関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_devicefuncs)(**pfnFlush1**、 **pfncheckcounterinfo**、 **pfncheckcounter**、 **pfnUpdateSubresourceUP** members の追加)
-   [**D3DDDI \_プール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ne-d3dukmdt-_d3dddi_pool)(**D3DDDIPOOL \_ STAGINGMEM**定数の追加)
-   [**D3DDDICAPS \_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_d3dddicaps_type)(**D3DDDICAPS \_ GET \_ SIMPLE \_ の \_ インスタンス**化のサポート定数が追加されました)
-   [*Getcaps*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps) (解説の新しい情報)

## <a name="span-idddi_implementation_requirements_starting_with_wddm_13spanspan-idddi_implementation_requirements_starting_with_wddm_13spanddi-implementation-requirements-starting-with-wddm-13"></a><span id="ddi_implementation_requirements_starting_with_wddm_1.3"></span><span id="DDI_IMPLEMENTATION_REQUIREMENTS_STARTING_WITH_WDDM_1.3"></span>WDDM 1.3 以降の DDI 実装要件


WDDM 1.3 以降では、ユーザーモードドライバーを実装するために、次の関数が必須または省略可能です。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数グループ</th>
<th align="left">[説明]</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="_9_functions_that_are_optional_prior_to__1.3._Now_required_"></span><span id="_9_functions_that_are_optional_prior_to__1.3._now_required_"></span><span id="_9_FUNCTIONS_THAT_ARE_OPTIONAL_PRIOR_TO__1.3._NOW_REQUIRED_"></span>WDDM 1.3 より前のオプションである Direct3D 9 関数。 必須:</p></td>
<td align="left"><ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_bufblt1" data-raw-source="[&lt;em&gt;BufBlt1&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_bufblt1)"><em>BufBlt1</em></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource2" data-raw-source="[&lt;em&gt;CreateResource2&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource2)"><em>CreateResource2</em></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_texblt1" data-raw-source="[&lt;em&gt;TexBlt1&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_texblt1)"><em>TexBlt1</em></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_volblt1" data-raw-source="[&lt;em&gt;VolBlt1&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_volblt1)"><em>VolBlt1</em></a></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><span id="_9_functions_that_are_available_starting_with__1.3._A_driver_must_either_implement_all_of_these_functions_or_none_of_them_"></span><span id="_9_functions_that_are_available_starting_with__1.3._a_driver_must_either_implement_all_of_these_functions_or_none_of_them_"></span><span id="_9_FUNCTIONS_THAT_ARE_AVAILABLE_STARTING_WITH__1.3._A_DRIVER_MUST_EITHER_IMPLEMENT_ALL_OF_THESE_FUNCTIONS_OR_NONE_OF_THEM_"></span>WDDM 1.3 以降で使用可能な Direct3D 9 関数。 ドライバーは、これらの関数のすべてを実装するか、いずれも実装しないようにする必要があります。</p></td>
<td align="left"><ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_checkcounter" data-raw-source="[&lt;em&gt;pfnCheckCounter&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_checkcounter)"><em>pfnCheckCounter</em></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_checkcounterinfo" data-raw-source="[&lt;em&gt;pfnCheckCounterInfo&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_checkcounterinfo)"><em>pfnCheckCounterInfo</em></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_flush1" data-raw-source="[&lt;em&gt;pfnFlush1&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_flush1)"><em>pfnFlush1</em></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_present1" data-raw-source="[&lt;em&gt;pfnPresent1(D3D)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_present1)"><em>pfnPresent1 (D3D)</em></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_3_ddi_base_functions" data-raw-source="[&lt;em&gt;pfnPresent1(DXGI)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_3_ddi_base_functions)"><em>pfnPresent1 (DXGI)</em></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_updatesubresourceup" data-raw-source="[&lt;em&gt;pfnUpdateSubresourceUP&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_updatesubresourceup)"><em>pfnUpdateSubresourceUP</em></a></li>
<li>pfnSetMarker</li>
<li>pfnSetMarkerMode</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="When_the__1.3_and_later_optional_functions_immediately_above_are_implemented__these_functions_have_associated_behavior_changes_"></span><span id="when_the__1.3_and_later_optional_functions_immediately_above_are_implemented__these_functions_have_associated_behavior_changes_"></span><span id="WHEN_THE__1.3_AND_LATER_OPTIONAL_FUNCTIONS_IMMEDIATELY_ABOVE_ARE_IMPLEMENTED__THESE_FUNCTIONS_HAVE_ASSOCIATED_BEHAVIOR_CHANGES_"></span>上記の WDDM 1.3 以降のオプションの関数が実装されている場合、これらの関数には動作の変更が関連付けられています。</p></td>
<td align="left"><ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions" data-raw-source="[&lt;em&gt;BltDXGI&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)"><em>Bltdxgi</em></a> —ネイティブステージング</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions" data-raw-source="[&lt;em&gt;Blt1DXGI&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions)"><em>Blt1DXGI</em></a> —ネイティブステージング</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource2" data-raw-source="[&lt;em&gt;CreateResource2&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource2)"><em>CreateResource2</em></a> —ネイティブステージング、大規模なキャプチャテクスチャ</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps" data-raw-source="[&lt;em&gt;GetCaps&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)"><em>Getcaps</em></a> : タイムスタンプ、単純なインスタンス化</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lock" data-raw-source="[&lt;em&gt;Lock&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lock)"><em>ロック</em></a>—ネイティブステージング</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_texblt1" data-raw-source="[&lt;em&gt;TexBlt1&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_texblt1)"><em>TexBlt1</em></a> —ネイティブステージング</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_unlock" data-raw-source="[&lt;em&gt;Unlock&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_unlock)"><em>ロック解除</em></a>—ネイティブステージング</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_volblt1" data-raw-source="[&lt;em&gt;VolBlt1&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_volblt1)"><em>VolBlt1</em></a> —ネイティブステージング</li>
</ul>
<p>これらのシナリオは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps" data-raw-source="[&lt;em&gt;GetCaps&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)"><em>Getcaps</em></a>が呼び出される場合に適用されます。</p>
<ul>
<li><strong>D3DDDICAPS_GETD3DQUERYDATA</strong>が設定されている場合、ドライバーは必要に応じてタイムスタンプのサポートを報告できます。つまり、Direct3D ランタイムはサポートをマスクしません。</li>
<li><strong>D3DDDICAPS_GET_SIMPLE_INSTANCING_SUPPORT</strong>が設定されている場合、ドライバーは、インスタンス化のオプションのハードウェアサポートを報告できます。</li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><span id="These__11_functions_have_associated_behavior_changes_"></span><span id="these__11_functions_have_associated_behavior_changes_"></span><span id="THESE__11_FUNCTIONS_HAVE_ASSOCIATED_BEHAVIOR_CHANGES_"></span>これらの Direct3D 11 関数には、動作の変更が関連付けられています。</p></td>
<td align="left"><ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource" data-raw-source="[&lt;em&gt;CreateResource(D3D11)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource)"><em>Createresource (D3D11)</em></a> -バッファーマップの既定値 (以下の「動作の変更」セクションを参照してください)</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_flush1" data-raw-source="[&lt;em&gt;pfnFlush1&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_flush1)"><em>pfnFlush1</em></a> —リソースのトリム</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourcemap" data-raw-source="[&lt;em&gt;ResourceMap&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourcemap)"><em>Resourcemap</em></a> —バッファーマップの既定値 (以下の「動作の変更」セクションを参照してください)</li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourceunmap" data-raw-source="[&lt;em&gt;ResourceUnmap&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourceunmap)"><em>Resourceunmap</em></a> -バッファーマップの既定値 (以下の「動作の変更」セクションを参照してください)</li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="span-id_behavior_spanspan-id_behavior_spanbehavior-changes-for-calls-to-resource-create-map-and-unmap-functions"></a><span id="_behavior_"></span><span id="_BEHAVIOR_"></span>Resource create、map、およびマップ解除関数の呼び出しの動作変更


WDDM 1.3 以降のドライバーによって実装されるこれらの関数の場合、Direct3D ランタイムはマップの既定のシナリオに対して制限された入力値のセットを提供します。 これらの制限値は、機能レベル11.1 以降をサポートするドライバーにのみ適用されます。

[***Createresource (D3D11)***](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource) **関数**-

これらの入力[**D3D11DDIARG \_ createresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createresource)構造体のメンバーは、次のように制限されています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">メンバー</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="ResourceDimension_and_Usage"></span><span id="resourcedimension_and_usage"></span><span id="RESOURCEDIMENSION_AND_USAGE"></span><strong>Resourcedimension</strong>と<strong>Usage</strong></p></td>
<td align="left"><p>これらの動作変更が適用さ<strong>れるのは</strong>、Direct3D ランタイムが<strong>resourcedimension</strong>と type <strong>D3D10_DDI_USAGE_DEFAULT</strong>の型<strong>D3D10DDIRESOURCE_BUFFER</strong>を指定した場合のみです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="BindFlags"></span><span id="bindflags"></span><span id="BINDFLAGS"></span><strong>BindFlags</strong></p></td>
<td align="left"><p>Direct3D ランタイムは、 <strong>D3D10_DDI_BIND_SHADER_RESOURCE</strong>と<strong>D3D11_DDI_BIND_UNORDERED_ACCESS</strong>の値のみを設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="MapFlags"></span><span id="mapflags"></span><span id="MAPFLAGS"></span><strong>MapFlags</strong></p></td>
<td align="left"><p>ここに記載されている他のすべてのメンバー要件が満たされている場合、ランタイムは<strong>D3D10_DDI_MAP_READ</strong>、 <strong>D3D10_DDI_MAP_WRITE</strong>、および<strong>D3D10_DDI_MAP_READWRITE</strong>の値を設定できます。 ドライバーは、これらの値をサポートしている必要があります。 <strong>D3D10_DDI_MAP_WRITE_DISCARD</strong>と<strong>D3D10_DDI_MAP_WRITE_NOOVERWRITE</strong>の値が無効です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="MiscFlags"></span><span id="miscflags"></span><span id="MISCFLAGS"></span><strong>MiscFlags</strong></p></td>
<td align="left"><p>ランタイムは、 <strong>D3D11_DDI_RESOURCE_MISC_BUFFER_ALLOW_RAW_VIEWS</strong>と<strong>D3D11_DDI_RESOURCE_MISC_BUFFER_STRUCTURED</strong>の値のみを設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Format"></span><span id="format"></span><span id="FORMAT"></span><strong>形式</strong></p></td>
<td align="left"><p>ランタイムは、 <strong>DXGI_FORMAT_UNKNOWN</strong>値のみを設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="SampleDesc"></span><span id="sampledesc"></span><span id="SAMPLEDESC"></span><strong>SampleDesc</strong></p></td>
<td align="left"><p>ランタイムは、 <a href="https://docs.microsoft.com/windows/desktop/api/dxgicommon/ns-dxgicommon-dxgi_sample_desc" data-raw-source="[&lt;strong&gt;DXGI_SAMPLE_DESC&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/dxgicommon/ns-dxgicommon-dxgi_sample_desc)"><strong>DXGI_SAMPLE_DESC</strong></a>を設定します。<strong>メンバーを</strong>1 に、<strong>品質</strong>メンバーを0にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="MipLevels"></span><span id="miplevels"></span><span id="MIPLEVELS"></span><strong>MipLevels</strong></p></td>
<td align="left"><p>ランタイムは、値を1に設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="ArraySize"></span><span id="arraysize"></span><span id="ARRAYSIZE"></span><strong>ArraySize</strong></p></td>
<td align="left"><p>ランタイムは、値を1に設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="pPrimaryDesc"></span><span id="pprimarydesc"></span><span id="PPRIMARYDESC"></span><strong>pPrimaryDesc</strong></p></td>
<td align="left"><p>ランタイムは、値を<strong>NULL</strong>に設定します。</p></td>
</tr>
</tbody>
</table>

 

[***Resourcemap***](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourcemap) **関数**—

[*Resourcemap*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourcemap)に対する次の入力パラメーターは制限されています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">[説明]</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="hResource"></span><span id="hresource"></span><span id="HRESOURCE"></span><em>hResource</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource" data-raw-source="[&lt;em&gt;CreateResource(D3D11)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource)"><em>CREATERESOURCE</em></a>の作成呼び出しで<em>mapflags</em>に0以外の値が設定されている場合、Direct3D ランタイムは<strong>D3D10DDIRESOURCE_BUFFER</strong>リソースのみを設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span></span><em></em></p></td>
<td align="left"><p>ランタイムは、 <strong>DXGI_FORMAT_UNKNOWN</strong>値のみを設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Subresource"></span><span id="subresource"></span><span id="SUBRESOURCE"></span><em>Subresource</em></p></td>
<td align="left"><p>ランタイムは、値を0に設定するだけです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="DDIMap"></span><span id="ddimap"></span><span id="DDIMAP"></span><em>DDIMap</em></p></td>
<td align="left"><p>ここに記載されている他のすべてのメンバーの要件が満たされている場合、ランタイムは<strong>D3D10_DDI_MAP_READ</strong>、 <strong>D3D10_DDI_MAP_WRITE</strong>、または<strong>D3D10_DDI_MAP_READWRITE</strong>の値を設定できます。これは、作成呼び出しで設定された<em>MAPFLAGS</em>値と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource" data-raw-source="[&lt;em&gt;CreateResource(D3D11)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource)"><em>createresource (D3D11)</em></a>に一致します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span><em>示す</em></p></td>
<td align="left"><p>ランタイムからの入力値が制限されていませんが、ドライバーは<strong>D3D10_DDI_MAP_FLAG_DONOTWAIT</strong>値をサポートできる必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="pMappedSubResource"></span><span id="pmappedsubresource"></span><span id="PMAPPEDSUBRESOURCE"></span>pMappedSubResource</p></td>
<td align="left"><p>ランタイムからの入力値が制限されていませんが、ドライバーは、有効な CPU キャッシュ可能なポインターを<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddi_mapped_subresource" data-raw-source="[&lt;strong&gt;D3D10DDI_MAPPED_SUBRESOURCE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddi_mapped_subresource)"><strong>D3D10DDI_MAPPED_SUBRESOURCE</strong></a>に割り当てる必要があります。<strong>pdata</strong>メンバーは、バッファーのサイズと<strong>pData</strong>に指定されたデータに一致するように、 <strong>rowpitch</strong>と<strong>DepthPitch</strong>を設定する必要があります。</p></td>
</tr>
</tbody>
</table>

 

[***Resourceunmap***](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourceunmap)解除 **関数**-

[*Resourceunmap マップ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourceunmap)解除に対する次の入力パラメーターは制限されています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">[説明]</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="hDevice"></span><span id="hdevice"></span><span id="HDEVICE"></span><em>hDevice</em></p></td>
<td align="left"><p>Direct3D ランタイムからの入力値は制限されていませんが、元の<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourcemap" data-raw-source="[&lt;em&gt;ResourceMap&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourcemap)"><em>Resourcemap</em></a>呼び出しの<em>hdevice</em>値に一致する値が使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="hResource"></span><span id="hresource"></span><span id="HRESOURCE"></span><em>hResource</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource" data-raw-source="[&lt;em&gt;CreateResource(D3D11)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource)"><em>Createresource (D3D11)</em></a>の作成呼び出しで<em>mapflags</em>の0以外の値が設定されている場合、ランタイムは<strong>D3D10DDIRESOURCE_BUFFER</strong>リソースのみを設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Subresource"></span><span id="subresource"></span><span id="SUBRESOURCE"></span><em>Subresource</em></p></td>
<td align="left"><p>ランタイムは、値を0に設定するだけです。</p></td>
</tr>
</tbody>
</table>

 

 

 





