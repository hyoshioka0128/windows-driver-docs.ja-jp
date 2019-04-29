---
title: デスクトップ イメージのスケーリング
description: デスクトップ イメージのスケーリング
ms.assetid: e27c7510-45b0-46e6-878f-b901cdd1cd57
keywords:
- Windows 7 の WDK の表示、CCD 概念、デスクトップ イメージのスケーリングの接続が表示されます。
- WDK の Windows Server 2008 R2 の表示、CCD 概念、デスクトップ イメージのスケーリングの接続が表示されます。
- Windows 7 の WDK の表示、CCD 概念、デスクトップ イメージのスケーリングの構成が表示されます。
- WDK の Windows Server 2008 R2 の表示、CCD 概念、デスクトップ イメージのスケーリングの構成が表示されます。
- CCD WDK Windows 7 の概念のディスプレイ、デスクトップ イメージのスケーリング
- CCD 概念 WDK Windows Server 2008 R2 の表示、デスクトップ イメージのスケーリング
- WDK の Windows 7 のディスプレイのデスクトップ イメージのスケーリング
- WDK の Windows Server 2008 R2 の表示のデスクトップ イメージのスケーリング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 545000757901bb9a6b6002447fa62bbc684a7d78
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390546"
---
# <a name="scaling-the-desktop-image"></a>デスクトップ イメージのスケーリング


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows オペレーティング システムにのみ適用されます。

呼び出し元が使用できます、 [ **SetDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569533) CCD 関数をモニターしてデスクトップ イメージをスケーリングします。 場合は、デスクトップとモニターを使用して、同じ解像度、 **SetDisplayConfig**モニター デスクトップ イメージをスケーリングする必要はありません。 これは、 **SetDisplayConfig**操作は、スケーリングの識別と呼ばれます。 デスクトップとモニターの解像度が異なる場合、 **SetDisplayConfig**スケーリングの種類は次のいずれかに適用されます。 モニターの解像度がによって定義されている、 [ **DISPLAYCONFIG\_ターゲット\_モード**](https://msdn.microsoft.com/library/windows/hardware/ff553993)構造体。

<span id="Centered"></span><span id="centered"></span><span id="CENTERED"></span>**中央揃え**  
中央揃えのスケーリングは、デスクトップがせず、スケーリングは、すべてのモニターに表示されるモードです。 ときに[ **SetDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569533)中央揃えのスケーリングでは、適用される黒い帯が、デスクトップの上下に表示される可能性があります。 中央のスケーリングを次に示します。

![中央揃えのスケーリング方法を示す図](images/ccd-center-scale.png)

<span id="Stretched"></span><span id="stretched"></span><span id="STRETCHED"></span>**拡大**  
拡張されたスケールでデスクトップが水平および垂直に拡大する表示全体が使用されていることを確認するモニターのモードです。 ときに[ **SetDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569533)適用されるスケールを拡大、黒い帯がないデスクトップの上下に表示します。 ただし、デスクトップはゆがんで見える可能性があります。 スケール拡張を次に示します。

![拡大縮小拡大を示す図します。](images/ccd-stretch-scale.png)

<span id="Aspect-Ratio-Preserving_Stretched"></span><span id="aspect-ratio-preserving_stretched"></span><span id="ASPECT-RATIO-PRESERVING_STRETCHED"></span>**伸縮縦横比保持**  
拡張されたスケールの縦横比保持は、デスクトップの水平方向に拡張し、可能な限り垂直方向に縦横比を維持しながらモードです。 ときに[ **SetDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569533)拡張スケーリングの縦横比保護を適用黒い帯表示がありますか*上と下*または*左側と右*デスクトップ。 黒のバンドを表示することはできませんただし、どちらも*上と下*と*の左と右*デスクトップ。 ユーザーは、優先するこのタイプのスケール、予想されるため、 **SetDisplayConfig**このタイプの既定値としてスケールを適用します。 次の図は、拡張されたスケーリングの縦横比保持を示します。

![拡張されたスケーリングの縦横比保持方法を示す図](images/ccd-arpstretch-scale.png)

スケーリングは、ソースとターゲット パスに使用されるモードによって異なります。 さらに、呼び出し元が呼び出すことができます[ **SetDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569533)ターゲット モードの情報を指定せず (つまり、設定、 *modeInfoArray*パラメーターは省略可能と設定することができます**NULL**)。 そのため、呼び出し元通常予測できない場合**SetDisplayConfig**スケーリングを実行する必要があります。 さらに、グラフィックス アダプターでサポートされる種類のスケーリングの完全な一覧を取得する API が存在しません。 [ **EnumDisplaySettings** ](https://msdn.microsoft.com/library/windows/desktop/dd162611) DMDFO を返します (Windows SDK のドキュメントで説明) Win32 関数\_の既定の**dmDisplayFixedOutput**メンバー、 **DEVMODE**構造体、 *lpDevMode*パラメーターが指す型をスケーリングする新しい Windows 7 を呼び出し元が要求したときにします。

スケーリング、呼び出し元に渡します[ **SetDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569533)スケーリング操作を実行する明示的な要求ではなく、インテントをスケーリングします。 スケーリングが必要な場合 (たとえば、ソースとターゲットの解像度が異なる)、 **SetDisplayConfig**呼び出し元が提供されるスケーリングを使用します。 指定されたスケールがサポートされていない場合**SetDisplayConfig**グラフィックス アダプターの既定値を使用してスケーリングします。 ときに、呼び出し元からに渡されるソースとターゲットの解像度**SetDisplayConfig**は同じですが、 **SetDisplayConfig**セットにスケーリングが識別されます。

次の表は、さまざまな[ **SetDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569533)のスケーリング要求。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">テーブルをシンボルします。</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DC_IDENTITY</p></td>
<td align="left"><p>DISPLAYCONFIG_SCALING_IDENTITY</p></td>
</tr>
<tr class="even">
<td align="left"><p>DC_CENTERED</p></td>
<td align="left"><p>DISPLAYCONFIG_SCALING_CENTERED</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DC_STRETCHED</p></td>
<td align="left"><p>DISPLAYCONFIG_SCALING_STRETCHED</p></td>
</tr>
<tr class="even">
<td align="left"><p>DC_ASPECTRATIOCENTEREDMAX</p></td>
<td align="left"><p>DISPLAYCONFIG_SCALING_ASPECTRATIOCENTEREDMAX</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DC_CUSTOM</p></td>
<td align="left"><p>DISPLAYCONFIG_SCALING_CUSTOM</p></td>
</tr>
<tr class="even">
<td align="left"><p>DC_PREFERRED</p></td>
<td align="left"><p>DISPLAYCONFIG_SCALING_PREFERRED</p></td>
</tr>
<tr class="odd">
<td align="left"><p>AdapterDefault</p></td>
<td align="left"><p>アダプターの既定の値を拡大縮小</p>
<p>現時点では、タブレットのシステムでは、既定値が拡大します。 タブレットではないシステムをサポートするグラフィックス アダプターで、 <a href="windows-vista-display-driver-model-design-guide.md" data-raw-source="[Windows Display Driver Model (WDDM)](windows-vista-display-driver-model-design-guide.md)">Windows Display Driver Model (WDDM)</a>、既定値はドライバーによって定義されます。 Windows Display Driver Model (WDDM) をサポートするグラフィックス アダプターを備えたタブレットではないシステムで<a href="https://msdn.microsoft.com/library/windows/hardware/ff557343" data-raw-source="[features new for Windows 7](https://msdn.microsoft.com/library/windows/hardware/ff557343)">Windows 7 の新機能</a>、既定値は DC_ASPECTRATIOCENTEREDMAX します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DatabaseValue</p></td>
<td align="left"><p>現在の接続モニターをデータベースからのスケールの値</p></td>
</tr>
</tbody>
</table>

 

次の表は、データベースに保存されている値と実際に設定されている値を示します。

結果ソース モード SetDisplayConfig に渡されたフラグをスケーリングし、結果ソース モードと別の解決策があるターゲット モード、ターゲット モードが同じ解像度をある**設定**

**ストア**

**設定**

**ストア**

DC\_ID Db ではなく現在の構成

DC\_の ID

AdapterDefault

AdapterDefault

AdapterDefault

DC\_ID Db での現在の構成

DC\_の ID

DatabaseValue

DatabaseValue

DatabaseValue

DC\_中央揃え

DC\_の ID

DC\_中央揃え

DC\_中央揃え

DC\_中央揃え

DC\_STRETCHED

DC\_の ID

DC\_STRETCHED

DC\_STRETCHED

DC\_STRETCHED

DC\_で Windows 7 の機能のドライバーを使用した WDDM ASPECTRATIOCENTEREDMAX

DC\_の ID

DC\_ASPRATIOMAX

DC\_ASPRATIOMAX

DC\_ASPRATIOMAX

DC\_WDDM ドライバーで ASPECTRATIOCENTEREDMAX

DC\_の ID

AdapterDefault

AdapterDefault

AdapterDefault

DC\_WDDM のパスにカスタム スケーリングをサポートしている Windows 7 の機能のドライバーを使用したカスタム

DC\_カスタム

DC\_カスタム

DC\_カスタム

DC\_カスタム

DC\_WDDM のパスにカスタム スケーリングをサポートしない機能ドライバーを Windows 7 を使用したカスタム

DC\_の ID

AdapterDefault

AdapterDefault

AdapterDefault

DC\_WDDM ドライバーでカスタム

DC\_の ID

AdapterDefault

AdapterDefault

AdapterDefault

DC\_Db ではなく現在の設定を優先

DC\_の ID

AdapterDefault

AdapterDefault

AdapterDefault

DC\_Db での現在の設定を優先

DC\_の ID

DatabaseValue

DatabaseValue

DatabaseValue

 

次の表は、スケール、呼び出し元に渡す方法、従来の[ **ChangeDisplaySettingsEx**](https://msdn.microsoft.com/library/windows/desktop/dd183413)API (Windows SDK のドキュメントで説明) は、スケール セットにマップされます。

結果ソース モード ChangeDisplaySettingsEx に渡されたフラグをスケーリングし、結果ソース モードと別の解決策があるターゲット モード、ターゲット モードが同じ解像度をある**設定**

**ストア**

**設定**

**ストア**

DMDFO\_CCD データベースではなく現在の構成で既定値

DC\_の ID

AdapterDefault

AdapterDefault

AdapterDefault

DMDFO\_CCD データベース内の現在の構成で既定値

DC\_の ID

DatabaseValue

DatabaseValue

DatabaseValue

DMDFO\_STRETCH

DC\_の ID

DC\_STRETCHED

DC\_STRETCHED

DC\_STRETCHED

DMDFO\_CENTER

DC\_の ID

DC\_中央揃え

DC\_中央揃え

DC\_中央揃え

DM\_DISPLAYFIXEDOUTPUT が未設定、CCD データベースではなく現在の構成

DC\_の ID

AdapterDefault

AdapterDefault

AdapterDefault

DM\_DISPLAYFIXEDOUTPUT が未設定、CCD データベース内の現在の構成

DC\_の ID

DatabaseValue

DatabaseValue

DatabaseValue

 

次の表は、どのディスプレイの構成のスケーリングを翻訳およびから返された[ **EnumDisplaySettings**](https://msdn.microsoft.com/library/windows/desktop/dd162611)します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">現在アクティブなスケーリング</th>
<th align="left">GDI スケーリングをレガシ EnumDIsplaySettings(ENUM_CURRENT_SETTINGS) から返される値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DC_IDENTITY</p></td>
<td align="left"><p>DMDFO_DEFAULT</p></td>
</tr>
<tr class="even">
<td align="left"><p>DC_CENTERED</p></td>
<td align="left"><p>DMDFO_CENTER</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DC_STRETCHED</p></td>
<td align="left"><p>DMDFO_STRETCH</p></td>
</tr>
<tr class="even">
<td align="left"><p>DC_ASPRATIOMAX</p></td>
<td align="left"><p>DMDFO_DEFAULT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DC_CUSTOM</p></td>
<td align="left"><p>DMDFO_DEFAULT</p></td>
</tr>
<tr class="even">
<td align="left"><p>DC_PREFERRED</p></td>
<td align="left"><p>DMDFO_DEFAULT</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddirectxgamesandscalingspanspan-iddirectxgamesandscalingspandirectx-games-and-scaling"></a><span id="directx_games_and_scaling"></span><span id="DIRECTX_GAMES_AND_SCALING"></span>DirectX ゲームとスケーリング

Microsoft DirectX 9 L と以前のランタイムは、アプリケーションでいつでも呼び出すことが必要です、 [ **ChangeDisplaySettingsEx** ](https://msdn.microsoft.com/library/windows/desktop/dd183413) DM せず関数\_DISPLAYFIXEDOUTPUT の設定、 **dmFields**構造体 DEVMODE のメンバー、 *lpDevMode*パラメーターを指します。 DirectX 10 およびそれ以降のランタイムを使用すると、アプリケーションのスケーリングにそれらのアプリケーションを渡すことを選択**ChangeDisplaySettingsEx**します。 次の表に、スケーリングのスケーリング フラグに渡される値のマッピング**ChangeDisplaySettingsEx**します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">DXGI 反転値をスケーリングするチェーン</th>
<th align="left">ChangeDisplaySettingsEx に渡されるフラグのスケーリング</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DXGI_MODE_SCALING_UNSPECIFIED</p></td>
<td align="left"><p>DMDFO_DEFAULT、DMDFO_CENTER、または DMDFO_STRETCH します。 アプリケーションを使用するスケールは、現在のデスクトップ スケーリングなど、いくつかの要因と、ドライバーを公開するモードの一覧に依存します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXGI_MODE_SCALING_CENTERED</p></td>
<td align="left"><p>DMDFO_CENTER</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DXGI_MODE_SCALING_STRETCHED</p></td>
<td align="left"><p>DMDFO_STRETCH</p></td>
</tr>
</tbody>
</table>

 

この情報を使用して、上記のスケーリング テーブルと組み合わせて、DirectX アプリケーションから予想されるスケールを特定できます。

 

 





