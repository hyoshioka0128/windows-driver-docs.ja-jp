---
title: Code Analysis for Drivers の警告
description: Code Analysis for Drivers の警告
ms.assetid: 61dba158-7e1b-42ee-9882-0ba9cef77b3c
keywords:
- PREfast ドライバー WDK、警告の
- 'WDK: PREfast for Drivers の警告'
- 'WDK: PREfast for Drivers のエラー'
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dba77475c1343f224052fde589037e4af12bb47e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560650"
---
# <a name="code-analysis-for-drivers-warnings"></a>Code Analysis for Drivers の警告


このセクションでは、Code Analysis for Drivers ドライバー コードに潜在的なエラーを検出したときの報告される警告の一覧です。 いくつかの警告がカーネル モード コードを意図していて、ユーザー モード ドライバーの分析時に無視することができますに注意してください。

コード Analysis for Drivers は、次の種類の警告を報告します。

-   **一般的な警告**(6000 6999)。C および C++ の構文と一般的なコーディングのプラクティスに潜在的なエラー。 これらの警告の説明は、次を参照してください。 [c/c++ の警告のコード分析](/visualstudio/code-quality/code-analysis-for-c-cpp-warnings)します。

-   **Windows の特定の警告**(28600 28799)。これらの警告は、Windows での使用の特定のパターンに固有のものが、ドライバーに固有ではありません。

-   **ドライバー固有の警告**(28100 28199)。ドライバーの相互作用、アプリケーション、その他のドライバー、およびオペレーティング システムのエラー。

-   **注釈エラー** (28200 28299 および 36000 36999)。これらの警告は、注釈が正しくコード化されたした不適切なコンテキストで使用を示します。 ほとんどの場合のような警告を示して、注釈は、必要な (または) がない効果。

-   **メモリ割り当ての警告**(30029 30035)。これらは、メモリ割り当ての警告です。

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>このセクションでは


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="28101-wrong-function-type.md" data-raw-source="[C28101](28101-wrong-function-type.md)">C28101</a></p></td>
<td align="left"><p>C28101 を警告します。Drivers モジュールは、現在の関数は、正しい種類の関数ではない推定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28110-floating-point-hardware-protect.md" data-raw-source="[C28110](28110-floating-point-hardware-protect.md)">C28110</a></p></td>
<td align="left"><p>C28110 を警告します。ドライバーは、浮動小数点演算ハードウェアの状態を保護する必要があります。 参照してください float 型の使用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28111-floating-point-irql-mismatch.md" data-raw-source="[C28111](28111-floating-point-irql-mismatch.md)">C28111</a></p></td>
<td align="left"><p>C28111 を警告します。浮動小数点状態が保存された IRQL (この復元操作) の現在の IRQL が一致しません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28114-improper-irp-stack-copy.md" data-raw-source="[C28114](28114-improper-irp-stack-copy.md)">C28114</a></p></td>
<td align="left"><p>警告:C28114:初期化をクリアまたは更新する必要がある特定のフィールドのまま、IRP スタック エントリ全体をコピーします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28120-irql-execution-too-low.md" data-raw-source="[C28120](28120-irql-execution-too-low.md)">C28120</a></p></td>
<td align="left"><p>C28120 を警告します。関数は、現在の IRQ レベルで呼び出されるは許可されません。 現在のレベルが低すぎます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28121-irq-execution-too-high.md" data-raw-source="[C28121](28121-irq-execution-too-high.md)">C28121</a></p></td>
<td align="left"><p>C28121 を警告します。関数は、現在の IRQ レベルで呼び出されるは許可されません。 現在のレベルが多すぎます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28122-inconsistent-irq-level-calls-low.md" data-raw-source="[C28122](28122-inconsistent-irq-level-calls-low.md)">C28122</a></p></td>
<td align="left"><p>C28122 を警告します。関数は、低い IRQ レベルで呼び出されるは許可されません。 先行する関数の呼び出しは、この制約と一貫性がありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28123-inconsistent-irq-level-calls-high.md" data-raw-source="[C28123](28123-inconsistent-irq-level-calls-high.md)">C28123</a></p></td>
<td align="left"><p>C28123 を警告します。関数は、高い IRQ レベルで呼び出されるは許可されません。 先行する関数の呼び出しは、この制約と一貫性がありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28124-call-below-minimum-irq-level.md" data-raw-source="[C28124](28124-call-below-minimum-irq-level.md)">C28124</a></p></td>
<td align="left"><p>C28124 を警告します。呼び出しによって、IRQ レベルの分析中の関数で許容される最小値より小さく設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28126-accessmode-param-incorrect.md" data-raw-source="[C28126](28126-accessmode-param-incorrect.md)">C28126</a></p></td>
<td align="left"><p>C28126 を警告します。ObReferenceObject * への AccessMode パラメーターにする必要があります IRP-&gt;requestormode で</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28127-function-routine-mismatch.md" data-raw-source="[C28127](28127-function-routine-mismatch.md)">C28127</a></p></td>
<td align="left"><p>C28127 を警告します。ルーチンとして使用されている関数は、想定される型と一致しないと一致します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28128-structure-member-directly-accessed.md" data-raw-source="[C28128](28128-structure-member-directly-accessed.md)">C28128</a></p></td>
<td align="left"><p>C28128 を警告します。フィールドへのアクセスが直接行われました。 これは、ルーチンによって行われます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28129-assignment-made-to-operand.md" data-raw-source="[C28129](28129-assignment-made-to-operand.md)">C28129</a></p></td>
<td align="left"><p>C28129 を警告します。ビットを設定およびクリアを使用してのみ変更する必要があります、オペランドへの割り当てが確立されて</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28131-driverentry-saving-pointer-to-buffer.md" data-raw-source="[C28131](28131-driverentry-saving-pointer-to-buffer.md)">C28131</a></p></td>
<td align="left"><p>C28131 を警告します。DriverEntry ルーチンは I/O マネージャー バッファーを解放するため、ポインターではなく、引数のコピーを保存する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28132-driver-taking-the-size-of-pointer.md" data-raw-source="[C28132](28132-driver-taking-the-size-of-pointer.md)">C28132</a></p></td>
<td align="left"><p>C28132 を警告します。ポインターのサイズを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28133-ioinitializetimer-is-best-called-from-add-device.md" data-raw-source="[C28133](28133-ioinitializetimer-is-best-called-from-add-device.md)">C28133</a></p></td>
<td align="left"><p>C28133 を警告します。IoInitializeTimer は AddDevice から最もと呼ばれます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28134-pool-tag-type-should-be-integral.md" data-raw-source="[C28134](28134-pool-tag-type-should-be-integral.md)">C28134</a></p></td>
<td align="left"><p>C28134 を警告します。プール タグの種類が整数、いない文字列または文字列ポインターにする必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28135-first-argument-to-kewaitforsingleobject.md" data-raw-source="[C28135](28135-first-argument-to-kewaitforsingleobject.md)">C28135</a></p></td>
<td align="left"><p>C28135 を警告します。Kewaitforsingleobject の 1 の最初の引数がローカル変数の場合は、モード パラメーターは kernelmode であるをする必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28139-argument-operand-should-exactly-match.md" data-raw-source="[C28139](28139-argument-operand-should-exactly-match.md)">C28139</a></p></td>
<td align="left"><p>C28139 を警告します。引数の種類と一致する必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28141-argument-lowers-irq-level.md" data-raw-source="[C28141](28141-argument-lowers-irq-level.md)">C28141</a></p></td>
<td align="left"><p>C28141 を警告します。引数によって IRQ レベルを現在の IRQL では、以下に設定して、この関数は、目的のために使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28143-iomarkirppending-must-return-statuspending.md" data-raw-source="[C28143](28143-iomarkirppending-must-return-statuspending.md)">C28143</a></p></td>
<td align="left"><p>C28143 を警告します。IoMarkIrpPending を呼び出すディスパッチ ルーチンは STATUS_PENDING を返すことも必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28144-cancelirql-should-be-current-irql.md" data-raw-source="[C28144](28144-cancelirql-should-be-current-irql.md)">C28144</a></p></td>
<td align="left"><p>C28144 を警告します。終了時に、Irp の IRQL の時点でのキャンセル ルーチン内&gt;CancelIrql が現在の IRQL をする必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28145-opaque-mdl-structure-should-not-be-modified.md" data-raw-source="[C28145](28145-opaque-mdl-structure-should-not-be-modified.md)">C28145</a></p></td>
<td align="left"><p>C28145 を警告します。不透明な MDL 構造体は、ドライバーによっては変更しないでください。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28146-kernel-mode-drivers-should-use-ntstrsafe.md" data-raw-source="[C28146](28146-kernel-mode-drivers-should-use-ntstrsafe.md)">C28146</a></p></td>
<td align="left"><p>C28146 を警告します。カーネル モード ドライバーでは、strsafe.h ではない、ntstrsafe.h を使用してください。 ソース ファイルで見つかりました</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28147-improper-use-of-default-pool-tag.md" data-raw-source="[C28147](28147-improper-use-of-default-pool-tag.md)">C28147</a></p></td>
<td align="left"><p>C28147 を警告します。既定のプール タグの使用 (&#39; kdD&#39;または&#39;mdW&#39;) この関数の呼び出しのプールのタグ付けの目的が果たせなくなります</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28150-function-causes-irq-level-to-be-set-above-max.md" data-raw-source="[C28150](28150-function-causes-irq-level-to-be-set-above-max.md)">C28150</a></p></td>
<td align="left"><p>C28150 を警告します。関数によって、IRQ レベルを分析する関数の許容最大値より大きい設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28151-illegal-irql-value.md" data-raw-source="[C28151](28151-illegal-irql-value.md)">C28151</a></p></td>
<td align="left"><p>C28151 を警告します。値は、IRQL の有効な値</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28152-do-device-initializing-flag-not-cleared.md" data-raw-source="[C28152](28152-do-device-initializing-flag-not-cleared.md)">C28152</a></p></td>
<td align="left"><p>C28152 を警告します。AddDevice などの関数からの戻り値が予期せず DO_DEVICE_INITIALIZING</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28153-irql-annotation-eval-context.md" data-raw-source="[C28153](28153-irql-annotation-eval-context.md)">C28153</a></p></td>
<td align="left"><p>C28153 を警告します。注釈から IRQL の値をこのコンテキストで評価できませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28156-irql-inconsistent-with-required-irq-value.md" data-raw-source="[C28156](28156-irql-inconsistent-with-required-irq-value.md)">C28156</a></p></td>
<td align="left"><p>C28156 を警告します。実際の IRQL は適切な IRQL と一致しません</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28157-function-irql-never-restored.md" data-raw-source="[C28157](28157-function-irql-never-restored.md)">C28157</a></p></td>
<td align="left"><p>C28157 を警告します。IRQL が復元されたことはありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28158-no-irql-was-saved.md" data-raw-source="[C28158](28158-no-irql-was-saved.md)">C28158</a></p></td>
<td align="left"><p>C28158 を警告します。IRQL は保存されませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28161-exiting-without-right-to-use-floating-hardware.md" data-raw-source="[C28161](28161-exiting-without-right-to-use-floating-hardware.md)">C28161</a></p></td>
<td align="left"><p>C28161 を警告します。浮動小数点演算ハードウェアを使用する権限を取得せずに終了します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28162-exiting-while-holding-right-to-use-floating-hardware.md" data-raw-source="[C28162](28162-exiting-while-holding-right-to-use-floating-hardware.md)">C28162</a></p></td>
<td align="left"><p>C28162 を警告します。浮動小数点演算ハードウェアを使用する権利を保持しているときに終了します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28165-class-function-pointer-mismatch.md" data-raw-source="[C28165](28165-class-function-pointer-mismatch.md)">C28165</a></p></td>
<td align="left"><p>C28165 を警告します。クラスの関数ポインターが関数クラスと一致しません</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28166-function-does-not-restore-irql-value.md" data-raw-source="[C28166](28166-function-does-not-restore-irql-value.md)">C28166</a></p></td>
<td align="left"><p>C28166 を警告します。関数では、関数の開始時し、これを行うために必要な値に、IRQL が復元されません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28167-function-changes-irql-without-restore.md" data-raw-source="[C28167](28167-function-changes-irql-without-restore.md)">C28167</a></p></td>
<td align="left"><p>C28167 を警告します。関数は IRQL を変更し、終了前に、IRQL は復元されません。 変更を反映するようにマーク付けする必要があります。 または IRQL が復元する必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28168-dispatch-function-dispatch-annotation.md" data-raw-source="[C28168](28168-dispatch-function-dispatch-annotation.md)">C28168</a></p></td>
<td align="left"><p>C28168 を警告します。ディスパッチ関数はありません、 <strong><em>Dispatch_type</em></strong>テーブル エントリのディスパッチに一致する注釈</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28169-dispatch-function-does-not-have-proper-annotation.md" data-raw-source="[C28169](28169-dispatch-function-does-not-have-proper-annotation.md)">C28169</a></p></td>
<td align="left"><p>C28169 を警告します。ディスパッチ関数が含まれない<strong><em>Dispatch_type</em></strong>注釈</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28170-pageable-code-macro-not-found.md" data-raw-source="[C28170](28170-pageable-code-macro-not-found.md)">C28170</a></p></td>
<td align="left"><p>C28170 を警告します。関数は、ページング セグメントに宣言されていますが、PAGED_CODE も PAGED_CODE_LOCKED もが見つかりました</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28171-function-has-more-than-one-page-macro-instance.md" data-raw-source="[C28171](28171-function-has-more-than-one-page-macro-instance.md)">C28171</a></p></td>
<td align="left"><p>C28171 を警告します。関数には、PAGED_CODE または PAGED_CODE_LOCKED の 1 つ以上のインスタンス</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28172-function-macros-not-in-paged-segment.md" data-raw-source="[C28172](28172-function-macros-not-in-paged-segment.md)">C28172</a></p></td>
<td align="left"><p>C28172 を警告します。関数は、PAGED_CODE または PAGED_CODE_LOCKED がページング セグメントに宣言されていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28173-function-incorrectly-adapts-to-memory-above-4gb.md" data-raw-source="[C28173](28173-function-incorrectly-adapts-to-memory-above-4gb.md)">C28173</a></p></td>
<td align="left"><p>C28173 を警告します。正しくない 4 GB を超える物理メモリに合わせて、現在の関数が表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28175struct-member-should-not-be-accessed-by-driver.md" data-raw-source="[C28175](28175struct-member-should-not-be-accessed-by-driver.md)">C28175</a></p></td>
<td align="left"><p>C28175 を警告します。構造体のメンバーをドライバーによってアクセスはできません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28176-struct-member-should-not-be-modified-by-driver.md" data-raw-source="[C28176](28176-struct-member-should-not-be-modified-by-driver.md)">C28176</a></p></td>
<td align="left"><p>C28176 を警告します。構造体のメンバーは、ドライバーによっては変更しないでください。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28177-function-annotated-with-more-than-one-class.md" data-raw-source="[C28177](28177-function-annotated-with-more-than-one-class.md)">C28177</a></p></td>
<td align="left"><p>C28177 を警告します。1 つ以上の関数クラスには、関数が付きます。 1 つは無視されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28260-syntax-error-in-function-property.md" data-raw-source="[C28260](28260-syntax-error-in-function-property.md)">C28260</a></p></td>
<td align="left"><p>C28260 を警告します。関数内でのプロパティの解析中に、注釈で構文エラーが見つかりました</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28266-function-property-syntax-error.md" data-raw-source="[C28266](28266-function-property-syntax-error.md)">C28266</a></p></td>
<td align="left"><p>関数内のプロパティの注釈で構文エラーが見つかりました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28268-function-class-does-not-match-typedef.md" data-raw-source="[C28268](28268-function-class-does-not-match-typedef.md)">C28268</a></p></td>
<td align="left"><p>C28268 を警告します。関数の関数クラスが、ここで使用された typedef の関数クラスと一致しません</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28601-avoid-blocking-on-hwnd-broadcast.md" data-raw-source="[C28601](28601-avoid-blocking-on-hwnd-broadcast.md)">C28601</a></p></td>
<td align="left"><p>C28601 を警告します。HWND_BROADCAST でブロックします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28602-avoid-calling-sendmessagetimeout-with-hwnd-broadcast.md" data-raw-source="[C28602](28602-avoid-calling-sendmessagetimeout-with-hwnd-broadcast.md)">C28602</a></p></td>
<td align="left"><p>C28602 を警告します。Sendmessagetimeout HWND_BROADCAST を</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28604-smto-abortifhung-with-0-timeout-.md" data-raw-source="[C28604](28604-smto-abortifhung-with-0-timeout-.md)">C28604</a></p></td>
<td align="left"><p>C28604 を警告します。0 のタイムアウトで、SMTO_ABORTIFHUNG を sendmessagetimeout します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28615-must-call-resetstkoflw-in-except-block.md" data-raw-source="[C28615](28615-must-call-resetstkoflw-in-except-block.md)">C28615</a></p></td>
<td align="left"><p>C28615 を警告します。_ _Try ブロックで _alloca を呼び出すときに、_ _except() ブロックで _resetstkoflw を呼び出す必要があります。 Don&#39;catch() ブロック内から t 呼び出し _resetstkoflw</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28616-multithreaded-av-condition.md" data-raw-source="[C28616](28616-multithreaded-av-condition.md)">C28616</a></p></td>
<td align="left"><p>C28616 を警告します。マルチ スレッド AV 条件</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28617-avoid-using-the-return-value-of-beginthread.md" data-raw-source="[C28617](28617-avoid-using-the-return-value-of-beginthread.md)">C28617</a></p></td>
<td align="left"><p>C28617 を警告します。_Beginthread() の戻り値を使用しないでください。 代わりにします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28623-unsigned-cast-of-getmessagepos-coordinates.md" data-raw-source="[C28623](28623-unsigned-cast-of-getmessagepos-coordinates.md)">C28623</a></p></td>
<td align="left"><p>C28623 を警告します。座標の GetMessagePos() の符号なしのキャスト。 使用してくださいではなく処理するように/GET_Y_LPARAM</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28624-no-release-call-to-match-incremented-refcount.md" data-raw-source="[C28624](28624-no-release-call-to-match-incremented-refcount.md)">C28624</a></p></td>
<td align="left"><p>C28624 を警告します。LResultFromObject からカウントをインクリメントを一致するように Release() への呼び出しはありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28625-sensitive-data-may-be-retained.md" data-raw-source="[C28625](28625-sensitive-data-may-be-retained.md)">C28625</a></p></td>
<td align="left"><p>C28625 を警告します。機密データをクリアするために使用する関数呼び出しは最適化します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28636-calling-localfree-on-non-allocated-pointer.md" data-raw-source="[C28636](28636-calling-localfree-on-non-allocated-pointer.md)">C28636</a></p></td>
<td align="left"><p>C28636 を警告します。呼び出しています、グループ、Dacl または Sacl の呼び出しから取得した未割り当てのポインターで LocalFree を呼び出してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28637-calling-function-in-a-global-initializer-is-unsafe.md" data-raw-source="[C28637](28637-calling-function-in-a-global-initializer-is-unsafe.md)">C28637</a></p></td>
<td align="left"><p>C28637 を警告します。グローバル初期化子内の関数の呼び出しが安全</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28638-function-delayload-stub-is-missing-declaration-.md" data-raw-source="[C28638](28638-function-delayload-stub-is-missing-declaration-.md)">C28638</a></p></td>
<td align="left"><p>警告 C28638: 関数遅延読み込みスタブに対応する宣言がありません</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28639-calling-close-handle-with-string.md" data-raw-source="[C28639](28639-calling-close-handle-with-string.md)">C28639</a></p></td>
<td align="left"><p>C28639 を警告します。呼び出し元の文字列でハンドルを閉じる</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28640-delayload-function-stub-should-be-a-static-function.md" data-raw-source="[C28640](28640-delayload-function-stub-should-be-a-static-function.md)">C28640</a></p></td>
<td align="left"><p>警告 C28640: 関数遅延読み込みスタブは静的関数である必要があります</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28644-return-value-from-dpa-insertptr-not-checked.md" data-raw-source="[C28644](28644-return-value-from-dpa-insertptr-not-checked.md)">C28644</a></p></td>
<td align="left"><p>C28644 を警告します。未チェック DPA_InsertPtr からの戻り値</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28645-messagebox-called-using-the-question-mark-symbol.md" data-raw-source="[C28645](28645-messagebox-called-using-the-question-mark-symbol.md)">C28645</a></p></td>
<td align="left"><p>C28645 を警告します。これは推奨されなく疑問符のメッセージ シンボルを使用して MessageBox が呼び出されました</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28648-pulseevent-is-an-unreliable-function.md" data-raw-source="[C28648](28648-pulseevent-is-an-unreliable-function.md)">C28648</a></p></td>
<td align="left"><p>C28648 を警告します。PulseEvent は信頼性のない関数です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28649-automatic-or-global-stack-arrays-are-never-null.md" data-raw-source="[C28649](28649-automatic-or-global-stack-arrays-are-never-null.md)">C28649</a></p></td>
<td align="left"><p>C28649 を警告します。自動またはグローバル スタック配列が NULL ことはありません</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28650-generic-value-is-not-treated-as-failure.md" data-raw-source="[C28650](28650-generic-value-is-not-treated-as-failure.md)">C28650</a></p></td>
<td align="left"><p>C28650 を警告します。対象の型です。 0 が使用されている処理されませんエラーとして。</p>
<p>状態値を返すなどです。TRUE は、失敗を示すステータス値を返すとは異なります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28651-member-function-pointers-cause-write-pages-copy.md" data-raw-source="[C28651](28651-member-function-pointers-cause-write-pages-copy.md)">C28651</a></p></td>
<td align="left"><p>C28651 を警告します。静的初期化子がメンバー関数ポインターのための書き込みページでコピーを原因します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28652-overloaded-bitwise-operators-cause-write-pages-copy.md" data-raw-source="[C28652](28652-overloaded-bitwise-operators-cause-write-pages-copy.md)">C28652</a></p></td>
<td align="left"><p>C28652 を警告します。静的初期化子がオーバー ロードされたビット処理演算子のための書き込みページでコピーを原因します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28714-ntstatus-cast-between-semantically-different-integer-types.md" data-raw-source="[C28714](28714-ntstatus-cast-between-semantically-different-integer-types.md)">C28714</a></p></td>
<td align="left"><p>C28714 を警告します。意味の異なる整数型の間のキャストします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28715-boolean-cast-between-semantically-different-integer-types.md" data-raw-source="[C28715](28715-boolean-cast-between-semantically-different-integer-types.md)">C28715</a></p></td>
<td align="left"><p>C28715 を警告します。意味の異なる整数型の間のキャストします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28716-compiler-inserted-cast-between-semantically-different-integral.md" data-raw-source="[C28716](28716-compiler-inserted-cast-between-semantically-different-integral.md)">C28716</a></p></td>
<td align="left"><p>C28716 を警告します。意味の異なる整数型の間のキャストのコンパイラ挿入されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28717-invalid-variant-type.md" data-raw-source="[C28717](28717-invalid-variant-type.md)">C28717</a></p></td>
<td align="left"><p>C28717 を警告します。無効な VARIANT 型</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28718-unannotated-buffer.md" data-raw-source="[C28718](28718-unannotated-buffer.md)">C28718</a></p></td>
<td align="left"><p>C28718 を警告します。Unannotated バッファー</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28719-banned-api-usage-use-updated-function-replacement.md" data-raw-source="[C28719](28719-banned-api-usage-use-updated-function-replacement.md)">C28719</a></p></td>
<td align="left"><p>C28719 を警告します。禁止されている API の使用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28720-banned-api-usage-use-updated-function-replacement.md" data-raw-source="[C28720](28720-banned-api-usage-use-updated-function-replacement.md)">C28720</a></p></td>
<td align="left"><p>C28720 を警告します。禁止されている API の使用</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28721-deprecated-performance-counter-architecture.md" data-raw-source="[C28721](28721-deprecated-performance-counter-architecture.md)">C28721</a></p></td>
<td align="left"><p>C28721 を警告します。非推奨のパフォーマンス カウンター アーキテクチャ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28722-unannotated-function-declaration-buffer.md" data-raw-source="[C28722](28722-unannotated-function-declaration-buffer.md)">C28722</a></p></td>
<td align="left"><p>C28722 を警告します。関数宣言で unannotated バッファー</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28723-unannotated-buffer-without-declaration.md" data-raw-source="[C28723](28723-unannotated-buffer-without-declaration.md)">C28723</a></p></td>
<td align="left"><p>C28723 を警告します。対応する宣言がない関数定義で unannotated バッファー</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28725-use-watson-instead.md" data-raw-source="[C28725](28725-use-watson-instead.md)">C28725</a></p></td>
<td align="left"><p>C28725 を警告します。ワトソンを使用して、この SetUnhandledExceptionFilter ではなく</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28726-banned-api-usage-use-updated-function-replacement.md" data-raw-source="[C28726](28726-banned-api-usage-use-updated-function-replacement.md)">C28726</a></p></td>
<td align="left"><p>C28726 を警告します。禁止されている API の使用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28727-banned-api-usage-use-updated-function-replacement.md" data-raw-source="[C28727](28727-banned-api-usage-use-updated-function-replacement.md)">C28727</a></p></td>
<td align="left"><p>C28727 を警告します。禁止されている API の使用</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28728-banned-api-usage-use-updated-function-replacement.md" data-raw-source="[C28728](28728-banned-api-usage-use-updated-function-replacement.md)">C28728</a></p></td>
<td align="left"><p>C28728 を警告します。禁止されている API の使用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28730-possible-null-character-assignment.md" data-raw-source="[C28730](28730-possible-null-character-assignment.md)">C28730</a></p></td>
<td align="left"><p>C28730 を警告します。可能な割り当て&#39;\0&#39;直接ポインターにします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28735-banned-crimson-api-usage.md" data-raw-source="[C28735](28735-banned-crimson-api-usage.md)">C28735</a></p></td>
<td align="left"><p>C28735 を警告します。禁止されている Crimson API の使用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28736-legacy-crimson-or-perflib-banned-argument-used.md" data-raw-source="[C28736](28736-legacy-crimson-or-perflib-banned-argument-used.md)">C28736</a></p></td>
<td align="left"><p>C28736 を警告します。禁止されている API 引数の使用方法</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28740-unannotated-unsigned-buffer.md" data-raw-source="[C28740](28740-unannotated-unsigned-buffer.md)">C28740</a></p></td>
<td align="left"><p>C28740 を警告します。Unannotated 符号なしのバッファー</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28741-unannotated-non-constant-string-buffer-in-function.md" data-raw-source="[C28741](28741-unannotated-non-constant-string-buffer-in-function.md)">C28741</a></p></td>
<td align="left"><p>C28741 を警告します。関数で unannotated バッファー</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28742-unnanotated-non-constant-buffer-in-function.md" data-raw-source="[C28742](28742-unnanotated-non-constant-buffer-in-function.md)">C28742</a></p></td>
<td align="left"><p>C28742 を警告します。関数で unannotated バッファー</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28750-banned-istrlen-usage.md" data-raw-source="[C28750](28750-banned-istrlen-usage.md)">C28750</a></p></td>
<td align="left"><p>C28750 を警告します。Lstrlen とそのバリエーションの禁止された使用状況</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28751-banned-exallocatepool-usage.md" data-raw-source="[C28751](28751-banned-exallocatepool-usage.md)">C28751</a></p></td>
<td align="left"><p>C28751 を警告します。ExAllocatePool とそのバリエーションの禁止された使用状況</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="28752-banned-kernel32-advapi32-usage.md" data-raw-source="[C28752](28752-banned-kernel32-advapi32-usage.md)">C28752</a></p></td>
<td align="left"><p>C28752 を警告します。Kernel32 または advapi32 の API の使用を禁止されています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="28753-relying-on-undefined-order-of-evalutation-params.md" data-raw-source="[C28753](28753-relying-on-undefined-order-of-evalutation-params.md)">C28753</a></p></td>
<td align="left"><p>C28753 を警告します。未定義のパラメーターの評価順序に依存</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="30029-memory-allocating-function-requests-executable-memory.md" data-raw-source="[C30029](30029-memory-allocating-function-requests-executable-memory.md)">C30029</a></p></td>
<td align="left"><p>C30029 を警告します。メモリの割り当てを実行可能なメモリを要求する関数を呼び出す</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="30030-parameter-indicates-executable-memory.md" data-raw-source="[C30030](30030-parameter-indicates-executable-memory.md)">C30030</a></p></td>
<td align="left"><p>C30030 を警告します。メモリ割り当て関数を呼び出すと、実行可能なメモリを示すパラメーターを渡す</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="30031-pool-n-optin-called-before-entry-function.md" data-raw-source="[C30031](30031-pool-n-optin-called-before-entry-function.md)">C30031</a></p></td>
<td align="left"><p>C30031 を警告します。メモリ割り当て関数を呼び出すと、実行可能なメモリを示すパラメーターを渡す</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="30032-forcing-request-of-executable-memory.md" data-raw-source="[C30032](30032-forcing-request-of-executable-memory.md)">C30032</a></p></td>
<td align="left"><p>C30032 を警告します。メモリ割り当て関数と、強制的に実行可能なメモリを使用しての要求を呼び出し、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh920401" data-raw-source="[POOL_NX_OPTOUT](https://msdn.microsoft.com/library/windows/hardware/hh920401)">POOL_NX_OPTOUT</a>ディレクティブ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="30033-executable-allocation-detected-with-pool-nx-optin.md" data-raw-source="[C30033](30033-executable-allocation-detected-with-pool-nx-optin.md)">C30033</a></p></td>
<td align="left"><p>C30033 を警告します。コンパイルされたドライバーの実行可能ファイルの割り当てが見つかりました<a href="https://msdn.microsoft.com/library/windows/hardware/hh920402" data-raw-source="[POOL_NX_OPTIN](https://msdn.microsoft.com/library/windows/hardware/hh920402)">POOL_NX_OPTIN</a>します。 別のドライバーでの実行時に読み込まれるドライバーと判断されました。 読み込みのドライバーを呼び出すことを確認してください<strong>ExInitializeDriverRuntime (<em>DrvRtPoolNxOptIn</em>)</strong>その DriverEntry でします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="30034-passing-flag-value-to-allocating-function.md" data-raw-source="[C30034](30034-passing-flag-value-to-allocating-function.md)">C30034</a></p></td>
<td align="left"><p>C30034 を警告します。フラグの値を割り当てられている実行可能なメモリの原因となる割り当て関数に渡します。 割り当て関数が実行可能ファイルの非ページ プールのフォームを要求していないことを確認してください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="30035-function-call-must-be-made-inside-init-function.md" data-raw-source="[C30035](30035-function-call-must-be-made-inside-init-function.md)">C30035</a></p></td>
<td align="left"><p>C30035 を警告します。初期化関数内から行う必要がある関数が呼び出されました (たとえば、 <strong>DriverEntry()</strong>または<strong>DllInitialize()</strong>)。 PREfast は、初期化関数の呼び出しを行ったかどうかを判断できませんでした。</p></td>
</tr>
</tbody>
</table>

 

 

 

