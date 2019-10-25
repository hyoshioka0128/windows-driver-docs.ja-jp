---
title: 色形式の処理
description: 色形式の処理
ms.assetid: 4d0faba6-1994-474f-a5d3-e25cd2800cf7
keywords:
- Unidrv、色の形式
- WDK Unidrv の色形式
- ColorMode 機能
- プリンターの色の形式 WDK Unidrv
- 色の管理 WDK 印刷、形式
- Unidrv WDK 印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9366dd1465a5db1af5f0073cc8addc9d1ec97671
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843407"
---
# <a name="handling-color-formats"></a>色形式の処理





プリンターがサポートする各カラーフォーマットは、ColorMode 機能のオプションとして指定されています。 [ColorMode 機能のオプション属性](option-attributes-for-the-colormode-feature.md)を使用して、プリンターが受け入れる各色の形式を記述できます。 次の表は、Unidrv が処理できるカラーデータ形式を示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>カラープレーンの数</th>
<th>ピクセルあたりのビット数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>デバイス (<em>DevNumOfPlanes)</td>
<td>デバイス (</em>DevBPP)</td>
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
<td><p>ホーム フォルダーが置かれているコンピューターにアクセスできない</p></td>
<td><p>1 (<a href="https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-cmyk" data-raw-source="&lt;em&gt;CMYK&lt;/em&gt;"><em>CMYK</em></a>)</p></td>
</tr>
</tbody>
</table>

 

これらの形式では、Unidrv は*デバイスに依存しないビットマップ (DIB)* データを適切な形式に変換し、プリンターに送信することができます。 (このデータに対して実行できるハーフトーン操作については、「[ハーフトーン](halftoning-with-unidrv.md)」を参照してください)。

プリンターが、前の表に記載されていない色の形式をサポートしている場合は、次の操作を行う必要があります。

-   \*DevNumOfPlanes と \*DevBPP 属性を0に設定します。 これにより、Unidrv がプリンターに DIB データを送信するのを防ぐことができます。

-   [**Iprintoemuni:: ImageProcessing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)メソッドを実装する[レンダリングプラグイン](rendering-plug-ins.md)を提供します。

[**Iprintoemuni:: ImageProcessing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)メソッドでは、次の操作を実行する必要があります。

-   DIB データをプリンターのカラー形式に変換します。

-   データに対してハーフトーン操作を実行します。

-   印刷スプーラにデータを送信します。

[**Iprintoemuni:: ImageProcessing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)関数の提供の詳細については、「カスタマイズされた[色の形式](customized-color-formats.md)」を参照してください。

### <a name="rendering-high-quality-images"></a>高品質イメージのレンダリング

各色フォーマットでは、プリンターのハードウェアが受け入れる1ピクセルあたりのビット数と、Dib の作成時に Unidrv で使用するピクセルあたりのビット数を指定します。 これらの値は、それぞれ \*DevBPP 属性と \*DrvBPP 属性で指定します。 場合によっては、画像をビットマップとしてレンダリングすることが望ましい場合があります。これは、プリンターが処理できるビット数 (たとえば、高品質の写真の再生を試行するため) によって、ピクセルあたりのビット数が多くなります。 したがって、\***Devbpp**値に \*DevNumOfPlanes 値を乗算した結果より大きい \***drvbpp**値を指定することもできます。

たとえば、画像を24ビット/ピクセルビットマップとしてレンダリングする ColorMode オプションを定義するとしますが、ビットマップが*CMYK*データとしてプリンターに送信されるようにするとします。 このモードは次のように定義できます。

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

この例では、\***Devbpp**属性と \***DevNumOfPlanes**属性は、Unidrv がレンダリングしてプリンターに送信できる4平面の1ビット単位の CMYK 形式を表します。 ただし、この場合は、表示されたイメージを印刷する前に、ハーフトーン操作を実行する必要があります。 [ミニドライバーを](minidriver-supplied-halftoning.md)使用する必要があります。

 

 




