---
title: ProcAmp プロパティ
description: ProcAmp プロパティ
ms.assetid: 412c9144-dd52-4b36-bea1-b17c9c2c95b3
keywords:
- ProcAmp の WDK DirectX va なので、プロパティ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 399d2975d06360626c3590cd247b951cdea6d590
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573748"
---
# <a name="procamp-properties"></a>ProcAmp プロパティ


## <span id="ddk_procamp_properties_gg"></span><span id="DDK_PROCAMP_PROPERTIES_GG"></span>


ディスプレイ ドライバーには、VMR ProcAmp プロパティについては、ドライバーを照会したときに最小値、最大値、ステップのサイズ、および既定値を指定する必要があります。 ドライバーは、この情報への呼び出しに応答を指定できます、 [ **ProcAmpControlQueryRange** ](https://msdn.microsoft.com/library/windows/hardware/ff563950)関数。 ドライバーは、ProcAmp プロパティの値を返すことができます、次に示します (すべての値が浮動小数点数) の推奨される設定。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">プロパティ</th>
<th align="left">最小</th>
<th align="left">最大</th>
<th align="left">既定</th>
<th align="left">増分値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Brightness</p></td>
<td align="left"><p>-100.0F</p></td>
<td align="left"><p>100.0F</p></td>
<td align="left"><p>0.0 F</p></td>
<td align="left"><p>0.1F</p></td>
</tr>
<tr class="even">
<td align="left"><p>Contrast</p></td>
<td align="left"><p>0.0 F</p></td>
<td align="left"><p>10.0F</p></td>
<td align="left"><p>1.0 F</p></td>
<td align="left"><p>0.01F</p></td>
</tr>
<tr class="odd">
<td align="left"><p>[彩度]</p></td>
<td align="left"><p>0.0 F</p></td>
<td align="left"><p>10.0F</p></td>
<td align="left"><p>1.0 F</p></td>
<td align="left"><p>0.01F</p></td>
</tr>
<tr class="even">
<td align="left"><p>[色合い]</p></td>
<td align="left"><p>-180.0F</p></td>
<td align="left"><p>180.0F</p></td>
<td align="left"><p>0.0 F</p></td>
<td align="left"><p>0.1F</p></td>
</tr>
</tbody>
</table>

 

既定値になることが重要、 *null*ビデオ ストリームの変換。 これにより、アプリケーションには ProcAmp コントロールのプロパティが変更しない場合、そのビデオのパイプラインの ProcAmp 調整のステージをバイパスする VMR できます。

VMR とディスプレイ ドライバー、ProcAmp プロパティを使用する場合に、特定の検証を実行します。 VMR は、ドライバーを呼び出す前に、次のパラメーターの検証を適用します。

-   VMR によりアプリケーションで指定された値が、ドライバーによって指定された有効な範囲内にあるようになります。 VMR は、アプリケーションが提供した値を指定した範囲をクランプします。 たとえば、明るさの最大値が 100 で、アプリケーションは 105 の値を指定する場合、VMR は ~ 100 のアプリケーションの値をクランプします。 アプリケーションが現在の明るさの設定を確認する VMR を照会したときは、ここで 100 クランプされた値を受け取ります。

-   VMR は、必要な値は最も近い場所に入ることには、ドライバーによって返されたステップのサイズ増分値で示されていることを確認するアプリケーションが提供した値に丸めできるようになります。 たとえば、明るさサイズ増分値が 0.5 の場合は、許可されている最小の明度の値は、-100.0 と-80.7 の値を提供するアプリケーション。 VMR を調整します。 アプリケーションの値を、最も近い-80.5 ここでは、有効な値。

ドライバーでは、次のリレーションシップが保持することを確認してください。

-   範囲の最大値は、範囲の最小値を超えています。 これは、最大と最小値の差が 0.0 より大きいことを意味します。

-   既定値および最大値は、次の式で示すように、ステップのサイズ増分値で指定された有効な場所に分類されます。
    ```cpp
    min + (int((default - min) / increment) * increment) == default
    min + (int((max - min) / increment) * increment) == max
    ```

-   通常、アプリケーションでは、ProcAmp 設定を表示する Windows のスライダー コントロールを使用し、65536 は、最大範囲の Windows のスライダーを制御するため、ために、ドライバーは、65536 よりも少ない ProcAmp の個別の値の数を保持する必要があります。 次の非等値は、選択した値の true 必要があります。
    ```cpp
    int((max - min) / increment) < 65536.
    ```

-   ご使用のハードウェアでサポートされていない ProcAmp プロパティ、ドライバーは、最大値、最小値、および 0.0 の増分サイズの既定値を返すはずです。

 

 





