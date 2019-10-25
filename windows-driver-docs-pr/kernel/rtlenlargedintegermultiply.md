---
title: Windows カーネル ランタイム ライブラリの古いルーチン
description: Windows カーネル ランタイム ライブラリの古いルーチン
ms.assetid: cd9aa441-a7f2-42b1-8319-611bf53c995d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8483871000f19484106d3eb358532988efd156fb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836409"
---
# <a name="windows-kernel-run-time-library-obsolete-routines"></a>Windows カーネル ランタイム ライブラリの古いルーチン


次のランタイムライブラリの古いルーチンは、既存のドライバーバイナリをサポートするためにエクスポートされます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>廃止されたルーチン</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>RtlEnlargedIntegerMultiply</strong></td>
<td><p>パフォーマンスを向上させるために、結果が32ビット符号付き整数になる場合は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongmult" data-raw-source="[&lt;strong&gt;RtlLongMult&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongmult)"><strong>RtlLongMult</strong></a>ルーチンを使用します。 それ以外の場合は、64ビット整数演算のコンパイラサポートを使用します。</p></td>
</tr>
<tr class="even">
<td><strong>RtlEnlargedUnsignedDivide</strong></td>
<td><p>パフォーマンスを向上させるには、64ビット整数演算のコンパイラサポートを使用します。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlEnlargedUnsignedMultiply</strong></td>
<td><p>パフォーマンスを向上させるために、結果が32ビットの符号なし整数に適合する場合は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongmult" data-raw-source="[&lt;strong&gt;RtlULongMult&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongmult)"><strong>RtlULongMult</strong></a>ルーチンを使用します。 それ以外の場合は、64ビット整数演算のコンパイラサポートを使用します。</p></td>
</tr>
<tr class="even">
<td><strong>Rtlextended整数乗算</strong></td>
<td><p>パフォーマンスを向上させるには、64ビット整数演算のコンパイラサポートを使用します。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlExtendedLargeIntegerDivide</strong></td>
<td><p>パフォーマンスを向上させるには、64ビット整数演算のコンパイラサポートを使用します。</p></td>
</tr>
<tr class="even">
<td><strong>RtlExtendedMagicDivide</strong></td>
<td><p>パフォーマンスを向上させるには、64ビット整数演算のコンパイラサポートを使用します。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlFillBytes</strong></td>
<td><p>呼び出し元が指定したバッファーに、指定した符号なし文字を格納します。 代わりに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlfillmemory" data-raw-source="[&lt;strong&gt;RtlFillMemory&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlfillmemory)"><strong>Rtlfillmemory</strong></a>を使用してください。</p></td>
</tr>
<tr class="even">
<td><strong>Rtllarge整数の追加</strong></td>
<td><p>パフォーマンスを向上させるには、64ビット整数演算のコンパイラサポートを使用します。</p></td>
</tr>
<tr class="odd">
<td><strong>Rtllarge整数と</strong></td>
<td><p>パフォーマンスを向上させるには、64ビット整数演算のコンパイラサポートを使用します。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerArithmeticShift</strong></td>
<td><p>パフォーマンスを向上させるには、64ビット整数演算のコンパイラサポートを使用します。</p></td>
</tr>
<tr class="odd">
<td><strong>Rtllarge整数除算</strong></td>
<td><p>パフォーマンスを向上させるには、64ビット整数演算のコンパイラサポートを使用します。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerEqualTo</strong></td>
<td><p>パフォーマンスを向上させるには、64ビット整数演算のコンパイラサポートを使用します。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlLargeIntegerEqualToZero</strong></td>
<td><p>パフォーマンスを向上させるには、64ビット整数演算のコンパイラサポートを使用します。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerGreaterOrEqualToZero</strong></td>
<td><p>パフォーマンスを向上させるには、64ビット整数演算のコンパイラサポートを使用します。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlLargeIntegerGreaterThan</strong></td>
<td><p>パフォーマンスを向上させるには、64ビット整数演算のコンパイラサポートを使用します。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerGreaterThanOrEqualTo</strong></td>
<td><p>パフォーマンスを向上させるには、64ビット整数演算のコンパイラサポートを使用します。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlLargeIntegerGreaterThanZero</strong></td>
<td><p>パフォーマンスを向上させるには、64ビット整数演算のコンパイラサポートを使用します。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerLessOrEqualToZero</strong></td>
<td><p>パフォーマンスを向上させるには、64ビット整数演算のコンパイラサポートを使用します。</p></td>
</tr>
<tr class="odd">
<td><strong>Rtllarge整数は、</strong></td>
<td><p>パフォーマンスを向上させるには、64ビット整数演算のコンパイラサポートを使用します。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerLessThanOrEqualTo</strong></td>
<td><p>パフォーマンスを向上させるには、64ビット整数演算のコンパイラサポートを使用します。</p></td>
</tr>
<tr class="odd">
<td><strong>Rtllarge整数はゼロではありません</strong></td>
<td><p>パフォーマンスを向上させるには、64ビット整数演算のコンパイラサポートを使用します。</p></td>
</tr>
<tr class="even">
<td><strong>Rtllarge整数の符号を反転します。</strong></td>
<td><p>パフォーマンスを向上させるには、64ビット整数演算のコンパイラサポートを使用します。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlLargeIntegerNotEqualTo</strong></td>
<td><p>パフォーマンスを向上させるには、64ビット整数演算のコンパイラサポートを使用します。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerNotEqualToZero</strong></td>
<td><p>パフォーマンスを向上させるには、64ビット整数演算のコンパイラサポートを使用します。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlLargeIntegerShiftLeft</strong></td>
<td><p>パフォーマンスを向上させるには、64ビット整数演算のコンパイラサポートを使用します。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerShiftRight</strong></td>
<td><p>パフォーマンスを向上させるには、64ビット整数演算のコンパイラサポートを使用します。</p></td>
</tr>
<tr class="odd">
<td><strong>Rtllarge整数減算</strong></td>
<td><p>パフォーマンスを向上させるには、64ビット整数演算のコンパイラサポートを使用します。</p></td>
</tr>
<tr class="even">
<td><strong>RtlZeroBytes</strong></td>
<td><p>ブロックへのポインターと、入力する長さ (バイト単位) を指定して、メモリブロックに0を設定します。 パフォーマンスを向上させるには、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlzeromemory" data-raw-source="[&lt;strong&gt;RtlZeroMemory&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlzeromemory)"><strong>Rtlゼロメモリ</strong></a>を使用します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[**RtlFillMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlfillmemory)  
[**RtlLongMult**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntintsafe/nf-ntintsafe-rtlulongmult)  
[**Rtlゼロメモリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlzeromemory)  



