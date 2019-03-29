---
title: フォント メトリック関数
description: フォント メトリック関数
ms.assetid: 22d88765-bde5-4f1b-b106-9396868d6fb3
keywords:
- フォント メトリック関数、WDK グラフィック
- GDI WDK Windows 2000 の表示、フォント、メトリック関数
- グラフィック ドライバー WDK Windows 2000 を表示、フォント、メトリック関数
- DrvQueryFontData
- DrvQueryFontTree
- DrvFree
- DrvDestroyFont
- DrvQueryFont
- IFIMETRICS
- ラスター フォント WDK グラフィック
- 概念的な空間座標系の WDK グラフィック
- WDK フォントのサイズ
- メトリックは、WDK のフォントを関数します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87a5e4126a6c68ab80380393f252eba74dbc6a5e
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350257"
---
# <a name="font-metric-functions"></a>フォント メトリック関数


## <span id="ddk_font_metric_functions_gg"></span><span id="DDK_FONT_METRIC_FUNCTIONS_GG"></span>


GDI フォント情報を指定する必要があります、ドライバーは、フォントをサポートする必要があります、ときに、 [ **IFIMETRICS** ](https://msdn.microsoft.com/library/windows/hardware/ff567418)構造体。 各フォントの別の IFIMETRICS 構造があります。 ほとんどのフィールドでは表現 FWORDs、各デザイン領域で、符号付き 16 ビット整数。 フォントがラスター フォントの場合は、デザイン領域とデバイスの領域が同じとフォントの単位はピクセルの間の距離に相当します。

基本的に、IFIMETRICS 構造体は、テキスト メトリック構造体のグラフィックス DDI バージョンです。 すべての距離は、フォント デザイナーの概念的な座標システムを参照してください。 概念的な領域の座標システムは、右手座標系デカルト座標システム上部の y 座標が増加し、x 座標が右方向に増加します。

IFIMETRICS 構造体は、可変長設計されています。 関連付けられたフォント文字の文字列の長さに制限はありません。 一般的 IFIMETRICS 構造体の最後のフィールドの直後に続く文字列を格納することをお勧めします。

フォントが用意されている任意のドライバーをサポートする必要があります、 [ **DrvQueryFont** ](https://msdn.microsoft.com/library/windows/hardware/ff556262)関数。 ドライバーはまた、関数を含めることができます[ **DrvQueryFontData** ](https://msdn.microsoft.com/library/windows/hardware/ff556264)実現されたフォントに関する情報を取得します。 呼び出しで*DrvQueryFontData*、GDI カーニング ハンドルまたはグリフの配列へのポインターを提供します。 ドライバーは、GDI のグリフが関連付けられている情報を返します[ **GLYPHDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff566819)構造体。 場合*DrvQueryFontData*されたハンドルをカーニングするには、指定されたカーニング Win32 POINTL 構造体の形式でのペアについての情報を返します。 次の表には、フォント メトリック関数が一覧表示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556192" data-raw-source="[&lt;strong&gt;DrvDestroyFont&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556192)"><strong>DrvDestroyFont</strong></a></p></td>
<td align="left"><p>ドライバーが、割り当てのデータ構造体を解放するために、フォントの実現化が必要がなくなったら、ドライバーに通知します。 GDI は、フォント プロデューサーでフォントのコンシューマーの 1 回この関数は 1 回呼び出します。 ドライバーが割り当てられているリソースを解放する必要がある場合にのみ、省略可能 - をサポートする必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556226" data-raw-source="[&lt;strong&gt;DrvFree&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556226)"><strong>DrvFree</strong></a></p></td>
<td align="left"><p>指定されたデータ構造が不要になったドライバーに通知します。 ドライバーのメモリ管理には、この情報が必要です。 場合にのみ、省略可能 - を実装する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556262" data-raw-source="[&lt;strong&gt;DrvQueryFont&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556262)"><strong>DrvQueryFont</strong></a></p></td>
<td align="left"><p>ポインターを返します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff567418" data-raw-source="[&lt;strong&gt;IFIMETRICS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567418)"> <strong>IFIMETRICS</strong> </a>フォントの構造体。 フォントを処理するすべてのドライバーで必要です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556264" data-raw-source="[&lt;strong&gt;DrvQueryFontData&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556264)"><strong>DrvQueryFontData</strong></a></p></td>
<td align="left"><p>実現されたフォントに関する情報を返します。 必要な (選択した<em>i モード</em>値) のフォントを処理するすべてのドライバーでします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556266" data-raw-source="[&lt;strong&gt;DrvQueryFontTree&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556266)"><strong>DrvQueryFontTree</strong></a></p></td>
<td align="left"><p>ポインターいずれかを定義する構造体をマッピングから返します Unicode グリフ ハンドルまたはカーニング ハンドルをカーニングするペアのマッピング。 フォントを処理するすべてのドライバーで必要です。</p></td>
</tr>
</tbody>
</table>

 

関数は、 *DrvQueryFontTree* GDI は、次のいずれかを定義するツリー構造体へのポインターを取得できます。

-   Unicode からグリフの変種を含めて、グリフのハンドルへのマッピング (GDI [ **FD\_GLYPHSET** ](https://msdn.microsoft.com/library/windows/hardware/ff565625)構造)

-   カーニング ハンドルをカーニングするペアのマッピング ([**FD\_受け取る**](https://msdn.microsoft.com/library/windows/hardware/ff565630)構造)

*DrvQueryFontTree*ドライバーでは、これらのファイルを可能であれば precompute する必要がありますので、必要な構造体を生成するための労力が必要です。 構造体は、リソースまたはファイルに格納できます。 呼び出すの読み込みやそれを読み取るのための最適な方法は、構造体がファイルに格納されている場合、 [ **EngMapFontFile** ](https://msdn.microsoft.com/library/windows/hardware/ff564972)関数は、ファイルをメモリにマップされます。 スワップ ファイルにファイルが追加されませんが、ため、メモリが利用できる、必要な場合を開くと、ファイルの読み取り中よりも効率的であります。

具体的には、ドライバーが内の識別子を返します、 *pid*パラメーター。 GDI に渡されます、 [ **DrvFree** ](https://msdn.microsoft.com/library/windows/hardware/ff556226)関数は、返されたポインターをときに、 [ **FD\_GLYPHSET** ](https://msdn.microsoft.com/library/windows/hardware/ff565625)構造体、または配列[ **FD\_受け取る**](https://msdn.microsoft.com/library/windows/hardware/ff565630)構造体が不要になった。 Driver では、メモリを管理する方法に応じて*pid*構造を識別、構造体の割り当てられたまたは何も特定できます。

[**DrvFree** ](https://msdn.microsoft.com/library/windows/hardware/ff556226)と[ **DrvDestroyFont** ](https://msdn.microsoft.com/library/windows/hardware/ff556192)は両方の省略可能な関数です。 GDI 呼び出し*DrvFree*に指定されたデータ構造が不要になったことをドライバーに通知します。 ドライバーは、構造体のメモリを割り当て、対応するデータ構造体を解放するときに通知する必要がありますしない限り、それを実装する必要はありません。 たとえば、データが関連付けられている場合、 [ **FONTOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff565974)構造体、削除への呼び出しまで遅らせることができます*DrvDestroyFont*に必要なことはできませんので、実装*DrvFree*します。

*DrvDestroyFont*ドライバーは、割り当て、データ構造体を解放できますようにフォントの実現化が必要がなくなったら、ドライバーに通知します。 GDI は、フォント プロデューサーでフォントのコンシューマーの 1 回この関数は 1 回呼び出します。 これは、フォントのインスタンスが破棄されるときに、ドライバーが割り当てられているリソースを解放する必要がある場合にのみに実装する必要があります。

 

 





