---
title: 最適化されたテクスチャ
description: 最適化されたテクスチャ
ms.assetid: 2c1af9c0-f15a-426a-b861-09f3e1c8899e
keywords:
- テクスチャ管理 WDK Direct3D、最適化されたテクスチャ
- Direct3D WDK Windows 2000 の表示、テクスチャの管理
- 最適化されたテクスチャ WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 673a90cce1884e6e1809fc45465f04cd638e472e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557771"
---
# <a name="optimized-textures"></a>最適化されたテクスチャ


## <span id="ddk_optimized_textures_gg"></span><span id="DDK_OPTIMIZED_TEXTURES_GG"></span>


パフォーマンスを向上させるために一部のハードウェア ベンダは、標準の Microsoft DirectDraw surface 形式から、テクスチャ形式を変更されました。 1 つの方法では、参照の局所性を 2D メモリに配置されているため、ピクセルを並べて表示します。 たとえば、ピクセルは、配置する代わりにこのようなスキャンの 1 行ずつをスキャンします。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>3</p></td>
<td align="left"><p>... <em>width</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><em>幅</em>+1</p></td>
<td align="left"><p><em>幅</em>+2</p></td>
<td align="left"><p><em>幅</em>+3</p></td>
<td align="left"><p><em>幅</em>+4</p></td>
<td align="left"><p>...</p></td>
</tr>
</tbody>
</table>

 

ピクセルは、Dword の 4 x 8 ブロックで分類されます。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>3</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>5</p></td>
<td align="left"><p>6</p></td>
<td align="left"><p>7</p></td>
</tr>
</tbody>
</table>

 

したがっての参照を 1 つの連続する 32 バイトのメモリをラスタライザーを使用するためのピクセルの 4 x 8 ブロックでプルします。 このレイアウトにはメモリ参照が標準的な DirectDraw レイアウトよりも、ラスタライザーによって生成される通常のパターンの方がマップされます。 このようなスキーム 'スウィズ リング' として参照されます '修正プログラム' テクスチャまたはします。 これらの操作は、比較的に割り当てられるメモリの画面のサイズに影響を行い、実行を高速です。 ただし、アプリケーションを制御する必要がありますが、この操作ではまだ多く待機時間があります。

別の方法のビデオ メモリにテクスチャを圧縮して、アクセラレータ上でローカル キャッシュに展開することです。 これにより、最高速度で実行されているラスタライザーを保持するために必要なビデオ メモリ帯域幅が減少します。 DirectX 5.0、ドライバーでも実行できますこれが結果として得られる、小さいテクスチャのためのビデオ メモリ割り当てのアプリケーションのビューに影響を与えるくらい低速操作です。

ハードウェア ベンダーに合わせて、DirectX 6.0 およびそれ以降のバージョンのドライバーにテクスチャを使用すると、画面に独自の形式を変換する機会を提供する「最適化」テクスチャが有効にします。 最適化し、画面をロックできないより小さいか、元よりも大きい場合があります。

市場で多くの 3D アクセラレーター チップセット標準 DirectDraw メカニズムで表すことのできない独自の形式であります。 この機能は、このようなサーフェイスのタイプとすべてのハードウェアについて説明します。

多くの場合、更新する必要がある一部のテクスチャと可能な他のユーザーのアプリケーションがあるアプリケーションの間だけです。 結果として得られる改善のフィル レートにより修正プログラムの適用を享受後者のこれらできます。 示すように、フラグ、[に最適化されたテクスチャ API](optimized-texture-api.md)セクションは、それに応じてパフォーマンスを最適化できるようにドライバーには、この使用シナリオを指定するアプリケーションを許可します。

 

 





