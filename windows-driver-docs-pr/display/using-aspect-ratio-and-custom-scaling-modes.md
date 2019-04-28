---
title: 縦横比とカスタム スケーリング モードの使用
description: 縦横比とカスタム スケーリング モードの使用
ms.assetid: cafb6597-64a2-4d0f-bf7b-ab37f9a53bdc
keywords:
- 縦横比の WDK ディスプレイのスケーリング
- カスタム スケーリング WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb3cbc649a3df2b2bdab04b14f6072914344d439
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361218"
---
# <a name="using-aspect-ratio-and-custom-scaling-modes"></a>縦横比とカスタム スケーリング モードの使用


拡張されたスケーリングの縦横比保持とカスタム スケーリング モード以降で利用可能 Windows 7 をサポートするために (場所**DXGKDDI\_インターフェイス\_バージョン** &gt; =  **DXGKDDI\_インターフェイス\_バージョン\_WIN7**) で使用されるパスのデータ表示のミニポート ドライバー VidPN 存在に追加されます、次の機能。

-   [**D3DKMDT\_VIDPN\_存在\_パス\_スケーリング\_サポート**](https://msdn.microsoft.com/library/windows/hardware/ff546712)構造体。

    **AspectRatioCenteredMax**と**カスタム**メンバー

-   [**D3DKMDT\_VIDPN\_存在\_パス\_スケーリング**](https://msdn.microsoft.com/library/windows/hardware/ff546706)列挙体。

    **D3DKMDT\_VPPS\_ASPECTRATIOCENTEREDMAX**と**D3DKMDT\_VPPS\_カスタム**値

### <a name="span-idspecifyingscalingmodesspanspan-idspecifyingscalingmodesspan-specifying-scaling-modes"></a><span id="specifying_scaling_modes"></span><span id="SPECIFYING_SCALING_MODES"></span> スケーリング モードを指定します。

動作とスケーリング モードこれらを使用して、モニターのデスクトップの外観が記載[デスクトップ イメージをスケーリング](scaling-the-desktop-image.md)します。 表示モードのマネージャー (DMM) を呼び出すと、 [ *DxgkDdiEnumVidPnCofuncModality* ](https://msdn.microsoft.com/library/windows/hardware/ff559649)関数の場合、ドライバーがのメンバーを設定する必要があります[ **D3DKMDT\_VIDPN\_存在\_パス\_スケーリング\_サポート**](https://msdn.microsoft.com/library/windows/hardware/ff546712) VidPN 表示パスをサポートしている、次のように拡大縮小の型に応じた。

<span id="________Identity_Scaling_______"></span><span id="________identity_scaling_______"></span><span id="________IDENTITY_SCALING_______"></span> Identity のスケーリング   
パスが変換なしでコンテンツを表示できる場合は、設定、 **Identity**のメンバー [ **D3DKMDT\_VIDPN\_存在\_パス\_のスケーリング\_サポート**](https://msdn.microsoft.com/library/windows/hardware/ff546712) 0 以外の値。 ときに[ *DxgkDdiEnumVidPnCofuncModality* ](https://msdn.microsoft.com/library/windows/hardware/ff559649)を呼び出すと、設定、**スケーリング**のメンバー、 [ **D3DKMDT\_VIDPN\_存在する\_パス\_変換**](https://msdn.microsoft.com/library/windows/hardware/ff546719)構造体を**D3DKMDT\_VPPS\_IDENTITY**します。

<span id="________Centered_Scaling_______"></span><span id="________centered_scaling_______"></span><span id="________CENTERED_SCALING_______"></span> スケーリングを中央揃え   
パスを表示できる場合、コンテンツの調整し、設定、ターゲットで中央揃え、 **D3DKMDT\_VIDPN\_存在\_パス\_スケーリング\_サポートします。中央揃え**します。 ときに[ *DxgkDdiEnumVidPnCofuncModality* ](https://msdn.microsoft.com/library/windows/hardware/ff559649)を呼び出すと、設定**D3DKMDT\_VIDPN\_存在\_パス\_変換します。スケーリング**に**D3DKMDT\_VPPS\_中央揃え**します。

<span id="________Stretched_Scaling_______"></span><span id="________stretched_scaling_______"></span><span id="________STRETCHED_SCALING_______"></span> スケールを拡大   
パスがないソースの縦横比を維持しながら、ターゲットに合わせて、設定にスケーリングするコンテンツを表示できる場合**D3DKMDT\_VIDPN\_存在\_パス\_スケーリング\_サポートします。伸縮**します。 ときに[ *DxgkDdiEnumVidPnCofuncModality* ](https://msdn.microsoft.com/library/windows/hardware/ff559649)を呼び出すと、設定**D3DKMDT\_VIDPN\_存在\_パス\_変換します。スケーリング**に**D3DKMDT\_VPPS\_STRETCHED**します。

<span id="________Aspect-Ratio-Preserving_Stretched_Scaling_______"></span><span id="________aspect-ratio-preserving_stretched_scaling_______"></span><span id="________ASPECT-RATIO-PRESERVING_STRETCHED_SCALING_______"></span> 拡張されたスケーリングの縦横比保持   
場合は、パスが元の縦横比を維持しながら、ターゲットに合わせて、設定のソース コンテンツをスケールできます**D3DKMDT\_VIDPN\_存在\_パス\_スケーリング\_サポートします。AspectRatioCenteredMax**します。 ときに[ *DxgkDdiEnumVidPnCofuncModality* ](https://msdn.microsoft.com/library/windows/hardware/ff559649)を呼び出すと、設定**D3DKMDT\_VIDPN\_存在\_パス\_変換します。スケーリング**に**D3DKMDT\_VPPS\_ASPECTRATIOCENTEREDMAX**します。

<span id="________Custom_Scaling_______"></span><span id="________custom_scaling_______"></span><span id="________CUSTOM_SCALING_______"></span> カスタムのスケーリング   
パスは、もう一方で説明されていない 1 つまたは複数のスケーリング モードを表示できる場合[ **D3DKMDT\_VIDPN\_存在\_パス\_スケーリング\_サポート**](https://msdn.microsoft.com/library/windows/hardware/ff546712)メンバー構造体は、設定**D3DKMDT\_VIDPN\_存在\_パス\_スケーリング\_サポートします。カスタム**します。 ときに[ *DxgkDdiEnumVidPnCofuncModality* ](https://msdn.microsoft.com/library/windows/hardware/ff559649)を呼び出すと、設定**D3DKMDT\_VIDPN\_存在\_パス\_変換します。スケーリング**に**D3DKMDT\_VPPS\_カスタム**します。 独立系ハードウェア ベンダー (Ihv) は、指定されたターゲットにカスタム スケーリングを解釈するのに方法をドライバーに通知するためにプライベートのエスケープ値を使用できます。

ディスプレイのミニポート ドライバーを設定する必要がありますのみ、現在のピン留めされたターゲットとソース モード縦横比があるサイズが異なっている場合は、 **Stretched**と**中央揃え**メンバー。 DMM がの 0 以外の値をクリアするこの場合、 **AspectRatioCenteredMax**メンバー。

### <a name="span-idapitoddiscalingspanspan-idapitoddiscalingspan-api-to-ddi-scaling"></a><span id="api_to_ddi_scaling"></span><span id="API_TO_DDI_SCALING"></span> DDI スケーリング API

値を表示ミニポート ドライバー DDI スケールに値をスケーリング ユーザー モード API の対応、 [ **D3DKMDT\_VIDPN\_存在\_パス\_スケーリング**](https://msdn.microsoft.com/library/windows/hardware/ff546706)列挙が次の表に示すようにします。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff569533" data-raw-source="[&lt;strong&gt;SetDisplayConfig&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff569533)"><strong>SetDisplayConfig</strong> </a> API のスケーリング値</th>
<th align="left">DDI スケール値</th>
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

 

このマッピングは、内のテーブルで使用できる[デスクトップ イメージをスケーリング](scaling-the-desktop-image.md)DDI ディスプレイのミニポート ドライバーに送信される種類のスケーリングにユーザー モードのスケーリング型を変換する方法を理解します。

### <a name="span-idscalinganddriverversionsspanspan-idscalinganddriverversionsspan-scaling-and-driver-versions"></a><span id="scaling_and_driver_versions"></span><span id="SCALING_AND_DRIVER_VERSIONS"></span> ドライバーのバージョンとスケーリング

異なるバージョンのオペレーティング システムで実行されているミニポート ドライバー バージョンの異なる表示の動作は、次の表に表示されます。

ドライバーのバージョンのオペレーティング システムのバージョン

**DXGKDDI\_INTERFACE\_VERSION** &lt; **DXGKDDI\_INTERFACE\_VERSION\_WIN7**

、

&gt;= **DXGKDDI\_INTERFACE\_VERSION\_VISTA**

**DXGKDDI\_インターフェイス\_バージョン** &gt; =  **DXGKDDI\_インターフェイス\_バージョン\_WIN7**

Windows Vista

ドライバーは、Windows Vista の動作はします。

ドライバーする必要がありますの初期化中に、オペレーティング システムのバージョンを確認する必要がありますしない公開を使用しても、 **AspectRatioCenteredMax**と**カスタム**のメンバー **D3DKMDT\_VIDPN\_存在\_パス\_スケーリング\_サポート**します。 ドライバーには、この要件に違反している、DMM は無視されます**AspectRatioCenteredMax**と**カスタム**のみが認識されますと、 **Identity**、**中央揃え**、または**Stretched**メンバー。 ピン留めしようとすると、ドライバー、 **D3DKMDT\_VPPS\_ASPECTRATIOCENTEREDMAX**任意 VidPN パスで拡大縮小モード、DMM は状態コードを返す、**状態\_グラフィックス\_無効な\_パス\_コンテンツ\_GEOMETRY\_変換**はこのスケーリング モードと同様に処理ストレッチ モードを全画面表示とします。

Windows 7

値をクリアして、オペレーティング システム、 **AspectRatioCenteredMax**と**カスタム**メンバー ストレッチ スケーリングの縦横比保持とカスタム スケーリングに、ドライバーがサポートされていないことを前提としていますモードです。 DMM はスケーリング モードを設定してのみ**D3DKMDT\_VPPS\_IDENTITY**、 **D3DKMDT\_VPPS\_STRETCHED**、または**D3DKMDT\_VPPS\_中央揃え**します。 ドライバーは、Windows Vista のように動作します。

ドライバーをサポートする必要があります、 **AspectRatioCenteredMax**メンバー、およびオペレーティング システム、コントロール パネル アプリケーションからそれを使用します。 ドライバーは必要に応じて設定してカスタマイズされた機能を実装、**カスタム**メンバー。

 

DMM で常に確認するはドライバー インターフェイス&gt; =  **DXGKDDI\_インターフェイス\_バージョン\_WIN7**を確認して、使用しようとその前に、 **AspectRatioCenteredMax**または**カスタム**のメンバー [ **D3DKMDT\_VIDPN\_存在\_パス\_スケーリング\_サポート**](https://msdn.microsoft.com/library/windows/hardware/ff546712)します。

**重要な**  をサポートする表示ミニポート ドライバー、 **D3DKMDT\_VPPS\_ASPECTRATIOCENTEREDMAX**または**D3DKMDT\_VPPS\_カスタム**値の値を設定しない必要があります**D3DKMDT\_VPPS\_NOTSPECIFIED**します。

 

### <a name="span-idscalingwithmultipleadaptersspanspan-idscalingwithmultipleadaptersspan-scaling-with-multiple-adapters"></a><span id="scaling_with_multiple_adapters"></span><span id="SCALING_WITH_MULTIPLE_ADAPTERS"></span> 複数のアダプターを使用したスケール

スケーリングの型の値**D3DKMDT\_VPPS\_ASPECTRATIOCENTEREDMAX**と**D3DKMDT\_VPPS\_カスタム**Windows 7 で導入された、グラフィックス処理ユニット (GPU) に関連付けられている CCD 接続データベースに格納されます。 ユーザーは、別の GPU にこれらのスケーリングのメンバーをサポートするドライバーを使用した GPU が 1 つのモニターを移動した場合、2 つ目の GPU を元のドライバーによってサポートされていません可能性があります。 ここで、オペレーティング システムでは、システム既定のスケーリングにこれらのスケーリング型をマップするされます。

両方の Gpu スケーリング型をサポートする場合**D3DKMDT\_VPPS\_ASPECTRATIOCENTEREDMAX**と**D3DKMDT\_VPPS\_カスタム**、およびそのドライバーが、最初の GPU を実装して、 **D3DKMDT\_VPPS\_カスタム**カスタム要求をスケーリングし、ユーザーは、2 つ目の GPU にモニターを切り替えた場合、2 つ目の gpu ドライバーおそらくが登録されていない方法カスタムのスケーリング要求を解釈します。 この場合、2 つ目のドライバーがへの呼び出しを失敗する必要があります、 [ **DxgkDdiCommitVidPn** ](https://msdn.microsoft.com/library/windows/hardware/ff559597)関数を返す必要があります、**状態\_グラフィックス\_VIDPN\_モダリティ\_いない\_サポートされている**状態コードはオペレーティング システムはシステムの既定のスケーリングにこのスケーリング型をマップします。

 

 





