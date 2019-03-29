---
title: DEVMODEW 構造体
description: DEVMODEW 構造体
ms.assetid: 26212e3b-a591-4ed6-b441-b130d8d4d948
keywords:
- GDI WDK Windows 2000 の表示、DEVMODEW 構造体
- グラフィックス ドライバー WDK Windows 2000 の表示、DEVMODEW 構造体
- DEVMODEW 構造 WDK Windows 2000 の表示
- Unicode の WDK グラフィック
- 描画 WDK GDI、DEVMODEW 構造体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57a77730819f0c24fd22ed745871f129594e2f15
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464320"
---
# <a name="the-devmodew-structure"></a>DEVMODEW 構造体


## <span id="ddk_the_devmodew_structure_gg"></span><span id="DDK_THE_DEVMODEW_STRUCTURE_GG"></span>


[ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)構造体は、Microsoft Windows SDK ドキュメントに記載されている DEVMODE 構造体の Unicode バージョンです。 (DEVMODEW で 'W' サフィックスは、「ワイド」、または Unicode 文字を表します)。アプリケーションは、いずれかの構造体を使用して、DEVMODE 構造体ではなく DEVMODEW 構造体を使用するドライバーが必要です。

### <a name="span-idpublicandprivatemembersspanspan-idpublicandprivatemembersspanpublic-and-private-members"></a><span id="public_and_private_members"></span><span id="PUBLIC_AND_PRIVATE_MEMBERS"></span>パブリックおよびプライベート メンバー

メンバー (そのパブリック DEVMODEW メンバーとも呼ばれます) が定義されている次の DEVMODEW 構造体の直後には、ドライバーで定義されたメンバー (プライベート DEVMODEW メンバー) のセットがあります。 次の図は、パブリックのセクション (実際 DEVMODEW 構造自体) とプライベートのセクションを示します。

![devmodew 構造体のパブリックおよびプライベートのセクションを示す図](images/devmode.png)

通常、プライベート メンバーは、プリンター ドライバーでのみ使用されます。 このプライベート領域内のバイト単位のサイズを提供するドライバー、 **dmDriverExtra**メンバー。 ドライバーで定義されたプライベート メンバーは、ドライバーによって排他的に使用されます。

プリンター ドライバーでは、印刷ドキュメントのユーザーの選択肢を指定する DEVMODEW 構造が使用されます。 プリンターで印刷、用紙のサイズにコピーの数やその他の属性など、これらのオプションの既定値を指定することも使用されます。 ディスプレイ デバイスの DEVMODEW 構造体にはビット/ピクセル、ピクセルの数、および表示頻度の数などの表示属性を指定します。

### <a name="span-idinitializingadevmodewstructurespanspan-idinitializingadevmodewstructurespaninitializing-a-devmodew-structure"></a><span id="initializing_a_devmodew_structure"></span><span id="INITIALIZING_A_DEVMODEW_STRUCTURE"></span>DEVMODEW 構造体の初期化

プリンタ ドライバまたはディスプレイ ドライバーによって使用されることがあるか、によって DEVMODEW 構造は、2 つの方法で初期化されます。

-   ディスプレイ ドライバー DEVMODEW 初期化

    ディスプレイ ドライバーの[ **DrvGetModes** ](https://msdn.microsoft.com/library/windows/hardware/ff556233)エントリ ポイントを 0 に DEVMODEW 構造体のすべてのメンバーを初期化します。 *DrvGetModes* 、ディスプレイ ドライバー DLL の名前をコピーする、 **dmDeviceName** 、メンバーを設定、 **dmSpecVersion**と**dmDriverVersion**メンバーDEVMODEW 構造体とコピーのバージョンでは、適切なメンバーに属性情報を表示します。

-   プリンター ドライバー DEVMODEW の初期化

    アプリケーションがいずれかに呼び出しを実行するときに**DocumentProperties** (DLL 関数、Microsoft Windows SDK ドキュメントで説明されているプリンター インターフェイス) または[ **DrvDocumentPropertySheets**](https://msdn.microsoft.com/library/windows/hardware/ff548548) (、NT ベースのオペレーティング システム グラフィックス DDI)、既定値を持つ DEVMODEW 構造を作成します。 アプリケーションでは、自由に DEVMODEW のパブリック メンバーのいずれかを変更します。 すべての変更後、アプリケーションする必要があります、ドライバーの内部 DEVMODEW 構造の変更されたメンバーをマージするために、前に呼び出すことが、同じ関数の 2 番目の呼び出しを加えます。 2 番目の呼び出しが必要ないくつかの変更が正しく機能しないからプリンター ドライバーを呼び出す DEVMODEW 構造を修正する必要があります。 アプリケーションがマージされた DEVMODEW 構造に渡す、ドキュメントが印刷しようとしていますが、**フォーマット**(Microsoft Windows SDK のドキュメントで説明されている) 上に渡されますが、 [ **DrvEnablePDEV** ](https://msdn.microsoft.com/library/windows/hardware/ff556211) DDI します。 その時点で、ドライバーの DLL のレンダリング DEVMODEW 構造を検証し、印刷ジョブを実行する前に、修復は、必要に応じて、します。

### <a name="span-idusingadevmodewstructurespanspan-idusingadevmodewstructurespanusing-a-devmodew-structure"></a><span id="using_a_devmodew_structure"></span><span id="USING_A_DEVMODEW_STRUCTURE"></span>DEVMODEW 構造体の使用

いくつかの Api および Ddi グラフィックは、印刷、デバイス機能、表示されているユーザー インターフェイス、およびその他のユーザーのクエリを実行するために DEVMODEW 構造体の情報を使用します。 たとえば、 [ **DrvConvertDevMode** ](https://msdn.microsoft.com/library/windows/hardware/ff548532)印刷スプーラー グラフィックス DDI の 1 つのオペレーティング システムのバージョンから DEVMODEW 構造体を別の変換をします。 プリンター ドライバーを別のオペレーティング システムのバージョンで実行されている別のコンピューターから DEVMODEW 構造体を取得する場合は、必要があります。

### <a name="span-idmodifyingadevmodewstructurespanspan-idmodifyingadevmodewstructurespanmodifying-a-devmodew-structure"></a><span id="modifying_a_devmodew_structure"></span><span id="MODIFYING_A_DEVMODEW_STRUCTURE"></span>DEVMODEW 構造の変更

アプリケーションとドライバーは DEVMODEW 構造体の要求し、そのパブリックの部分を直接変更するのには無料です。 ただし、唯一のドライバーがプライベート DEVMODEW 構造体のメンバーを変更する許可されます。

プライベート DEVMODEW 構造体のメンバーを変更するには場合は、ドライバーにプライベート データの先頭のオフセットを決定してする必要があります。 この構造体の先頭へのポインターを指定し、 **dmSize**メンバーで、構造体のパブリックの部分のサイズを保持するには、秘密の部分の先頭を検出できます。 次の例では、プライベートのセクションの先頭へのポインターを初期化する方法を示します。 この例で*pdm* DEVMODEW 構造体の先頭を指します。

```cpp
PVOID pvDriverData = (PVOID)  (((BYTE *) pdm) + (pdm -> dmSize));
```

### <a name="span-idprinterdriverdisplaydriverdevmodewdifferencesspanspan-idprinterdriverdisplaydriverdevmodewdifferencesspanprinter-driverdisplay-driver-devmodew-differences"></a><span id="printer_driver_display_driver_devmodew_differences"></span><span id="PRINTER_DRIVER_DISPLAY_DRIVER_DEVMODEW_DIFFERENCES"></span>プリンター ドライバーや表示ドライバー DEVMODEW の違い

DEVMODEW 構造体のメンバーは、3 つのカテゴリに分類されます。

-   プリンター ドライバーでのみ使用するメンバー

-   のみ使用するメンバーのディスプレイ ドライバー

-   プリンターとディスプレイ ドライバーの両方で使用するメンバー

次の表に、使用されるいくつかのパブリック DEVMODEW メンバー*のみ*プリンター ドライバーで。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">プリンター ドライバーでのみ使用する DEVMODEW メンバー</th>
<th align="left">目的</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>dmScale</strong></p></td>
<td align="left"><p>イメージが印刷をスケールする割合を指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>dmCopies</strong></p></td>
<td align="left"><p>印刷する部数を指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dmColor</strong></p></td>
<td align="left"><p>カラー プリンターがカラーかモノクロ印刷する必要があるかどうかを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>dmOrientation</strong></p></td>
<td align="left"><p>用紙の向きを指定します縦または横のいずれか。</p></td>
</tr>
</tbody>
</table>

 

次の表に、使用されるいくつかのパブリック DEVMODEW メンバー*のみ*でドライバーを表示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ディスプレイ ドライバーでのみ使用する DEVMODEW メンバー</th>
<th align="left">目的</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>dmBitsPerPel</strong></p></td>
<td align="left"><p>色の解像度ディスプレイ デバイスのピクセルあたりのビットを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>dmPelsWidth</strong></p></td>
<td align="left"><p>表示されているデバイスの画面のピクセル単位の幅を指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dmPelsHeight</strong></p></td>
<td align="left"><p>表示されているデバイスの画面のピクセル、高さを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>dmDisplayFlags</strong></p></td>
<td align="left"><p>ノンインター レースとインター レース モノクロの場合と色の表示モードを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dmDisplayFrequency</strong></p></td>
<td align="left"><p>ヘルツ、ディスプレイのリフレッシュ レートを指定します。</p></td>
</tr>
</tbody>
</table>

 

3 番目のテーブルには、ディスプレイ ドライバーとプリンターの両方で使用されるいくつかのパブリック DEVMODEW メンバーが一覧表示されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">プリンターやディスプレイ ドライバーによって使用される DEVMODEW メンバー</th>
<th align="left">目的</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>dmDeviceName</strong></p></td>
<td align="left"><p>表示されたら、ディスプレイ ドライバーの DLL を指定します。</p>
<div>
 
</div>
プリンターのプリンターの「表示名」を指定します。</td>
</tr>
<tr class="even">
<td align="left"><p><strong>dmFields</strong></p></td>
<td align="left"><p>それに続くメンバーが使用されている、DEVMODEW を識別するビット フラグを指定します。 たとえば、DM_BITSPERPEL フラグが設定されてときに、 <strong>dmBitsPerPel</strong>メンバーには、有効なデータが含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dmSize</strong></p></td>
<td align="left"><p>DEVMODEW 構造体のパブリックの部分のバイト単位のサイズを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>dmDriverExtra</strong></p></td>
<td align="left"><p>次のパブリック構造体のメンバー、プライベートのドライバーのデータのバイト数を指定します。 ディスプレイ ドライバーでは、これは、通常は 0 です。</p></td>
</tr>
</tbody>
</table>

 

 

 





