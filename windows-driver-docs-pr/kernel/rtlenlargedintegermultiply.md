---
title: Windows カーネル ランタイム ライブラリの古いルーチン
description: Windows カーネル ランタイム ライブラリの古いルーチン
ms.assetid: cd9aa441-a7f2-42b1-8319-611bf53c995d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 288b4145db7542de3dec4a22e0e33e4eeedb1837
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373398"
---
# <a name="windows-kernel-run-time-library-obsolete-routines"></a>Windows カーネル ランタイム ライブラリの古いルーチン


既存のドライバー バイナリをサポートするために、次のランタイム ライブラリの古いルーチンがエクスポートされます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>古いルーチン</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>RtlEnlargedIntegerMultiply</strong></td>
<td><p>パフォーマンスの向上のため、使用して、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntintsafe/nf-ntintsafe-rtlulongmult" data-raw-source="[&lt;strong&gt;RtlLongMult&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntintsafe/nf-ntintsafe-rtlulongmult)"> <strong>RtlLongMult</strong> </a>ルーチンの場合は、結果は 32 ビット符号付き整数に表示されます。 それ以外の場合、64 ビット整数演算のコンパイラ サポートを使用します。</p></td>
</tr>
<tr class="even">
<td><strong>RtlEnlargedUnsignedDivide</strong></td>
<td><p>パフォーマンスの向上のためには、64 ビット整数演算のコンパイラ サポートを使用します。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlEnlargedUnsignedMultiply</strong></td>
<td><p>パフォーマンスの向上のため、使用して、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntintsafe/nf-ntintsafe-rtlulongmult" data-raw-source="[&lt;strong&gt;RtlULongMult&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntintsafe/nf-ntintsafe-rtlulongmult)"> <strong>RtlULongMult</strong> </a>ルーチンの場合は、結果は 32 ビット符号なし整数に表示されます。 それ以外の場合、64 ビット整数演算のコンパイラ サポートを使用します。</p></td>
</tr>
<tr class="even">
<td><strong>RtlExtendedIntegerMultiply</strong></td>
<td><p>パフォーマンスの向上のためには、64 ビット整数演算のコンパイラ サポートを使用します。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlExtendedLargeIntegerDivide</strong></td>
<td><p>パフォーマンスの向上のためには、64 ビット整数演算のコンパイラ サポートを使用します。</p></td>
</tr>
<tr class="even">
<td><strong>RtlExtendedMagicDivide</strong></td>
<td><p>パフォーマンスの向上のためには、64 ビット整数演算のコンパイラ サポートを使用します。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlFillBytes</strong></td>
<td><p>呼び出し元が指定のバッファーを指定した符号なし文字に設定します。 使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlfillmemory" data-raw-source="[&lt;strong&gt;RtlFillMemory&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlfillmemory)"> <strong>RtlFillMemory</strong> </a>代わりにします。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerAdd</strong></td>
<td><p>パフォーマンスの向上のためには、64 ビット整数演算のコンパイラ サポートを使用します。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlLargeIntegerAnd</strong></td>
<td><p>パフォーマンスの向上のためには、64 ビット整数演算のコンパイラ サポートを使用します。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerArithmeticShift</strong></td>
<td><p>パフォーマンスの向上のためには、64 ビット整数演算のコンパイラ サポートを使用します。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlLargeIntegerDivide</strong></td>
<td><p>パフォーマンスの向上のためには、64 ビット整数演算のコンパイラ サポートを使用します。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerEqualTo</strong></td>
<td><p>パフォーマンスの向上のためには、64 ビット整数演算のコンパイラ サポートを使用します。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlLargeIntegerEqualToZero</strong></td>
<td><p>パフォーマンスの向上のためには、64 ビット整数演算のコンパイラ サポートを使用します。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerGreaterOrEqualToZero</strong></td>
<td><p>パフォーマンスの向上のためには、64 ビット整数演算のコンパイラ サポートを使用します。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlLargeIntegerGreaterThan</strong></td>
<td><p>パフォーマンスの向上のためには、64 ビット整数演算のコンパイラ サポートを使用します。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerGreaterThanOrEqualTo</strong></td>
<td><p>パフォーマンスの向上のためには、64 ビット整数演算のコンパイラ サポートを使用します。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlLargeIntegerGreaterThanZero</strong></td>
<td><p>パフォーマンスの向上のためには、64 ビット整数演算のコンパイラ サポートを使用します。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerLessOrEqualToZero</strong></td>
<td><p>パフォーマンスの向上のためには、64 ビット整数演算のコンパイラ サポートを使用します。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlLargeIntegerLessThan</strong></td>
<td><p>パフォーマンスの向上のためには、64 ビット整数演算のコンパイラ サポートを使用します。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerLessThanOrEqualTo</strong></td>
<td><p>パフォーマンスの向上のためには、64 ビット整数演算のコンパイラ サポートを使用します。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlLargeIntegerLessThanZero</strong></td>
<td><p>パフォーマンスの向上のためには、64 ビット整数演算のコンパイラ サポートを使用します。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerNegate</strong></td>
<td><p>パフォーマンスの向上のためには、64 ビット整数演算のコンパイラ サポートを使用します。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlLargeIntegerNotEqualTo</strong></td>
<td><p>パフォーマンスの向上のためには、64 ビット整数演算のコンパイラ サポートを使用します。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerNotEqualToZero</strong></td>
<td><p>パフォーマンスの向上のためには、64 ビット整数演算のコンパイラ サポートを使用します。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlLargeIntegerShiftLeft</strong></td>
<td><p>パフォーマンスの向上のためには、64 ビット整数演算のコンパイラ サポートを使用します。</p></td>
</tr>
<tr class="even">
<td><strong>RtlLargeIntegerShiftRight</strong></td>
<td><p>パフォーマンスの向上のためには、64 ビット整数演算のコンパイラ サポートを使用します。</p></td>
</tr>
<tr class="odd">
<td><strong>RtlLargeIntegerSubtract</strong></td>
<td><p>パフォーマンスの向上のためには、64 ビット整数演算のコンパイラ サポートを使用します。</p></td>
</tr>
<tr class="even">
<td><strong>RtlZeroBytes</strong></td>
<td><p>ブロックおよび長さを格納するバイト数で指定してポインター ゼロ メモリのブロックを設定します。 パフォーマンスの向上のため、使用して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlzeromemory" data-raw-source="[&lt;strong&gt;RtlZeroMemory&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlzeromemory)"> <strong>RtlZeroMemory</strong></a>します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[**RtlFillMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlfillmemory)  
[**RtlLongMult**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntintsafe/nf-ntintsafe-rtlulongmult)  
[**RtlZeroMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlzeromemory)  



