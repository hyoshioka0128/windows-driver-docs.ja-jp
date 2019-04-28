---
title: x64 の手順
description: x64 の手順
ms.assetid: f05cbf3e-001c-43cc-8a53-0e22fd161a53
keywords:
- x64 プロセッサで命令
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 864abf8d4d44426f90f580b209b66e8fd78f3581
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381916"
---
# <a name="x64-instructions"></a>x64 の手順


## <span id="ddk_x64_instructions_dbg"></span><span id="DDK_X64_INSTRUCTIONS_DBG"></span>


ほとんどの x86 命令が 64 ビット モードで x64 に対して有効である続けます。 不要になったに、64 ビット モードではいくつかほとんど使用されていない操作はなどサポートされます。

-   10 進数の算術命令: バイナリ-コード化されました。AAA、AAD、AAM、AAS、DAA、DAS

-   バインドされています。

-   PUSHAD と POPAD

-   ほとんどの操作を扱うには、DS のプッシュやポップ DS などのレジスタがセグメント化します。 (FS または GS セグメントのレジスタを使用する操作は、現在も有効です)。

X64 命令セットには、x86、SSE 2 などに最近追加されたものが含まれています。 X64 用にコンパイルされたプログラムは、次の手順を自由に使用できます。

### <a name="span-iddatatransferspanspan-iddatatransferspanspan-iddatatransferspandata-transfer"></a><span id="Data_Transfer"></span><span id="data_transfer"></span><span id="DATA_TRANSFER"></span>データ転送

X64 では、64 ビットの即時定数またはメモリ アドレスを処理できる MOV 命令の新しいバリエーションを提供します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>MOV</p></td>
<td align="left"><p><strong>r</strong>,#n</p></td>
<td align="left"><p><strong>r</strong> = #n</p></td>
</tr>
<tr class="even">
<td align="left"><p>MOV</p></td>
<td align="left"><p><strong>rax</strong>、m</p></td>
<td align="left"><p>64 ビット アドレスでコンテンツを移動<strong>rax</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MOV</p></td>
<td align="left"><p>m, <strong>rax</strong></p></td>
<td align="left"><p>コンテンツを移動<strong>rax</strong>を 64 ビットのアドレス。</p></td>
</tr>
</tbody>
</table>

 

X64 では、64 ビットのオペランドは 32 ビットの符号拡張、新規の命令も提供します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>MOVSXD</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>r</strong>/m</p></td>
<td align="left"><p>DWORD を符号拡張と共に QWORD に移動します。</p></td>
</tr>
</tbody>
</table>

 

32 ビット subregisters 自動的に 0 に通常の MOV 操作は、MOVZXD 命令がないために、64 ビットを拡張します。

メモリからには、128 ビットの値 (Guid) などを移動する 2 つの SSE 命令を使用できます、**xmm * * * n*登録またはその逆です。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>MOVDQA</p></td>
<td align="left"><p><strong>r1</strong>/m、 <strong>r2</strong>/m</p></td>
<td align="left"><p>128 ビットの固定値に移動<strong>xmm</strong><em>n</em>登録、またはその逆です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MOVDQU</p></td>
<td align="left"><p><strong>r1</strong>/m、 <strong>r2</strong>/m</p></td>
<td align="left"><p>(配置ではなく) 128 ビット値の移動を登録、またはその逆。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddataconversionspanspan-iddataconversionspanspan-iddataconversionspandata-conversion"></a><span id="Data_Conversion"></span><span id="data_conversion"></span><span id="DATA_CONVERSION"></span>データ変換

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>CDQE</p></td>
<td align="left"><p>Dword を変換 (<strong>eax</strong>) には、qword (<strong>rax</strong>)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>CQO</p></td>
<td align="left"><p>qword の変換 (<strong>rax</strong>) oword に (<strong>rdx</strong>:<strong>rax</strong>)。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idstringmanipulationspanspan-idstringmanipulationspanspan-idstringmanipulationspanstring-manipulation"></a><span id="String_Manipulation"></span><span id="string_manipulation"></span><span id="STRING_MANIPULATION"></span>文字列操作

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>MOVSQ</p></td>
<td align="left"><p>移動から qword <strong>rsi</strong>に<strong>rdi します。</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>CMPSQ</p></td>
<td align="left"><p>比較では qword <strong>rsi</strong>で<strong>rdi します。</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>SCASQ</p></td>
<td align="left"><p>スキャンでは qword <strong>rdi</strong>します。 比較では qword <strong>rdi</strong>に<strong>rax</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>LODSQ</p></td>
<td align="left"><p>Qword から読み込む<strong>rsi</strong>に<strong>rax</strong><em>します。</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p>STOSQ</p></td>
<td align="left"><p>格納する qword <strong>rdi</strong>から<strong>rax</strong><em>します。</em></p></td>
</tr>
</tbody>
</table>

 

 

 





