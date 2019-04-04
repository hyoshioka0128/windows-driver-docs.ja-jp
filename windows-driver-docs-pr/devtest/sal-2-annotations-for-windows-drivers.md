---
title: Windows ドライバーの SAL 2.0 注釈
description: Microsoft ソース コード注釈言語 (SAL) には、Windows ドライバーの分析と関連のカーネル コードに固有の注釈が含まれています。
ms.assetid: 2CD181B8-4E1D-457A-9FF9-DAB3AB932730
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1311f596f4d96b1db3c3cdb8d27b428043c10070
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532879"
---
# <a name="sal-20-annotations-for-windows-drivers"></a>Windows ドライバーの SAL 2.0 注釈


Microsoft ソース コード注釈言語 (SAL) には、Windows ドライバーの分析と関連のカーネル コードに固有の注釈が含まれています。 注釈の言語は、関数、パラメーター、戻り値、構造、および構造体のフィールドのプロパティを記述する方法を提供します。 注釈は、コメントする、コードを追加、コンパイラによって無視されますが、静的分析ツールを使ってに似ています。 注釈を使用は、開発者の有効性を向上させるのに役立ちます、静的分析の結果の精度を向上させるのに役立ちより適切に特定のバグが存在するかどうかを判断するためのツールを使用します。 ドライバーの注釈は非ドライバーやカーネルに関係のないコードで使用するためのものではありません。 ドライバーの注釈は、Driverspecs.h で定義されます。

**注**  Windows 8 に SAL 1.0 に代わる SAL 2.0 が導入されています。 SAL 2.0 については、[C と C++ コードの欠陥を削減する SAL 注釈を使って](https://go.microsoft.com/fwlink/p/?linkid=247283)を参照してください。 SAL 2.0 には、SAL 1.0 が置き換えられます。 SAL 2.0 が Windows 8 向けに、Windows Driver Kit (WDK) 8 を使用してください。 ドライバーの SAL 1.0 についての情報を必要がある場合は、Windows 7 の WDK に付属するマニュアルを参照してください。

 

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
<th align="left">使用</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em>IRQL_requires_max</em></strong>(<em>value</em>)</p>
<p><strong><em>IRQL_requires_min</em></strong>(<em>value</em>)</p>
<p><strong><em>IRQL_raises</em></strong>(<em>値</em>)</p>
<p><strong><em>IRQL_requires</em></strong>(<em>値</em>)</p>
<p><strong><em>IRQL_raises</em></strong>(<em>値</em>)</p>
<p><strong><em>IRQL_saves</em></strong></p>
<p><strong><em>IRQL_restores</em></strong></p>
<p><strong><em>IRQL_saves_global</em></strong>(<em>種類</em>、 <em>param</em>)</p>
<p><strong><em>IRQL_restores_global</em></strong>(<em>kind</em>, <em>param</em>)</p>
<p><strong><em>IRQL_always_function_min</em></strong>(<em>value</em>)</p>
<p><strong><em>IRQL_always_function_max</em></strong>(<em>value</em>)</p>
<p><strong><em>IRQL_requires_same</em></strong></p></td>
<td align="left"><a href="irql-annotations-for-drivers.md" data-raw-source="[IRQL annotations](irql-annotations-for-drivers.md)">IRQL の注釈</a></td>
<td align="left"><p>IRQL の注釈を使用すると、関数を実行する範囲の IRQL レベルを指定します。 IRQL の注釈には、エラーをより正確に検索するコード分析ツールが役立ちます。</p></td>
</tr>
<tr class="even">
<td align="left"><strong><em>IRQL_is_cancel</em></strong></td>
<td align="left"><a href="irql-annotations-for-drivers.md" data-raw-source="[IRQL annotations](irql-annotations-for-drivers.md)">IRQL の注釈</a></td>
<td align="left"><p>使用して、 <em>IRQL_is_cancel</em>注釈は、の正常な動作を確認できます、 <strong>DRIVER_CANCEL</strong>コールバック関数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>Kernel_float_saved</em></strong></p>
<p><strong><em>Kernel_float_restored</em></strong></p>
<p><strong><em>Kernel_float_used</em></strong></p></td>
<td align="left"><a href="floating-point-annotations-for-drivers.md" data-raw-source="[Floating point annotations for drivers](floating-point-annotations-for-drivers.md)">ドライバーのポイントの注釈を浮動小数点</a></td>
<td align="left"><p>浮動を使用して、浮動小数点のカーネル モード コードとエラーを報告する浮動小数点状態が適切に保護されていない場合の使用を検出するコード分析ツールのヘルプへの注釈をポイントします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><em>Kernel_clear_do_init</em></strong></p></td>
<td align="left"><a href="do-device-initializing-annotation-for-drivers.md" data-raw-source="[DO_DEVICE_INITIALIZING annotation](do-device-initializing-annotation-for-drivers.md)">DO_DEVICE_INITIALIZING 注釈</a></td>
<td align="left"><p>使用して、 <em>Kernel_clear_do_init</em>デバイス オブジェクトの Flags フィールドにビットの注釈を注釈付きの関数は、DO_DEVICE_INITIALIZING をクリアする必要かどうかを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>Kernel_IoGetDmaAdapter</em></strong></p></td>
<td align="left"><a href="-kernel-iogetdmaadapter--annotation-for-drivers.md" data-raw-source="[_Kernel_IoGetDmaAdapter_ Annotation](-kernel-iogetdmaadapter--annotation-for-drivers.md)"><em>Kernel_IoGetDmaAdapter</em>注釈</a></td>
<td align="left"><p>使用して、 <em>Kernel_IoGetDmaAdapter</em> DMA ポインターの誤用を検索するコード分析ツールに出力するための注釈。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><em>Interlocked_operand</em></strong></p></td>
<td align="left"><a href="driver-annotations-for-interlocked-operands.md" data-raw-source="[Annotations for interlocked operands](driver-annotations-for-interlocked-operands.md)">インタロックされたオペランドの注釈</a></td>
<td align="left"><p>使用して、 <em>Interlocked_operand</em>インター ロックのオペランドとして識別する関数のパラメーターの注釈。 関数の数は、そのパラメーターの 1 つとして、インタロックされたプロセッサ命令を使用してアクセスする必要がある変数のアドレスを取得します。 キャッシュ リード スルーのアトミック手順では、これらし、非常に微妙なバグが発生する場合は、オペランドが正しくに使用されていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>Dispatch_type</em></strong></p></td>
<td align="left"><a href="declaring-functions-using-function-role-types-for-wdm-drivers.md#annotating_driver_dispatch_routines" data-raw-source="[Annotations for Driver Dispatch Routines](declaring-functions-using-function-role-types-for-wdm-drivers.md#annotating_driver_dispatch_routines)">ドライバーの注釈のディスパッチ ルーチン</a>します。</td>
<td align="left"><p>使用して、 <em>Dispatch_type</em> WDM ドライバー ディスパッチ ルーチンを宣言するときに使用される注釈。 参照してください<a href="declaring-functions-using-function-role-types-for-wdm-drivers.md" data-raw-source="[Declaring Functions Using Function Role Types for WDM Drivers](declaring-functions-using-function-role-types-for-wdm-drivers.md)">WDM ドライバーのロールの種類の関数を使用して関数の宣言</a>と<a href="declaring-functions-using-function-role-types-for-wdm-drivers.md#annotating_driver_dispatch_routines" data-raw-source="[Annotating Driver Dispatch Routines](declaring-functions-using-function-role-types-for-wdm-drivers.md#annotating_driver_dispatch_routines)">ドライバー ディスパッチ ルーチンに注釈を付ける</a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><em>Flt_CompletionContext_Outptr</em></strong></p></td>
<td align="left"><a href="-flt-completioncontext-outptr--annotation.md" data-raw-source="[_Flt_CompletionContext_Outptr_ Annotation](-flt-completioncontext-outptr--annotation.md)"><em>Flt_CompletionContext_Outptr</em> Annotation</a></td>
<td align="left"><p>使用して、 <strong><em>Flt_CompletionContext_Outptr</em></strong>ファイル システム ミニフィルターの前の操作のコールバック関数を宣言するときに注釈 (<a href="https://msdn.microsoft.com/library/windows/hardware/ff551109" data-raw-source="[&lt;strong&gt;PFLT_PRE_OPERATION_CALLBACK&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551109)"><strong>PFLT_PRE_OPERATION_CALLBACK</strong></a>). この注釈を配置、 <em>CompletionContext</em>パラメーター。 この注釈を設定することを確認するコード分析ツール、 <em>CompletionContext</em> FLT_PREOP_CALLBACK_STATUS が値を返すが正しい。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[SAL 注釈を使用して C/C++ のコード障害を減らす](https://go.microsoft.com/fwlink/p/?linkid=247283)

 

 






