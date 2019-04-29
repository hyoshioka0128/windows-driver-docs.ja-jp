---
title: ドライバーの浮動小数点注釈
description: 注釈がコード分析ツールを浮動小数点の使用を検出できます。 浮動小数点では、カーネル モード コードをポイントし、浮動小数点状態が適切に保護されていない場合、エラーを報告できます。 浮動小数点のルールは、カーネル モード コードに対してのみチェックされます。
ms.assetid: 86FF1A21-674F-4BDA-AC03-C1E5F06A4439
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45f5d626d7c43d231514d92b98d96671e6a03754
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329706"
---
# <a name="floating-point-annotations-for-drivers"></a>ドライバーの浮動小数点注釈


注釈がコード分析ツールを浮動小数点の使用を検出できます。 浮動小数点では、カーネル モード コードをポイントし、浮動小数点状態が適切に保護されていない場合、エラーを報告できます。 浮動小数点のルールは、カーネル モード コードに対してのみチェックされます。

いくつかのプロセッサ ファミリは、カーネル モード コード内から浮動小数点演算を使用して、プロセッサは、のスコープ内でのみ行う必要がある x86 特には関数を保存して、浮動小数点状態を復元します。 この規則の違反は実行時に問題が発生することのみ散発されます (ただし、これらの問題を非常に深刻なことができる) ために見つけることは困難にすることはできます。 注釈の適切に使用して、コード分析ツールは、カーネル モード コードで浮動小数点の使用を検出し、エラーを報告する浮動小数点状態が適切に保護されていない場合に効果的です。 浮動小数点のルールは、カーネル モード コードに対してのみチェックされます。

浮動小数点状態とその実行内容を示す関数のパラメーターには、次の注釈を追加します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">浮動小数点の注釈</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="_Kernel_float_saved_"></span><span id="_kernel_float_saved_"></span><span id="_KERNEL_FLOAT_SAVED_"></span><em>Kernel_float_saved</em></p></td>
<td align="left"><p>注釈付きの関数は、関数が正常に返されるときに、浮動小数点演算ハードウェアの状態を保存します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="_Kernel_float_restored_"></span><span id="_kernel_float_restored_"></span><span id="_KERNEL_FLOAT_RESTORED_"></span><em>Kernel_float_restored</em></p></td>
<td align="left"><p>注釈付きの関数は、関数が正常に返されるときに、浮動小数点演算ハードウェアの状態を復元します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="_Kernel_float_used_"></span><span id="_kernel_float_used_"></span><span id="_KERNEL_FLOAT_USED_"></span><em>Kernel_float_used</em></p></td>
<td align="left"><p>使用することができます、関数は呼び出し元関数によって安全に呼び出された場合、 <em>Kernel_float_used</em>エラーの報告を抑制する注釈。 ただし、呼び出し元の関数がでも注釈がない場合<em>Kernel_float_used</em>で注釈を付ける関数の間で関数呼び出しが存在しないまたは<em>Kernel_float_saved と _Kernel_float_restored</em>、それぞれ、コード分析ツールは、エラーが報告されます。</p></td>
</tr>
</tbody>
</table>



これらの注釈は既に KeSaveFloatingPoint 状態を取得して、リークを防ぐためにリソースを解放するための注釈だけでなく、KeRestoreFloatingPointState システム関数適用します。 類似した EngXxx 関数もこの方法で注釈が付いています。 ただし、これらの関数をラップする関数は、これらの注釈も使用する必要があります。

関数の注釈を付けることができます、全体としての関数がいくつかの呼び出し元関数によって安全に呼び出されると、\_カーネル\_float\_使用\_注釈。 これは、警告を抑制し、また、コードを分析ツールを呼び出し元が関数を安全に使用することを確認します。 追加のレベルの\_カーネル\_float\_使用\_追加することができます必要に応じて。 \_カーネル\_float\_使用\_コード分析ツール、関数の結果または関数のパラメーターのいずれかのいずれかが浮動小数点型を悪くはありませんが、指定されたに注釈が自動的には注釈を明示的に指定します。

たとえば、\_カーネル\_float\_保存\_注釈は、浮動小数点状態は KeSaveFloatingPointState システム関数の FloatingState パラメーターに格納されていることを示します。

```ManagedCPlusPlus
_Must_inspect_result_  
_IRQL_requires_max_(DISPATCH_LEVEL)  
__drv_valueIs(<0;==0)  
_When_(return==0, _Kernel_float_saved_)  
_At_(*FloatingState, _Kernel_requires_resource_not_held_(FloatState) _When_(return==0, _Kernel_acquires_resource_(FloatState)))  
__forceinline  
NTSTATUS  
KeSaveFloatingPointState (  
    _Out_ PVOID FloatingState  
    )  
```

次の例では、\_カーネル\_float\_使用\_注釈は、浮動小数点状態の使用方法についての警告を抑制します。 注釈は、分析ツール MyDoesFloatingPoint への呼び出しが安全な浮動小数点のコンテキストで発生することを確認するコードもとします。

```
_Kernel_float_used_
void
    MyDoesFloatingPoint(arguments);
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Windows ドライバーの SAL 2.0 注釈](sal-2-annotations-for-windows-drivers.md)










