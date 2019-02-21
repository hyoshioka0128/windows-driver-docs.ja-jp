---
title: GDI の浮動小数点サービス
description: GDI の浮動小数点サービス
ms.assetid: 7e32c683-ffad-4a95-9c3a-6716f7ce20cb
keywords:
- GDI WDK Windows 2000 の表示、浮動小数点演算
- グラフィックス ドライバー WDK Windows 2000 の表示、浮動小数点演算
- WDK GDI、浮動小数点演算の描画
- 浮動小数点演算 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04f60fc29e5c710d31895016089e3b9a4887b736
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537134"
---
# <a name="gdi-floating-point-services"></a>GDI の浮動小数点サービス


## <span id="ddk_gdi_floating_point_services_gg"></span><span id="DDK_GDI_FLOATING_POINT_SERVICES_GG"></span>


グラフィックスのカーネル モード ドライバーは、GDI が指定した呼び出しの間でのすべての浮動小数点演算を行う必要があります[ **EngSaveFloatingPointState** ](https://msdn.microsoft.com/library/windows/hardware/ff565010)と[ **EngRestoreFloatingPointState** ](https://msdn.microsoft.com/library/windows/hardware/ff565006)ルーチン。

ハードウェアの浮動小数点プロセッサの場合、ドライバーは浮動小数点演算を直接実行できます。 それ以外の場合、ドライバーは、GDI を使用できます[ **FLOATOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff565804)浮動小数点演算をエミュレートするために次の表に示したサービス。 プロセッサの種類に関係なく、ドライバーは浮動小数点値を宣言するときに、FLOATL データ型を使用する必要があります。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565006" data-raw-source="[&lt;strong&gt;EngRestoreFloatingPointState&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565006)"><strong>EngRestoreFloatingPointState</strong></a></p></td>
<td align="left"><p>Windows 2000 や以降のカーネル浮動小数点の状態、ドライバーは、浮動小数点を使用した後、MMX ハードウェア命令を復元します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565010" data-raw-source="[&lt;strong&gt;EngSaveFloatingPointState&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565010)"><strong>EngSaveFloatingPointState</strong></a></p></td>
<td align="left"><p>現在の Windows 2000 およびそれ以降のカーネルの浮動小数点状態を保存します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565814" data-raw-source="[&lt;strong&gt;FLOATOBJ_Add&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565814)"><strong>FLOATOBJ_Add</strong></a></p></td>
<td align="left"><p>2 つの FLOATOBJs を追加します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565822" data-raw-source="[&lt;strong&gt;FLOATOBJ_AddFloat&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565822)"><strong>FLOATOBJ_AddFloat</strong></a></p></td>
<td align="left"><p>FLOATOBJ と FLOATL を追加します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565826" data-raw-source="[&lt;strong&gt;FLOATOBJ_AddLong&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565826)"><strong>FLOATOBJ_AddLong</strong></a></p></td>
<td align="left"><p>FLOATOBJ され、長いを追加します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565835" data-raw-source="[&lt;strong&gt;FLOATOBJ_Div&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565835)"><strong>FLOATOBJ_Div</strong></a></p></td>
<td align="left"><p>別の 1 つ FLOATOBJ を分割します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565841" data-raw-source="[&lt;strong&gt;FLOATOBJ_DivFloat&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565841)"><strong>FLOATOBJ_DivFloat</strong></a></p></td>
<td align="left"><p>FLOATL、FLOATOBJ で除算します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565845" data-raw-source="[&lt;strong&gt;FLOATOBJ_DivLong&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565845)"><strong>FLOATOBJ_DivLong</strong></a></p></td>
<td align="left"><p>LONG、FLOATOBJ で除算します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565861" data-raw-source="[&lt;strong&gt;FLOATOBJ_Equal&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565861)"><strong>FLOATOBJ_Equal</strong></a></p></td>
<td align="left"><p>2 つの FLOATOBJs が等しいかどうかを判断します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565870" data-raw-source="[&lt;strong&gt;FLOATOBJ_EqualLong&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565870)"><strong>FLOATOBJ_EqualLong</strong></a></p></td>
<td align="left"><p>FLOATOBJ され、長いが等しいかどうかを判断します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565871" data-raw-source="[&lt;strong&gt;FLOATOBJ_GetFloat&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565871)"><strong>FLOATOBJ_GetFloat</strong></a></p></td>
<td align="left"><p>計算し、FLOATOBJ の float 型と同じ値を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565873" data-raw-source="[&lt;strong&gt;FLOATOBJ_GetLong&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565873)"><strong>FLOATOBJ_GetLong</strong></a></p></td>
<td align="left"><p>計算し、FLOATOBJ の時間の長いと同等の値を返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565880" data-raw-source="[&lt;strong&gt;FLOATOBJ_GreaterThan&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565880)"><strong>FLOATOBJ_GreaterThan</strong></a></p></td>
<td align="left"><p>1 つ FLOATOBJ が他よりも大きいかどうかを判断します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565884" data-raw-source="[&lt;strong&gt;FLOATOBJ_GreaterThanLong&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565884)"><strong>FLOATOBJ_GreaterThanLong</strong></a></p></td>
<td align="left"><p>FLOATOBJ が長整数型よりも大きいかどうかを判断します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565894" data-raw-source="[&lt;strong&gt;FLOATOBJ_LessThan&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565894)"><strong>FLOATOBJ_LessThan</strong></a></p></td>
<td align="left"><p>1 つ FLOATOBJ が他よりも小さいかどうかを判断します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565902" data-raw-source="[&lt;strong&gt;FLOATOBJ_LessThanLong&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565902)"><strong>FLOATOBJ_LessThanLong</strong></a></p></td>
<td align="left"><p>FLOATOBJ が長整数型よりも小さいかどうかを判断します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565908" data-raw-source="[&lt;strong&gt;FLOATOBJ_Mul&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565908)"><strong>FLOATOBJ_Mul</strong></a></p></td>
<td align="left"><p>2 つの FLOATOBJ 値を乗算します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565914" data-raw-source="[&lt;strong&gt;FLOATOBJ_MulFloat&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565914)"><strong>FLOATOBJ_MulFloat</strong></a></p></td>
<td align="left"><p>によって、FLOATL の FLOATOBJ を乗算します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565916" data-raw-source="[&lt;strong&gt;FLOATOBJ_MulLong&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565916)"><strong>FLOATOBJ_MulLong</strong></a></p></td>
<td align="left"><p>長整数型で、FLOATOBJ を乗算します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565919" data-raw-source="[&lt;strong&gt;FLOATOBJ_Neg&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565919)"><strong>FLOATOBJ_Neg</strong></a></p></td>
<td align="left"><p>FLOATOBJ の符号を変更します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565922" data-raw-source="[&lt;strong&gt;FLOATOBJ_SetFloat&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565922)"><strong>FLOATOBJ_SetFloat</strong></a></p></td>
<td align="left"><p>FLOATOBJ FLOATL の特定の値に設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565928" data-raw-source="[&lt;strong&gt;FLOATOBJ_SetLong&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565928)"><strong>FLOATOBJ_SetLong</strong></a></p></td>
<td align="left"><p>FLOATOBJ を long 型の特定の値に設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565935" data-raw-source="[&lt;strong&gt;FLOATOBJ_Sub&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565935)"><strong>FLOATOBJ_Sub</strong></a></p></td>
<td align="left"><p>別の 1 つ FLOATOBJ を減算します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565938" data-raw-source="[&lt;strong&gt;FLOATOBJ_SubFloat&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565938)"><strong>FLOATOBJ_SubFloat</strong></a></p></td>
<td align="left"><p>FLOATOBJ の FLOATL を減算します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565941" data-raw-source="[&lt;strong&gt;FLOATOBJ_SubLong&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565941)"><strong>FLOATOBJ_SubLong</strong></a></p></td>
<td align="left"><p>LONG FLOATOBJ からを減算します。</p></td>
</tr>
</tbody>
</table>

 

 

 





