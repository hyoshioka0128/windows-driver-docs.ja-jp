---
title: 色形式の処理
description: 色形式の処理
ms.assetid: 4d0faba6-1994-474f-a5d3-e25cd2800cf7
keywords:
- Unidrv、色の形式
- 色は WDK Unidrv を書式設定します。
- 返さ機能
- プリンターのカラー形式 WDK Unidrv
- カラー管理 WDK の印刷の形式
- Unidrv WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5ef06be43537bfd2ce64fe5bfb15e46f6aed9c3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378596"
---
# <a name="handling-color-formats"></a>色形式の処理





プリンターがサポートする各色形式は、返さ機能へのオプションとして指定されます。 使用して[返さ機能の属性をオプション](option-attributes-for-the-colormode-feature.md)プリンターが受け取る各色形式を記述することができます。 次の表は、Unidrv を処理できる色のデータ形式を示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>カラー プレーン数</th>
<th>1 ピクセルあたりのビット数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>デバイスで (<em>DevNumOfPlanes)</td>
<td>デバイスで (</em>DevBPP)</td>
</tr>
<tr class="even">
<td><p>1</p></td>
<td><p>1 (黒と白)</p></td>
</tr>
<tr class="odd">
<td><p>1</p></td>
<td><p>8</p></td>
</tr>
<tr class="even">
<td><p>1</p></td>
<td><p>24</p></td>
</tr>
<tr class="odd">
<td><p>3</p></td>
<td><p>1 (CMY および RGB)</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>1 (<a href="https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-cmyk" data-raw-source="&lt;em&gt;CMYK&lt;/em&gt;"><em>CMYK</em></a>)</p></td>
</tr>
</tbody>
</table>

 

これらの形式の Unidrv を変換できる*デバイスに依存しないビットマップ (DIB)* に適切なデータを書式設定し、プリンターに送信します。 (このデータに対して実行できるハーフトーン操作が記載されて[Unidrv のハーフトーン](halftoning-with-unidrv.md))。

プリンターでは、前の表に記載されていない色形式をサポートする場合は、次の操作を行う必要があります。

-   設定、 \*DevNumOfPlanes と\*DevBPP 属性を 0 にします。 これを行うと、Unidrv は DIB のデータをプリンターに送信できなくなります。

-   提供、[プラグインでレンダリング](rendering-plug-ins.md)を実装する、 [ **IPrintOemUni::ImageProcessing** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)メソッド。

[ **IPrintOemUni::ImageProcessing** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)メソッドは、次の操作を実行する必要があります。

-   DIB データをプリンターのカラー形式に変換します。

-   ハーフトーン データ操作を実行します。

-   印刷スプーラーにデータを送信します。

提供の詳細については、 [ **IPrintOemUni::ImageProcessing** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)関数を参照してください[色の書式設定のカスタマイズ](customized-color-formats.md)します。

### <a name="rendering-high-quality-images"></a>高品質なイメージのレンダリング

各色の形式では、プリンターのハードウェアが受け取るピクセルあたりのビットとピクセルの Dib を作成するときに使用する Unidrv たいごとのビットの両方を指定します。 これらの値がで指定された、 \*DevBPP と\*DrvBPP 属性にそれぞれします。 場合によっては、(順序で、たとえば、高品質の写真を再現しようとする)、プリンターで処理できるよりも高い番号ビット/ピクセルのビットマップとしてレンダリングされるイメージのことをお勧めします。 そのため、指定する許容は、 \* **DrvBPP**を乗算した結果よりも大きい値を\* **DevBPP**値を\*DevNumOfPlanes 値。

たとえば、24 ビット/ピクセルのビットマップ、として表示するイメージを原因となる返さオプションを定義したいが、そのビットマップとしてプリンターに送信する場合*CMYK*データ。 次のようにこのモードを定義する場合があります。

```cpp
*Feature: ColorMode
{
    *Option: 24toCMYK
    {
        *Name: "Photographic Quality"
        *DrvBPP: 24
        *DevNumOfPlanes: 4
        *DevBPP: 1
        *ColorPlaneOrder: LIST(CYAN, MAGENTA, YELLOW, BLACK)
        *IPCallbackID: 1
    }
 other options
}
```

この例で、 \* **DevBPP**と\* **DevNumOfPlanes** Unidrv がレンダリングしに送信される 4 平面、平面あたり 1 ビット CMYK 形式を表す属性をプリンターです。 ただし、ここでは、ハーフトーン処理する必要があります実行描画された画像の印刷前にします。 [ミニドライバーが指定したハーフトーン](minidriver-supplied-halftoning.md)使用する必要があります。

 

 




