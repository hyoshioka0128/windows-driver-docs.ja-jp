---
title: Windows カーネルのグローバル変数
description: カーネルのグローバル変数。
ms.assetid: 1ea5c4e3-ed70-449c-a49e-b1e3c892e981
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ecaf5b20ac14617420e08e38dad895a204a1bfc5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573735"
---
# <a name="windows-kernel-global-variables"></a>Windows カーネルのグローバル変数


カーネルのグローバル変数。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>変数</th>
<th>宣言</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Mm64BitPhysicalAddress</strong></td>
<td><code>PBOOLEAN Mm64BitPhysicalAddress</code>
<p>Wdm.h で宣言されています。</p></td>
<td><p>ハードウェアとオペレーティング システムが 64 ビットの物理アドレスをサポートするかどうかを指定します。 値が指す<strong>TRUE</strong> 64 ビットの物理アドレスをサポートして、ハードウェアとオペレーティング システムが場合<strong>FALSE</strong>それ以外の場合。</p>
<p>この変数には、ドライバーで使用する方法の詳細については、<a href="performing-dma-in-64-bit-windows.md" data-raw-source="[Performing DMA in 64-Bit Windows](performing-dma-in-64-bit-windows.md)">64 ビット Windows で DMA を実行する</a>を参照してください。</p></td>
</tr>
<tr class="even">
<td><strong>MmBadPointer</strong></td>
<td><code>PVOID MmBadPointer;</code>
<p>Wdm.h で宣言されています。</p></td>
<td><p>無効になることが保証されるメモリ位置へのポインター。</p>
<div class="alert">
<strong>注</strong>以降では、Windows 8.1、 <strong>MmBadPointer</strong>は非推奨とされます。 ドライバーを使用する必要があります、 <a href="mm-bad-pointer.md#mm_bad_pointer" data-raw-source="[&lt;strong&gt;MM_BAD_POINTER&lt;/strong&gt;](mm-bad-pointer.md#mm_bad_pointer)"> <strong>MM_BAD_POINTER</strong> </a>マクロ代わりにします。
</div>
<div>
 
</div>
<p>オペレーティング システムのバグを生成するメモリ アドレスをアドレスがあるかどうかがで指定された、 <strong>MmBadPointer</strong>変数にアクセスします。</p>
<p>使用することができます<strong>MmBadPointer</strong>ドライバー コードをデバッグします。 任意の初期化されていないポインター変数に設定<strong>MmBadPointer</strong>に無効なポインターを逆参照しようとするコードを最初の時間を検索します。</p>
<p>すべてのアドレスの PAGE_SIZE 内<strong>MmBadPointer</strong>無効になることが保証されます。 たとえば場合、<em>アドレス</em>ポインター場合<strong>MmBadPointer</strong> &lt; = <em>アドレス</em> &lt; <strong>MmBadPointer</strong> + PAGE_SIZE、アクセスしようとしました。 *<em>アドレス</em>により、オペレーティング システムは、バグ チェックを生成します。 <strong>MmBadPointer</strong> + PAGE_SIZE は無効になることは保証されません。</p></td>
</tr>
<tr class="odd">
<td><strong>PsInitialSystemProcess</strong></td>
<td><code>PEPROCESS PsInitialSystemProcess;</code>
<p>Ntddk.h で宣言されています。</p></td>
<td><p>指す、 <a href="eprocess.md" data-raw-source="[&lt;strong&gt;EPROCESS&lt;/strong&gt;](eprocess.md)"> <strong>」プロセス</strong></a>システム プロセスの構造体。</p></td>
</tr>
<tr class="even">
<td><strong>NLS_MB_CODE_PAGE_TAG</strong></td>
<td><code>extern BOOLEAN  NLS_MB_CODE_PAGE_TAG;</code></td>
<td><p>コード ページが 1 バイトまたはマルチバイト コード ページであるかどうかを指定します。</p>
<p><strong>NLS_MB_CODE_PAGE_TAG</strong>は<strong>TRUE</strong>のマルチバイト コード ページと<strong>FALSE</strong>の 1 バイト コード ページ。</p>
<p>NLS_MB_CODE_PAGE_TAG はシステム用に予約されています。 ユーザー モードから呼び出して<a href="https://go.microsoft.com/fwlink/p/?linkid=121902" data-raw-source="[GetCPInfoEx](https://go.microsoft.com/fwlink/p/?linkid=121902)">GetCPInfoEx</a>代わりにします。</p>
<p>可能であれば、アプリケーションは、コード ページではなく Unicode を使用する必要があります。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[**」プロセス**](eprocess.md)  
[GetCPInfoEx](https://go.microsoft.com/fwlink/p/?linkid=121902)  
[**MM\_不良\_ポインター**](mm-bad-pointer.md#mm_bad_pointer)  
[64 ビット Windows で DMA を実行します。](performing-dma-in-64-bit-windows.md)  



