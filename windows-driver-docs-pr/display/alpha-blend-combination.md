---
title: アルファブレンドの組み合わせ
description: アルファブレンドの組み合わせ
ms.assetid: 567810da-ad8d-4ceb-b914-868632384d09
keywords:
- アルファブレンドと WDK の組み合わせ WDK DirectX VA
- 画像のブレンド (WDK DirectX VA)
- アルファブレンドの組み合わせ WDK DirectX VA、アルファブレンドの組み合わせについて
- 画像のブレンド WDK DirectX VA、アルファブレンドの組み合わせについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f553355f3f661cb8bc1df711e399e0c454f605cc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839073"
---
# <a name="alpha-blend-combination"></a>アルファブレンドの組み合わせ


## <span id="ddk_alpha_blend_combination_gg"></span><span id="DDK_ALPHA_BLEND_COMBINATION_GG"></span>


[BDXVA\_Func 変数](bdxva-func-variable.md)が3に等しい場合、指定された操作は、アルファブレンドの組み合わせになります。 アルファブレンドの組み合わせでは、最後に読み込まれたアルファブレンドのソース情報を取得し、それを参照画像と結合して、表示するブレンド画像を作成します。

[**DXVA\_BufferDescription**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_bufferdescription)構造体の**dwtypeindex**メンバーによって指定されたアルファブレンドの組み合わせバッファーは、ソース画像とアルファブレンドの情報からブレンドされた画像を生成するために使用されます。 変換元と変換先の画像が4:4:4 形式でない場合は、1番目のサンプル (たとえば、最初、3番目、5番目など) は、AYUV のアルファブレンドサーフェイスまたはそれと同等のグラフィックのブレンド情報をに適用します (解像度は低くなります)。) ブレンドされた結果を生成するために、必要に応じて垂直方向または水平方向のデータソースのクロミナンス情報を生成します。

次の構造体は、アルファブレンドの組み合わせを実装するために使用されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Structure</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_bufferdescription" data-raw-source="[&lt;strong&gt;DXVA_BufferDescription&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_bufferdescription)"><strong>DXVA_BufferDescription</strong></a></p></td>
<td align="left"><p>使用するアルファブレンドの組み合わせバッファーを指定します。 このバッファーは、ソース画像とアルファブレンド情報からのブレンドされた画像の生成を制御します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_blendcombination" data-raw-source="[&lt;strong&gt;DXVA_BlendCombination&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_blendcombination)"><strong>DXVA_BlendCombination</strong></a></p></td>
<td align="left"><p>アルファブレンドの組み合わせバッファーからブレンドされた画像を生成する方法を指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configalphacombine" data-raw-source="[&lt;strong&gt;DXVA_ConfigAlphaCombine&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configalphacombine)"><strong>DXVA_ConfigAlphaCombine</strong></a></p></td>
<td align="left"><p>アルファブレンドの組み合わせ操作を実行する方法の構成を確立します。</p></td>
</tr>
</tbody>
</table>

 

 

 





