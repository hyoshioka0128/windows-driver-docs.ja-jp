---
title: 縦横比とカスタム スケーリング モードの使用
description: 縦横比とカスタム スケーリング モードの使用
ms.assetid: cafb6597-64a2-4d0f-bf7b-ab37f9a53bdc
keywords:
- 縦横比のスケーリング WDK ディスプレイ
- カスタムスケーリング WDK ディスプレイ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82debc193bdeda448c909bd83508556075281e7c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825400"
---
# <a name="using-aspect-ratio-and-custom-scaling-modes"></a>縦横比とカスタム スケーリング モードの使用


Windows 7 以降で使用できる、拡張されたスケーリングおよびカスタムスケーリングモードを有効にする ( **dxgkddi\_インターフェイス\_バージョン**&gt;= **DXGKDDI\_インターフェイス\_バージョン\_WIN7**) では、次の機能が、表示ミニポートドライバーによって使用される、VidPN の現在のパスデータに追加されます。

-   [**D3DKMDT\_VIDPN\_\_パス\_スケーリング\_サポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_scaling_support)構造:

    **AspectRatioCenteredMax**と**カスタム**メンバー

-   [**D3DKMDT\_VIDPN\_\_パス\_スケーリング**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_vidpn_present_path_scaling)列挙型:

    **D3DKMDT\_vpps\_ASPECTRATIOCENTEREDMAX**と**D3DKMDT\_VPPS\_カスタム**値

### <a name="span-idspecifying_scaling_modesspanspan-idspecifying_scaling_modesspan-specifying-scaling-modes"></a><span id="specifying_scaling_modes"></span><span id="SPECIFYING_SCALING_MODES"></span>スケーリングモードの指定

これらのスケーリングモードを使用したモニター上のデスクトップの動作と外観については、「[デスクトップイメージのスケーリング](scaling-the-desktop-image.md)」を参照してください。 表示モードマネージャー (DMM) が[*DxgkDdiEnumVidPnCofuncModality*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_enumvidpncofuncmodality)関数を呼び出すと、ドライバーは[**D3DKMDT\_\_VIDPN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_scaling_support)のメンバーを設定する必要があります。\_パス\_、型に応じて\_のサポートをスケーリングします。次のように、VidPN 存在パスがサポートするスケーリングの。

<span id="________Identity_Scaling_______"></span><span id="________identity_scaling_______"></span><span id="________IDENTITY_SCALING_______"></span>Id のスケーリング   
パスに変換なしでコンテンツを表示できる場合は、 [**D3DKMDT\_\_\_VIDPN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_scaling_support)の**id**メンバーを設定し、\_のサポートを0以外の値にスケーリング\_ます。 [*DxgkDdiEnumVidPnCofuncModality*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_enumvidpncofuncmodality)が呼び出されたときに、 [**D3DKMDT\_VIDPN\_現在\_パス\_変換**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_transformation)構造の**スケーリング**メンバーを**D3DKMDT\_vpps\_IDENTITY に設定します。** .

<span id="________Centered_Scaling_______"></span><span id="________centered_scaling_______"></span><span id="________CENTERED_SCALING_______"></span>中央のスケーリング   
パスのサイズを調整してターゲットの中央に表示することができる場合は、 **D3DKMDT\_VIDPN\_\_のパス\_スケーリング\_サポートを設定します。中央**。 [*DxgkDdiEnumVidPnCofuncModality*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_enumvidpncofuncmodality)が呼び出されたときに、 **D3DKMDT\_VIDPN\_現在\_パス\_変換を設定します。** **D3DKMDT\_vpps\_中央**にスケーリングしています。

<span id="________Stretched_Scaling_______"></span><span id="________stretched_scaling_______"></span><span id="________STRETCHED_SCALING_______"></span>拡大/縮小   
ソースの縦横比を維持したまま、ターゲットに合わせて拡大縮小されたコンテンツをパスで表示できる場合は、 **D3DKMDT\_VIDPN\_\_のパス\_スケーリング\_サポートを設定します。拡大**。 [*DxgkDdiEnumVidPnCofuncModality*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_enumvidpncofuncmodality)が呼び出されたときに、 **D3DKMDT\_VIDPN\_現在\_パス\_変換を設定します。** **D3DKMDT\_vpps\_stretch**にスケーリングしています。

<span id="________Aspect-Ratio-Preserving_Stretched_Scaling_______"></span><span id="________aspect-ratio-preserving_stretched_scaling_______"></span><span id="________ASPECT-RATIO-PRESERVING_STRETCHED_SCALING_______"></span>縦横比-拡大したスケーリングの保持   
ソースの縦横比を維持したまま、ターゲットに合わせてソースコンテンツのサイズを変更できる場合は、 **D3DKMDT\_VIDPN\_\_のパス\_スケーリング\_サポートを設定します。AspectRatioCenteredMax**。 [*DxgkDdiEnumVidPnCofuncModality*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_enumvidpncofuncmodality)が呼び出されたときに、 **D3DKMDT\_VIDPN\_現在\_パス\_変換を設定します。** **D3DKMDT\_vpps\_ASPECTRATIOCENTEREDMAX**にスケーリングしています。

<span id="________Custom_Scaling_______"></span><span id="________custom_scaling_______"></span><span id="________CUSTOM_SCALING_______"></span>カスタムスケーリング   
パスに、もう一方の D3DKMDT で記述されていない1つまたは複数のスケーリングモードを表示できる場合は[ **\_vidpn\_\_パス\_スケーリング\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_scaling_support)によって構造体のメンバーがサポートされている場合は、set **D3DKMDT\_VIDPN\_present\_PATH\_スケーリング\_サポート。カスタム**。 [*DxgkDdiEnumVidPnCofuncModality*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_enumvidpncofuncmodality)が呼び出されたときに、 **D3DKMDT\_VIDPN\_現在\_パス\_変換を設定します。** **D3DKMDT\_vpps\_カスタム**にスケーリングします。 独立系ハードウェアベンダー (Ihv) は、プライベートエスケープ値を使用して、特定のターゲットでカスタムスケーリングを解釈する方法をドライバーに通知できます。

現在ピン留めされているターゲットモードとソースモードの縦横比が同じでも、サイズが異なる場合、表示ミニポートドライバーは、**拡大**および**中央**のメンバーのみを設定する必要があります。 この場合、DMM は**AspectRatioCenteredMax**メンバーの0以外の値をクリアします。

### <a name="span-idapi_to_ddi_scalingspanspan-idapi_to_ddi_scalingspan-api-to-ddi-scaling"></a><span id="api_to_ddi_scaling"></span><span id="API_TO_DDI_SCALING"></span>API から DDI へのスケーリング

次の表に、ユーザーモード API のスケーリング値と、 [**D3DKMDT\_VIDPN\_\_パス\_スケーリング**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_vidpn_present_path_scaling)の列挙値を表示する方法を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><a href="https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-setdisplayconfig" data-raw-source="[&lt;strong&gt;SetDisplayConfig&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-setdisplayconfig)"><strong>Setdisplayconfig</strong></a>API のスケーリング値</th>
<th align="left">DDI のスケーリング値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DC_IDENTITY</p></td>
<td align="left"><p>D3DKMDT_VPPS_IDENTITY</p></td>
</tr>
<tr class="even">
<td align="left"><p>DC_CENTERED</p></td>
<td align="left"><p>D3DKMDT_VPPS_CENTERED</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DC_STRETCHED</p></td>
<td align="left"><p>D3DKMDT_VPPS_STRETCHED</p></td>
</tr>
<tr class="even">
<td align="left"><p>DC_ASPRATIOMAX</p></td>
<td align="left"><p>D3DKMDT_VPPS_ASPECTRATIOCENTEREDMAX</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DC_CUSTOM</p></td>
<td align="left"><p>D3DKMDT_VPPS_CUSTOM</p></td>
</tr>
<tr class="even">
<td align="left"><p>DC_PREFERRED</p></td>
<td align="left"><p>D3DKMDT_VPPS_PREFERRED</p></td>
</tr>
</tbody>
</table>

 

このマッピングは、「[デスクトップイメージのスケーリング](scaling-the-desktop-image.md)」の表と共に使用して、ユーザーモードのスケーリング型が、ディスプレイミニポートドライバーに送信される DDI スケーリング型にどのように変換されるかを理解することができます。

### <a name="span-idscaling_and_driver_versionsspanspan-idscaling_and_driver_versionsspan-scaling-and-driver-versions"></a><span id="scaling_and_driver_versions"></span><span id="SCALING_AND_DRIVER_VERSIONS"></span>スケーリングとドライバーのバージョン

次の表は、異なるバージョンのオペレーティングシステムで実行されているさまざまなディスプレイミニポートドライバーのバージョンの動作を示しています。

ドライバーバージョンのオペレーティングシステムのバージョン

**Dxgkddi\_インターフェイス\_バージョン**&lt; **dxgkddi\_interface\_version\_WIN7**

キーを押しながら

&gt;= **Dxgkddi\_インターフェイス\_バージョン\_VISTA**

**Dxgkddi\_インターフェイス\_バージョン**&gt;= **DXGKDDI\_interface\_version\_WIN7**

Windows Vista

ドライバーには Windows Vista の動作があります。

ドライバーは、初期化中にオペレーティングシステムのバージョンを確認する必要があります。また、D3DKMDT\_\_VIDPN の**AspectRatioCenteredMax**および**カスタム**メンバーを公開したり使用したりしないでください。 **\_パス\_スケーリング @no__t7_ サポート。 (_s)** ドライバーがこの要件に違反した場合、DMM は**AspectRatioCenteredMax**と**Custom**を無視し、 **id**、**中央**、または**拡張**されたメンバーのみを認識します。 ドライバーが任意の VidPN パスで**D3DKMDT\_VPPS\_ASPECTRATIOCENTEREDMAX** scaling モードにピン留めしようとすると、dmm は **\_グラフィックス\_無効な\_パス\_コンテンツのステータスコードの状態を返し\_ジオメトリ\_変換**では、このスケーリングモードは全画面のストレッチモードと同じように扱われます。

Windows 7

オペレーティングシステムは、 **AspectRatioCenteredMax**メンバーと**カスタム**メンバーの値をクリアします。また、このドライバーでは、拡張スケーリングモードとカスタムスケーリングモードの縦横比がサポートされていないことを前提としています。 DMM では、スケーリングモード**D3DKMDT\_vpps\_IDENTITY**、 **D3DKMDT\_VPPS\_stretch**、または**D3DKMDT\_vpps\_中央揃え**でのみ設定されます。 ドライバーは、Windows Vista と同様に動作します。

ドライバーは**AspectRatioCenteredMax**メンバーをサポートする必要があり、オペレーティングシステムはコントロールパネルのアプリケーションからこのメンバーを使用します。 ドライバーは、**カスタム**メンバーを設定することによって、カスタマイズされた機能を必要に応じて実装できます。

 

DMM は、D3DKMDT の**AspectRatioCenteredMax**または**カスタム**メンバーの確認と使用を試みる前に、Driver インターフェイスが**DXGKDDI\_インターフェイス\_バージョン\_WIN7**を= &gt;ことを常に確認します。 [ **\_VIDPN\_\_パス\_スケーリング\_サポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_scaling_support)。

**重要**   **D3DKMDT\_VPPS\_ASPECTRATIOCENTEREDMAX**または**D3DKMDT\_vpps**をサポートするディスプレイミニポートドライバー\_カスタム値で**D3DKMDT\_vpps の値を設定することはできません @no__ が指定さ**れていません。

 

### <a name="span-idscaling_with_multiple_adaptersspanspan-idscaling_with_multiple_adaptersspan-scaling-with-multiple-adapters"></a><span id="scaling_with_multiple_adapters"></span><span id="SCALING_WITH_MULTIPLE_ADAPTERS"></span>複数のアダプターを使用したスケーリング

スケーリングの種類**D3DKMDT\_vpps\_ASPECTRATIOCENTEREDMAX**と**D3DKMDT\_vpps**の値は、Windows 7 で導入されたカスタム\_、グラフィックスに関連付けられている CCD 接続データベースに格納されます。処理ユニット (GPU)。 ユーザーが、これらのスケーリングメンバーをサポートするドライバーを使用して1つの GPU から別の GPU にモニターを移動した場合、元のドライバーで2番目の GPU がサポートされていない可能性があります。 この場合、オペレーティングシステムはこれらのスケーリングの種類をシステムの既定のスケーリングにマップします。

両方の Gpu がスケーリングの種類をサポートしている場合は **\_vpps\_ASPECTRATIOCENTEREDMAX**と**D3DKMDT\_vpps\_カスタム**であり、最初の Gpu のドライバーは**D3DKMDT\_VPPS を実装\_カスタム**カスタムスケーリング要求では、ユーザーがモニターを2番目の GPU に切り替えた場合、2番目の GPU のドライバーはカスタムスケーリング要求を解釈する方法を認識しないことがあります。 この場合、2番目のドライバーは[**DxgkDdiCommitVidPn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_commitvidpn)関数への呼び出しに失敗する必要があります。また、**サポートされている状態コード\_ではなく、\_\_\_\_グラフィックの状態**を返す必要があります。オペレーティングシステムによって、このスケーリングの種類がシステムの既定のスケーリングにマップされます。

 

 





