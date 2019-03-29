---
title: Direct3D レンダリングのパフォーマンスの向上
description: Windows Display Driver Model (WDDM) 1.3 およびそれ以降のドライバーできますマイクロソフトの Direct3D Direct3D 9 のハードウェアを改善できるレンダリング パフォーマンスの向上をハードウェア コマンド バッファーとカウンターの使用をサポートしてとをシステム メモリの効率的なコピーを作成します。サブリソースします。 Direct3D のバージョン 10 ハードウェアで利用できる機能の一部をミラー化には、これらの機能は、新しい Windows 8.1 以降です。
ms.assetid: F9AAE489-EC45-4EE6-875E-E084BB3054EE
ms.date: 10/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: cbed8871a27bf3aec88a928492c1d822f06d398c
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349499"
---
# <a name="direct3d-rendering-performance-improvements"></a>Direct3D レンダリングのパフォーマンスの向上


Windows Display Driver Model (WDDM) 1.3 およびそれ以降のドライバーできますマイクロソフトの Direct3D Direct3D 9 のハードウェアを改善できるレンダリング パフォーマンスの向上をハードウェア コマンド バッファーとカウンターの使用をサポートしてとをシステム メモリの効率的なコピーを作成します。サブリソースします。 Direct3D のバージョン 10 ハードウェアで利用できる機能の一部をミラー化には、これらの機能は、新しい Windows 8.1 以降です。

新しいトリミングの Direct3D 11.1 リソースとマップ既定のパフォーマンスの向上も使用できます。 マップの既定のシナリオは、以下の動作変更セクションに記載されています。

## <a name="span-idrenderingperformancereferencespanspan-idrenderingperformancereferencespanspan-idrenderingperformancereferencespanrendering-performance-reference"></a><span id="Rendering_performance_reference"></span><span id="rendering_performance_reference"></span><span id="RENDERING_PERFORMANCE_REFERENCE"></span>レンダリングのパフォーマンスのリファレンス


このリファレンス セクションでは、ユーザー モード デバイス ドライバー インターフェイス (Ddi) について説明します。

### <a name="direct3d-rendering-performance-functions-implemented-by-the-user-mode-driver"></a>ユーザー モード ドライバーによって実装された Direct3D レンダリング パフォーマンス関数

このセクションには、Windows 表示 Driver Model (WDDM) 1.3 およびそれ以降のユーザー モードでマイクロソフトの Direct3D レンダリングのパフォーマンスの向上をサポートするためにドライバーの実装を表示する関数が含まれています。


|||
|:--|:--|
|[PFND3DDDI_FLUSH1](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_flush1)| [PFND3DDDI_CHECKCOUNTERINFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_checkcounterinfo)|
|[PFND3DDDI_CHECKCOUNTER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_checkcounter) |[PFND3DDDI_UPDATESUBRESOURCEUP](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_updatesubresourceup)|

### <a name="direct3d-rendering-performance-structures-and-enumerations"></a>Direct3D レンダリング パフォーマンス構造および列挙体

これらのユーザー モードの構造および列挙体は、レンダリングのパフォーマンスの向上をサポートし、は、新しいまたは Windows 8.1 向けに更新されました。 Direct3D レベル 9 ドライバー以外のすべての適用[ **D3D11\_1\_DDI\_フラッシュ\_フラグ**](https://msdn.microsoft.com/library/windows/hardware/hh451049)します。

-   [**D3DDDI\_フラッシュ\_フラグ**](https://msdn.microsoft.com/library/windows/hardware/dn449154) (新規)
-   [**D3DDDIARG\_COPYFLAGS** ](https://msdn.microsoft.com/library/windows/hardware/dn449151) (新規)
-   [**D3DDDIARG\_カウンター\_情報**](https://msdn.microsoft.com/library/windows/hardware/dn449152) (新規)
-   [**D3DDDIARG\_UPDATESUBRESOURCEUP** ](https://msdn.microsoft.com/library/windows/hardware/dn449153) (新規)
-   [**D3DDDICAPS\_単純\_INSTANCING\_サポート**](https://msdn.microsoft.com/library/windows/hardware/dn465882) (新規)
-   [*CreateResource2* ](https://msdn.microsoft.com/library/windows/hardware/hh406287) (WDDM 1.3 およびそれ以降の Direct3D レベル 9 ドライバーに返す必要があります、 **E\_INVALIDARG**エラー コードの場合、 **CaptureBuffer**フラグの値の設定)
-   [**D3D11\_1\_DDI\_フラッシュ\_フラグ**](https://msdn.microsoft.com/library/windows/hardware/hh451049) (**D3DWDDM1\_3DDI\_トリミング\_メモリ**定数追加)
-   [**D3DDDI\_DEVICEFUNCS** ](https://msdn.microsoft.com/library/windows/hardware/ff544519) (**pfnFlush1**、 **pfnCheckCounterInfo**、 **pfnCheckCounter**、 **pfnUpdateSubresourceUP**追加されたメンバー)
-   [**D3DDDI\_プール**](https://msdn.microsoft.com/library/windows/hardware/ff544634) (**D3DDDIPOOL\_STAGINGMEM**定数の追加)
-   [**D3DDDICAPS\_型**](https://msdn.microsoft.com/library/windows/hardware/ff544132) (**D3DDDICAPS\_取得\_単純\_INSTANCING\_サポート**定数の追加)
-   [*GetCaps* ](https://msdn.microsoft.com/library/windows/hardware/ff566762) (「解説」の新しい情報)

## <a name="span-idddiimplementationrequirementsstartingwithwddm13spanspan-idddiimplementationrequirementsstartingwithwddm13spanddi-implementation-requirements-starting-with-wddm-13"></a><span id="ddi_implementation_requirements_starting_with_wddm_1.3"></span><span id="DDI_IMPLEMENTATION_REQUIREMENTS_STARTING_WITH_WDDM_1.3"></span>WDDM 1.3 以降 DDI 実装要件


WDDM 1.3 以降では、次の関数は必須またはオプションでは、ユーザー モード ドライバーを実装するには。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数グループ</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="_9_functions_that_are_optional_prior_to__1.3._Now_required_"></span><span id="_9_functions_that_are_optional_prior_to__1.3._now_required_"></span><span id="_9_FUNCTIONS_THAT_ARE_OPTIONAL_PRIOR_TO__1.3._NOW_REQUIRED_"></span>WDDM 1.3 の前に省略可能である Direct3D 9 関数。 必要なようになりました。</p></td>
<td align="left"><ul>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh406236" data-raw-source="[&lt;em&gt;BufBlt1&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406236)"><em>BufBlt1</em></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh406287" data-raw-source="[&lt;em&gt;CreateResource2&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406287)"><em>CreateResource2</em></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh439866" data-raw-source="[&lt;em&gt;TexBlt1&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439866)"><em>TexBlt1</em></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh439911" data-raw-source="[&lt;em&gt;VolBlt1&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439911)"><em>VolBlt1</em></a></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><span id="_9_functions_that_are_available_starting_with__1.3._A_driver_must_either_implement_all_of_these_functions_or_none_of_them_"></span><span id="_9_functions_that_are_available_starting_with__1.3._a_driver_must_either_implement_all_of_these_functions_or_none_of_them_"></span><span id="_9_FUNCTIONS_THAT_ARE_AVAILABLE_STARTING_WITH__1.3._A_DRIVER_MUST_EITHER_IMPLEMENT_ALL_OF_THESE_FUNCTIONS_OR_NONE_OF_THEM_"></span>WDDM 1.3 以降より使用可能である Direct3D 9 関数。 ドライバーは、これらすべての関数、またはそれらのいずれを実装する必要がありますか。</p></td>
<td align="left"><ul>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/dn449227" data-raw-source="[&lt;em&gt;pfnCheckCounter&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/dn449227)"><em>pfnCheckCounter</em></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/dn449228" data-raw-source="[&lt;em&gt;pfnCheckCounterInfo&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/dn449228)"><em>pfnCheckCounterInfo</em></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/dn449229" data-raw-source="[&lt;em&gt;pfnFlush1&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/dn449229)"><em>pfnFlush1</em></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/dn458010" data-raw-source="[&lt;em&gt;pfnPresent1(D3D)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/dn458010)"><em>pfnPresent1(D3D)</em></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/dn469267" data-raw-source="[&lt;em&gt;pfnPresent1(DXGI)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/dn469267)"><em>pfnPresent1(DXGI)</em></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/dn449230" data-raw-source="[&lt;em&gt;pfnUpdateSubresourceUP&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/dn449230)"><em>pfnUpdateSubresourceUP</em></a></li>
<li>pfnSetMarker</li>
<li>pfnSetMarkerMode</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="When_the__1.3_and_later_optional_functions_immediately_above_are_implemented__these_functions_have_associated_behavior_changes_"></span><span id="when_the__1.3_and_later_optional_functions_immediately_above_are_implemented__these_functions_have_associated_behavior_changes_"></span><span id="WHEN_THE__1.3_AND_LATER_OPTIONAL_FUNCTIONS_IMMEDIATELY_ABOVE_ARE_IMPLEMENTED__THESE_FUNCTIONS_HAVE_ASSOCIATED_BEHAVIOR_CHANGES_"></span>WDDM 1.3 およびすぐに上記の後で省略可能な関数が実装された場合は、これらの関数は、動作の変更を関連付けられています。</p></td>
<td align="left"><ul>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff538252" data-raw-source="[&lt;em&gt;BltDXGI&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538252)"><em>BltDXGI</em> </a> -ネイティブのステージング</li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh406235" data-raw-source="[&lt;em&gt;Blt1DXGI&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406235)"><em>Blt1DXGI</em> </a> -ネイティブのステージング</li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh406287" data-raw-source="[&lt;em&gt;CreateResource2&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406287)"><em>CreateResource2</em> </a> -ネイティブのステージング環境、大規模なキャプチャ テクスチャ</li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff566762" data-raw-source="[&lt;em&gt;GetCaps&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566762)"><em>GetCaps</em> </a> — タイムスタンプが、単純なインスタンス化</li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff568213" data-raw-source="[&lt;em&gt;Lock&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568213)"><em>ロック</em></a> -ネイティブのステージング</li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh439866" data-raw-source="[&lt;em&gt;TexBlt1&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439866)"><em>TexBlt1</em> </a> -ネイティブのステージング</li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff570104" data-raw-source="[&lt;em&gt;Unlock&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570104)"><em>ロックを解除</em></a> -ネイティブのステージング</li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh439911" data-raw-source="[&lt;em&gt;VolBlt1&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439911)"><em>VolBlt1</em> </a> -ネイティブのステージング</li>
</ul>
<p>これらのシナリオは、ときに適用<a href="https://msdn.microsoft.com/library/windows/hardware/ff566762" data-raw-source="[&lt;em&gt;GetCaps&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566762)"> <em>GetCaps</em> </a>が呼び出されます。</p>
<ul>
<li>場合<strong>D3DDDICAPS_GETD3DQUERYDATA</strong>が、ドライバーは、タイムスタンプ、つまり、Direct3D のランタイムがサポートをマスクしませんサポートを報告できます必要に応じて設定します。</li>
<li>場合<strong>D3DDDICAPS_GET_SIMPLE_INSTANCING_SUPPORT</strong>設定、ドライバーは省略可能なハードウェアのサポートを報告できますがインスタンス化します。</li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><span id="These__11_functions_have_associated_behavior_changes_"></span><span id="these__11_functions_have_associated_behavior_changes_"></span><span id="THESE__11_FUNCTIONS_HAVE_ASSOCIATED_BEHAVIOR_CHANGES_"></span>Direct3d11 のこれらの関数の動作の変更が関連付けられています。</p></td>
<td align="left"><ul>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff540694" data-raw-source="[&lt;em&gt;CreateResource(D3D11)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540694)"><em>CreateResource(D3D11)</em> </a> — バッファー マップは既定 (以下のセクションの動作の変更を参照してください)</li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/dn449229" data-raw-source="[&lt;em&gt;pfnFlush1&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/dn449229)"><em>pfnFlush1</em> </a> -リソースのトリム</li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff569492" data-raw-source="[&lt;em&gt;ResourceMap&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff569492)"><em>ResourceMap</em> </a> — バッファー マップは既定 (以下のセクションの動作の変更を参照してください)</li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff569495" data-raw-source="[&lt;em&gt;ResourceUnmap&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff569495)"><em>ResourceUnmap</em> </a> — バッファー マップは既定 (以下のセクションの動作の変更を参照してください)</li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="span-idbehaviorspanspan-idbehaviorspanbehavior-changes-for-calls-to-resource-create-map-and-unmap-functions"></a><span id="_behavior_"></span><span id="_BEHAVIOR_"></span>リソースへの呼び出しの動作の変更を作成、マップ、および関数をマップ解除


WDDM 1.3 およびそれ以降のドライバーによって実装されるこれらの関数は、Direct3D のランタイムは、マップの既定のシナリオの入力値の制限のセットを提供します。 これらの制限値は、11.1 およびそれ以降の機能レベルをサポートするドライバーのみに適用されます。

[***CreateResource(D3D11)***](https://msdn.microsoft.com/library/windows/hardware/ff540694) **関数**:

これらの入力[ **D3D11DDIARG\_CREATERESOURCE** ](https://msdn.microsoft.com/library/windows/hardware/ff542062)構造体のメンバーに制限されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Member</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="ResourceDimension_and_Usage"></span><span id="resourcedimension_and_usage"></span><span id="RESOURCEDIMENSION_AND_USAGE"></span><strong>ResourceDimension</strong>と<strong>使用状況</strong></p></td>
<td align="left"><p>これらの動作の変更は、Direct3D のランタイム型を提供する場合にのみ適用されます<strong>D3D10DDIRESOURCE_BUFFER</strong>の<strong>ResourceDimension</strong>と種類<strong>D3D10_DDI_USAGE_DEFAULT</strong><strong>使用状況</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="BindFlags"></span><span id="bindflags"></span><span id="BINDFLAGS"></span><strong>BindFlags</strong></p></td>
<td align="left"><p>Direct3D ランタイム セットの場合のみ、 <strong>D3D10_DDI_BIND_SHADER_RESOURCE</strong>と<strong>D3D11_DDI_BIND_UNORDERED_ACCESS</strong>値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="MapFlags"></span><span id="mapflags"></span><span id="MAPFLAGS"></span><strong>MapFlags</strong></p></td>
<td align="left"><p>その他のメンバー要件をすべてここに表示が満たされた場合、ランタイムを設定できます<strong>D3D10_DDI_MAP_READ</strong>、 <strong>D3D10_DDI_MAP_WRITE</strong>、および<strong>D3D10_DDI_MAP_READWRITE</strong>値。 ドライバーは、これらの値をサポートする必要があります。 値<strong>D3D10_DDI_MAP_WRITE_DISCARD</strong>と<strong>D3D10_DDI_MAP_WRITE_NOOVERWRITE</strong>が無効です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="MiscFlags"></span><span id="miscflags"></span><span id="MISCFLAGS"></span><strong>MiscFlags</strong></p></td>
<td align="left"><p>ランタイムのみが設定、 <strong>D3D11_DDI_RESOURCE_MISC_BUFFER_ALLOW_RAW_VIEWS</strong>と<strong>D3D11_DDI_RESOURCE_MISC_BUFFER_STRUCTURED</strong>値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Format"></span><span id="format"></span><span id="FORMAT"></span><strong>書式設定</strong></p></td>
<td align="left"><p>ランタイムのみが設定、 <strong>DXGI_FORMAT_UNKNOWN</strong>値。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="SampleDesc"></span><span id="sampledesc"></span><span id="SAMPLEDESC"></span><strong>SampleDesc</strong></p></td>
<td align="left"><p>ランタイム セット、 <a href="https://msdn.microsoft.com/library/windows/desktop/bb173072" data-raw-source="[&lt;strong&gt;DXGI_SAMPLE_DESC&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/bb173072)"> <strong>DXGI_SAMPLE_DESC</strong></a>.<strong>カウント</strong>メンバーを 1 に、<strong>品質</strong>メンバーをゼロにします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="MipLevels"></span><span id="miplevels"></span><span id="MIPLEVELS"></span><strong>MipLevels</strong></p></td>
<td align="left"><p>ランタイムは、値を 1 に設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="ArraySize"></span><span id="arraysize"></span><span id="ARRAYSIZE"></span><strong>ArraySize</strong></p></td>
<td align="left"><p>ランタイムは、値を 1 に設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="pPrimaryDesc"></span><span id="pprimarydesc"></span><span id="PPRIMARYDESC"></span><strong>pPrimaryDesc</strong></p></td>
<td align="left"><p>ランタイムでは、値を設定<strong>NULL</strong>します。</p></td>
</tr>
</tbody>
</table>

 

[***ResourceMap***](https://msdn.microsoft.com/library/windows/hardware/ff569492) **関数**:

これらの入力パラメーターを[ *ResourceMap* ](https://msdn.microsoft.com/library/windows/hardware/ff569492)は制限されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="hResource"></span><span id="hresource"></span><span id="HRESOURCE"></span><em>hResource</em></p></td>
<td align="left"><p>Direct3D のランタイム設定のみを<strong>D3D10DDIRESOURCE_BUFFER</strong> 0 以外の値をリソース<em>MapFlags</em>作成の呼び出しで設定されている<a href="https://msdn.microsoft.com/library/windows/hardware/ff540694" data-raw-source="[&lt;em&gt;CreateResource(D3D11)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540694)"> <em>CreateResource(D3D11)</em></a>.</p></td>
</tr>
<tr class="even">
<td align="left"><p><span></span><em></em></p></td>
<td align="left"><p>ランタイムのみが設定、 <strong>DXGI_FORMAT_UNKNOWN</strong>値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Subresource"></span><span id="subresource"></span><span id="SUBRESOURCE"></span><em>Subresource</em></p></td>
<td align="left"><p>のみ、ランタイムは、値を 0 に設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="DDIMap"></span><span id="ddimap"></span><span id="DDIMAP"></span><em>DDIMap</em></p></td>
<td align="left"><p>その他のメンバー要件をすべてここに表示が満たされた場合、ランタイムを設定できます<strong>D3D10_DDI_MAP_READ</strong>、 <strong>D3D10_DDI_MAP_WRITE</strong>、または<strong>D3D10_DDI_MAP_READWRITE</strong>値一致する、 <em>MapFlags</em>値のセットの作成の呼び出しで<a href="https://msdn.microsoft.com/library/windows/hardware/ff540694" data-raw-source="[&lt;em&gt;CreateResource(D3D11)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540694)"> <em>CreateResource(D3D11)</em></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span><em>フラグ</em></p></td>
<td align="left"><p>ドライバーがサポートできる、ランタイムからの入力値は制限がありませんが、 <strong>D3D10_DDI_MAP_FLAG_DONOTWAIT</strong>値。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="pMappedSubResource"></span><span id="pmappedsubresource"></span><span id="PMAPPEDSUBRESOURCE"></span>pMappedSubResource</p></td>
<td align="left"><p>ランタイムからの入力値の制限はありませんが、ドライバーに有効な CPU キャッシュ可能なポインターを割り当てる必要があります、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff541839" data-raw-source="[&lt;strong&gt;D3D10DDI_MAPPED_SUBRESOURCE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541839)"> <strong>D3D10DDI_MAPPED_SUBRESOURCE</strong></a>.<strong>pData</strong>メンバーおよび設定する必要があります、 <strong>RowPitch</strong>と<strong>DepthPitch</strong>バッファーとに表示されるデータのサイズに合わせて<strong>pData</strong>します。</p></td>
</tr>
</tbody>
</table>

 

[***ResourceUnmap***](https://msdn.microsoft.com/library/windows/hardware/ff569495) **関数**:

これらの入力パラメーターを[ *ResourceUnmap* ](https://msdn.microsoft.com/library/windows/hardware/ff569495)は制限されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="hDevice"></span><span id="hdevice"></span><span id="HDEVICE"></span><em>hDevice</em></p></td>
<td align="left"><p>Direct3D ランタイムからの入力値が、制限はありませんが、値に一致する、 <em>hDevice</em> 、元の値<a href="https://msdn.microsoft.com/library/windows/hardware/ff569492" data-raw-source="[&lt;em&gt;ResourceMap&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff569492)"> <em>ResourceMap</em> </a>を呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="hResource"></span><span id="hresource"></span><span id="HRESOURCE"></span><em>hResource</em></p></td>
<td align="left"><p>ランタイム設定のみを<strong>D3D10DDIRESOURCE_BUFFER</strong> 0 以外の値をリソース<em>MapFlags</em>作成の呼び出しで設定されている<a href="https://msdn.microsoft.com/library/windows/hardware/ff540694" data-raw-source="[&lt;em&gt;CreateResource(D3D11)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540694)"> <em>CreateResource(D3D11)</em></a>.</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Subresource"></span><span id="subresource"></span><span id="SUBRESOURCE"></span><em>Subresource</em></p></td>
<td align="left"><p>のみ、ランタイムは、値を 0 に設定します。</p></td>
</tr>
</tbody>
</table>

 

 

 





