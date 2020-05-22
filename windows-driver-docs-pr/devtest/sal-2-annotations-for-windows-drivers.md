---
title: Windows ドライバーの SAL 2.0 注釈
description: Microsoft ソースコード注釈言語 (SAL) には、Windows ドライバーおよび関連するカーネルコードの分析に固有の注釈が含まれています。
ms.assetid: 2CD181B8-4E1D-457A-9FF9-DAB3AB932730
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f8190ca3fff8f6daeec928d033d25529335152a
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769718"
---
# <a name="sal-20-annotations-for-windows-drivers"></a>Windows ドライバーの SAL 2.0 注釈


Microsoft ソースコード注釈言語 (SAL) には、Windows ドライバーおよび関連するカーネルコードの分析に固有の注釈が含まれています。 注釈言語は、関数、パラメーター、戻り値、構造体、および構造体の各フィールドのプロパティを記述する方法を提供します。 注釈は、コードに追加するコメントに似ており、コンパイラでは無視されますが、静的分析ツールで使用されます。 注釈を使用すると、開発者の有効性が向上し、静的な分析によって得られる結果の精度が向上し、特定のバグが存在するかどうかをツールがより適切に判断できるようになります。 ドライバーの注釈は、ドライバー以外のコードまたは非カーネル関連のコードで使用するためのものではありません。 ドライバーの注釈は Driverspecs. h で定義されています。

**メモ**   Windows 8 では、sal 1.0 を置き換える SAL 2.0 が導入されています。 SAL 2.0 の詳細については、「 [Sal 注釈を使用して C/c + + コードの欠陥を減らす](https://docs.microsoft.com/cpp/code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects)」を参照してください。 Sal 2.0 が SAL 1.0 に置き換えられます。 SAL 2.0 は、windows 8 用 Windows Driver Kit (WDK) 8 で使用する必要があります。 ドライバーの SAL 1.0 に関する情報が必要な場合は、Windows 7 用の WDK に付属のドキュメントを参照してください。

 

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ドライバーの注釈</th>
<th align="left">カテゴリ</th>
<th align="left">用途</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em>IRQL_requires_max</em></strong>(<em>値</em>)</p>
<p><strong><em>IRQL_requires_min</em></strong>(<em>値</em>)</p>
<p><strong><em>IRQL_raises</em></strong>(<em>値</em>)</p>
<p><strong><em>IRQL_requires</em></strong>(<em>値</em>)</p>
<p><strong><em>IRQL_raises</em></strong>(<em>値</em>)</p>
<p><strong><em>IRQL_saves</em></strong></p>
<p><strong><em>IRQL_restores</em></strong></p>
<p><strong><em>IRQL_saves_global</em></strong>(<em>kind</em>, <em>param</em>)</p>
<p><strong><em>IRQL_restores_global</em></strong>(<em>kind</em>, <em>param</em>)</p>
<p><strong><em>IRQL_always_function_min</em></strong>(<em>値</em>)</p>
<p><strong><em>IRQL_always_function_max</em></strong>(<em>値</em>)</p>
<p><strong><em>IRQL_requires_same</em></strong></p></td>
<td align="left"><a href="irql-annotations-for-drivers.md" data-raw-source="[IRQL annotations](irql-annotations-for-drivers.md)">IRQL 注釈</a></td>
<td align="left"><p>IRQL 注釈を使用して、関数を実行する IRQL レベルの範囲を指定します。 IRQL 注釈は、コード分析ツールがより正確にエラーを検出するのに役立ちます。</p></td>
</tr>
<tr class="even">
<td align="left"><strong><em>IRQL_is_cancel</em></strong></td>
<td align="left"><a href="irql-annotations-for-drivers.md" data-raw-source="[IRQL annotations](irql-annotations-for-drivers.md)">IRQL 注釈</a></td>
<td align="left"><p><em>IRQL_is_cancel</em>注釈を使用すると、 <strong>DRIVER_CANCEL</strong>コールバック関数の適切な動作を保証できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>Kernel_float_saved</em></strong></p>
<p><strong><em>Kernel_float_restored</em></strong></p>
<p><strong><em>Kernel_float_used</em></strong></p></td>
<td align="left"><a href="floating-point-annotations-for-drivers.md" data-raw-source="[Floating point annotations for drivers](floating-point-annotations-for-drivers.md)">ドライバーの浮動小数点注釈</a></td>
<td align="left"><p>浮動小数点注釈を使用すると、コード分析ツールがカーネルモードコードでの浮動小数点の使用を検出し、浮動小数点の状態が適切に保護されていない場合にエラーを報告するのに役立ちます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><em>Kernel_clear_do_init</em></strong></p></td>
<td align="left"><a href="do-device-initializing-annotation-for-drivers.md" data-raw-source="[DO_DEVICE_INITIALIZING annotation](do-device-initializing-annotation-for-drivers.md)">DO_DEVICE_INITIALIZING 注釈</a></td>
<td align="left"><p><em>Kernel_clear_do_init</em>注釈を使用して、注釈が付けられた関数がデバイスオブジェクトの Flags フィールドの DO_DEVICE_INITIALIZING ビットをクリアする必要があるかどうかを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>Kernel_IoGetDmaAdapter</em></strong></p></td>
<td align="left"><a href="-kernel-iogetdmaadapter--annotation-for-drivers.md" data-raw-source="[_Kernel_IoGetDmaAdapter_ Annotation](-kernel-iogetdmaadapter--annotation-for-drivers.md)"><em>Kernel_IoGetDmaAdapter</em>ゴム</a></td>
<td align="left"><p><em>Kernel_IoGetDmaAdapter</em>注釈を使用して、DMA ポインターの誤用を探すようにコード分析ツールに指示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><em>Interlocked_operand</em></strong></p></td>
<td align="left"><a href="driver-annotations-for-interlocked-operands.md" data-raw-source="[Annotations for interlocked operands](driver-annotations-for-interlocked-operands.md)">インタロックオペランドの注釈</a></td>
<td align="left"><p>関数パラメーターに<em>Interlocked_operand</em>注釈を使用して、それらをインタロックされたオペランドとして識別します。 多くの関数は、インタロックされたプロセッサ命令を使用してアクセスする必要がある変数のアドレスをパラメーターの1つとして受け取ります。 これらはキャッシュ読み取り-アトミック命令です。オペランドが正しく使用されていないと、非常に微妙なバグの結果になります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>Dispatch_type</em></strong></p></td>
<td align="left"><a href="declaring-functions-using-function-role-types-for-wdm-drivers.md#annotating_driver_dispatch_routines" data-raw-source="[Annotations for Driver Dispatch Routines](declaring-functions-using-function-role-types-for-wdm-drivers.md#annotating_driver_dispatch_routines)">ドライバーディスパッチルーチンの注釈</a>。</td>
<td align="left"><p>WDM ドライバーディスパッチルーチンを宣言するときに使用される<em>Dispatch_type</em>注釈を使用します。 「 <a href="declaring-functions-using-function-role-types-for-wdm-drivers.md" data-raw-source="[Declaring Functions Using Function Role Types for WDM Drivers](declaring-functions-using-function-role-types-for-wdm-drivers.md)">WDM ドライバーの関数ロール型を使用した関数の宣言</a>」および「<a href="declaring-functions-using-function-role-types-for-wdm-drivers.md#annotating_driver_dispatch_routines" data-raw-source="[Annotating Driver Dispatch Routines](declaring-functions-using-function-role-types-for-wdm-drivers.md#annotating_driver_dispatch_routines)">ドライバーディスパッチルーチン</a>への注釈の付け」を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><em>Flt_CompletionContext_Outptr</em></strong></p></td>
<td align="left"><a href="-flt-completioncontext-outptr--annotation.md" data-raw-source="[_Flt_CompletionContext_Outptr_ Annotation](-flt-completioncontext-outptr--annotation.md)"><em>Flt_CompletionContext_Outptr</em>ゴム</a></td>
<td align="left"><p>ファイルシステムミニ操作のコールバック関数 (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback" data-raw-source="[&lt;strong&gt;PFLT_PRE_OPERATION_CALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)"><strong>PFLT_PRE_OPERATION_CALLBACK</strong></a>) を宣言する場合は、 <strong><em>Flt_CompletionContext_Outptr</em></strong>注釈を使用します。 この注釈を<em>完了パラメーターに配置します</em>。 この注釈は、コード分析ツールに対して、FLT_PREOP_CALLBACK_STATUS の戻り値につい<em>て、完了した</em>かどうかを確認するように指示します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[C/C++ コードの欠陥を減らすための SAL 注釈の使用](https://docs.microsoft.com/cpp/code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects)

 

 






