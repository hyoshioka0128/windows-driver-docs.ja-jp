---
title: smt
description: Smt 拡張機能は、同時マルチ スレッドのプロセッサ情報の概要を表示します。
ms.assetid: 28c07f89-6208-4b04-b7b9-825dda4f5f5a
keywords:
- Windows デバッグ smt
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- smt
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 803bdeef549c43d9932421871e25246706595c5f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550718"
---
# <a name="smt"></a>! smt


**! Smt**拡張機能は、同時マルチ スレッドのプロセッサ情報の概要を表示します。

```dbgcmd
!smt
```

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>利用不可</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

以下に例を示します。

```dbgcmd
lkd> !smt 
SMT Summary:
------------
   KeActiveProcessors: **------------------------------ (00000003)
        KiIdleSummary: -------------------------------- (00000000)
 No PRCB     Set Master SMT Set                                     IAID
  0 820f4820 Master     **------------------------------ (00000003)  00
  1 87a4d120 820f4820   **------------------------------ (00000003)  01

Maximum cores per physical processor:   2
Maximum logical processors per core:    1
```

**いいえ**列は、プロセッサの数を示します。

**PRCB**列は、プロセッサのプロセッサのコントロール ブロックのアドレスを示します。 各論理プロセッサは個別に一覧表示します。

各物理プロセッサが 1 つの論理プロセッサとして一覧表示、**マスター**下、**設定のマスター**列。

**SMT 設定**列には、プロセッサの同時マルチ スレッドのプロセッサ セットの情報が表示されます。

**IAID**列には、初期のプログラミング可能な 割り込みコント ローラーの高度な識別子 (APIC ID) が表示されます。 ハード コーディングされた初期 APIC ID に置き換えます。 true x64 コンピューターで、各プロセッサを開始 CPUID 命令では、この ID 値を取得できます。 他の特定のコンピューターで APIC のメモリがマップされた入力/出力 (MMIO) 領域からアクセス可能な APIC ID を変更できるように最初の APIC ID はすべてのプロセッサ間で一意である必要ありません。 この手法には、ソフトウェア、コンピューター内のすべてのプロセッサに対して一意の APIC Id を割り当てることができます。 対象のコンピュータのプロセッサに応じて、 **IAID**列は、この ID を表示することがありますまたは空白にすることがあります。

 

 





