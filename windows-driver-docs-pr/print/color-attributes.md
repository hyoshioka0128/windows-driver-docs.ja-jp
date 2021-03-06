---
title: 色属性
description: 色属性
ms.assetid: c8de0186-9cf5-43e5-81e7-33351a34c13c
keywords:
- 色の WDK Unidrv 属性
- 一般的なプリンター WDK Unidrv、色を属性します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 746b8fd27306930e3095600ea3b5017c0778ba46
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359137"
---
# <a name="color-attributes"></a>色属性





色の属性は[一般的な印刷属性](general-printing-attributes.md)カラー印刷を制御するための特性を指定します。

次の表は、色の属性を一覧表示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>属性名</th>
<th>属性パラメーター</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong><em>ChangeColorModeOnDoc でしょうか。</strong></p></td>
<td><p><strong>TRUE</strong>または<strong>FALSE</strong>します。 副作用なしのドキュメントのページ間でプリンターのカラー モードを変更できるかどうかを示します。</p></td>
<td><p>任意。 指定されていない場合、既定値は<strong>TRUE</strong>します。 Unidrv は、印刷速度を最適化するために、この値を使用します。 詳細については、次の表の次の注を参照してください。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>CyanInMagentaDye</strong></p></td>
<td><p>0 ~ 1000、マゼンタ昇華でシアンの汚れの割合を示す値、数値。 値は、100 倍の汚れ割合です。 840 として 8.4% の汚れを指定するなど、10% が 1000 とします。</p></td>
<td><p>任意。 指定されていない場合は、Unidrv が指定した既定値が使用されます。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>CyanInYellowDye</strong></p></td>
<td><p>0 ~ 1000、黄色昇華でシアンの汚れの割合を示す値、数値。 値は、100 倍の汚れ割合です。 840 として 8.4% の汚れを指定するなど、10% が 1000 とします。</p></td>
<td><p>任意。 指定されていない場合は、Unidrv が指定した既定値が使用されます。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>EnableGDIColorMapping</strong></p></td>
<td><p><strong>TRUE</strong>または<strong>FALSE</strong>します。 GDI がプリンターのカラー スペースに、表示から色域マッピングを実行する必要があるかどうかを示します。</p></td>
<td><p>任意。 指定されていない場合、既定値は<strong>FALSE</strong>します。 場合<strong>TRUE</strong>、Unidrv HT_FLAG_DO_DEVCLR_XFORM フラグを設定する、 <a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_gdiinfo" data-raw-source="[&lt;strong&gt;GDIINFO&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_gdiinfo)"> <strong>GDIINFO</strong> </a>構造体。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>MagentaInCyanDye</strong></p></td>
<td><p>0 ~ 1000、シアン昇華でマゼンタの汚れの割合を示す値、数値。 値は、100 倍の汚れ割合です。 840 として 8.4% の汚れを指定するなど、10% が 1000 とします。</p></td>
<td><p>任意。 指定されていない場合は、Unidrv が指定した既定値が使用されます。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>MagentaInYellowDye</strong></p></td>
<td><p>0 ~ 1000、黄色の昇華でマゼンタ汚れの割合を示す値、数値。 値は、100 倍の汚れ割合です。 840 として 8.4% の汚れを指定するなど、10% が 1000 とします。</p></td>
<td><p>任意。 指定されていない場合は、Unidrv が指定した既定値が使用されます。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>YellowInCyanDye</strong></p></td>
<td><p>0 ~ 1000、シアン昇華で黄色の汚れの割合を示す値、数値。 値は、100 倍の汚れ割合です。 840 として 8.4% の汚れを指定するなど、10% が 1000 とします。</p></td>
<td><p>任意。 指定されていない場合は、Unidrv が指定した既定値が使用されます。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>YellowInMagentaDye</strong></p></td>
<td><p>0 ~ 1000、マゼンタ昇華で黄色の汚れの割合を示す値、数値。 値は、100 倍の汚れ割合です。 840 として 8.4% の汚れを指定するなど、10% が 1000 とします。</p></td>
<td><p>任意。 指定されていない場合は、Unidrv が指定した既定値が使用されます。</p></td>
</tr>
</tbody>
</table>

 

**注**  ときに、  **\*ChangeColorModeOnDoc でしょうか。** 色属性に設定されて**TRUE**、色の最適化が有効になっています。 この属性を設定すると**FALSE**最適化は行われません。 色の最適化を有効にすると、スプール ファイルの色の存在と色で再生するスプール ファイルスプール ファイルの色の欠如により、モノクロで再生するスプール ファイル。
透かしの色を生成するプラグインでレンダリング Unidrv を作成する場合は、その色の最適化とカラーの透かしドキュメントを白黒で印刷するとき、白黒で印刷するように求められます。 色および白黒ドキュメントをカラーの透かしが正しく印刷することを確認するには、色の最適化を無効にします。

によって制御される色の最適化、  **\*ChangeColorModeOnDoc?** 色属性を設定して制御することも、 **dwColorOptimization**のメンバー、 [ **属性\_情報\_2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/ns-winddiui-_attribute_info_2)または[**属性\_情報\_3** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/ns-winddiui-_attribute_info_3)構造体。 色の最適化も制御できますを使用して、 [ **GdiEndPageEMF** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winppi/nf-winppi-gdiendpageemf)関数。

 

このページに一覧表示の色属性の例については、次を参照してください。、[サンプル GPD ファイル](sample-gpd-files.md)します。

 

 




