---
title: ドライバーの IRQL の注釈
description: ドライバー コードに IRQL の注釈がある場合は、コード分析ツールは位置関数を実行する必要がありより正確に見つけられるエラーのレベルの範囲に関するより優れた推定を行うことができます。
ms.assetid: E4C1D490-BE06-483A-90E4-6F3223E269A3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d184f7742da975a6375884141aa9f33f2e033e4f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538274"
---
# <a name="irql-annotations-for-drivers"></a>ドライバーの IRQL の注釈

ドライバー コードに IRQL の注釈がある場合は、コード分析ツールは位置関数を実行する必要がありより正確に見つけられるエラーのレベルの範囲に関するより優れた推定を行うことができます。 たとえば、位置、関数を呼び出すことができます。 最大の IRQL を指定する注釈を追加できます。高い IRQL で関数を呼び出すと、コード分析ツールは、不整合を識別できます。

すべてのドライバー開発者は、割り込み要求レベル (Irql) を検討する必要があります。 IRQL は 0 ~ 31 の整数パッシブ\_レベル、ディスパッチ\_レベル、および APC\_レベルは通常参照シンボル、およびその他の数値の値。 IRQL 値の増減は、厳密なスタック規範に従う必要があります。 関数は、呼び出された同じ IRQL で返すことを目指します。 IRQL の値は、スタックの非減少する必要があります。 関数は、最初は生成せず、IRQL を下げることはできません。 IRQL の注釈は、これらのルールを適用するのに役立ちます。

ドライバー コードに IRQL の注釈がある場合は、コード分析ツールは位置関数を実行する必要がありより正確に見つけられるエラーのレベルの範囲に関するより優れた推定を行うことができます。 たとえば、位置、関数を呼び出すことができます。 最大の IRQL を指定する注釈を追加できます。高い IRQL で関数を呼び出すと、コード分析ツールは、不整合を識別できます。

ドライバー関数に関する適切な可能性のある IRQL の多くの情報で注釈を付ける必要があります。 追加の情報を使用できる場合は、呼び出し元の関数と、呼び出された関数の両方のチェックの後でコード分析ツールが役立ちます。 場合によっては、注釈の追加は偽陽性を抑制する優れた方法です。 ユーティリティ関数の場合など、一部の関数は、IRQL でも呼び出すことができます。 この場合は、IRQL の注釈がないは、適切な注釈です。

関数 IRQL の注釈の追加時に、どの関数を進化させる、だけでなく、現在の実装を検討するは特に重要です。 たとえば、実装されている関数は、デザイナーが意図したよりも高い IRQL で正しく動作可能性があります。 基に、コードが実際には、関数の注釈を設定することになりますが、デザイナーが最大の IRQL 将来の機能強化がいくつかのまたは保留中のシステム要件を低減する必要性など、将来の要件に注意してくださかった。 場合があります。 注釈は、実際の実装からではなく、デザイナーの関数の目的から派生する必要があります。

次の表に、注釈を使用して、関数とそのパラメーターの適切な IRQL を示すことができます。 IRQL の値は、Wdm.h で定義されます。

|IRQL の注釈|説明|
|--- |--- |
|\_IRQL_requires_max_(_irql_)|_Irql_が最大の IRQL が、関数を呼び出すことができます。|
|\_IRQL_requires_min_(_irql_)|_Irql_が最小の IRQL が、関数を呼び出すことができます。|
|\_IRQL_requires_(_irql_)|指定された IRQL で関数を入力する必要があります_irql_します。|
|\_IRQL_raises_(_irql_)|関数の指定した終了_irql_が (低いされません) の現在の IRQL をさせるのみ呼び出すことができます。|
|\_IRQL_saves_|注釈付きのパラメーターは、後で復元する現在の IRQL を保存します。|
|\_IRQL_restores_|注釈付きのパラメーターにはから IRQL の値が含まれています_IRQL_saves_関数が返されるときに復元します。|
|\_IRQL_saves_global_ (種類、param)|現在の IRQL は、IRQL の復元元のコード分析ツールの内部にある場所に保存されます。 この注釈を使用して、関数の注釈を設定します。 場所は種類で識別され、param によってさらに絞り込みます。 たとえば、OldIrql の種類、可能性があり、FastMutex のパラメーターを古い IRQL の値が保持されている可能性があります。|
|\_IRQL_restores_global_(_kind_, _param_)|コード分析ツールの内部にある場所から IRQL_saves_global で注釈を付ける関数によって保存された IRQL が復元されます。|
|\_IRQL_always_function_min_(_value_)|IRQL の値は、最小値、関数が、IRQL を下げることができます。|
|\_IRQL_always_function_max_(_value_)|IRQL の値は、関数が、IRQL を発生できる最大値です。|
|\_IRQL_requires_same_|注釈付きの関数は、入力し、同じ IRQL で終了する必要があります。 関数は、IRQL を変更できますが、終了する前に元の値の IRQL が復元する必要があります。|
|\_IRQL_uses_cancel_|注釈付きのパラメーターは、DRIVER_CANCEL コールバック関数によって復元する必要があります、IRQL の値です。 ほとんどの場合、代わりに IRQL_is_cancel 注釈を使用します。|
 

## <a name="span-idannotationsfordrivercancelspanspan-idannotationsfordrivercancelspanspan-idannotationsfordrivercancelspanannotations-for-drivercancel"></a><span id="Annotations_for_DRIVER_CANCEL"></span><span id="annotations_for_driver_cancel"></span><span id="ANNOTATIONS_FOR_DRIVER_CANCEL"></span>ドライバーの注釈\_キャンセル


間の違いは、 \_IRQL\_使用\_キャンセル\_と\_IRQL\_は\_キャンセル\_注釈。 \_IRQL\_使用\_キャンセル\_だけ注釈では、注釈付きのパラメーターが、ドライバーによって復元する必要があります、IRQL の値を指定します\_CANCEL callback 関数。 \_IRQL\_は\_キャンセル\_注釈から成る複合注釈は、 \_IRQL\_使用\_キャンセル\_さらに他のいくつかの注釈ドライバーの動作が正しいことを確認する\_CANCEL callback ユーティリティ関数。 単独で、 \_IRQL\_を使用して\_キャンセル\_注釈は場合によっては便利なだけ; によって、義務の残りの部分が説明されている場合など、 \_IRQL\_は\_キャンセル\_が既に他の方法で満たされました。

|IRQL の注釈|説明|
|--- |--- |
|IRQL_is_cancel|注釈付きのパラメーターには、DRIVER_CANCEL コールバック関数の呼び出しの一部として渡される IRQL です。 この注釈は、関数がキャンセル ルーチンから呼び出され、DRIVER_CANCEL 関数では、キャンセルのスピン ロックの解放などの要件を完了するユーティリティであることを示します。|


## <a name="span-idhowirqlannotationsinteractspanspan-idhowirqlannotationsinteractspanspan-idhowirqlannotationsinteractspanhow-irql-annotations-interact"></a><span id="How_IRQL_Annotations_Interact"></span><span id="how_irql_annotations_interact"></span><span id="HOW_IRQL_ANNOTATIONS_INTERACT"></span>IRQL の注釈がやり取りする方法


IRQL パラメーターの注釈相互作用の他の注釈により、IRQL の値が設定、リセット、保存、およびさまざまな呼び出された関数で復元するためです。

### <a name="span-idspecifyingmaximumandminimumirqlspanspan-idspecifyingmaximumandminimumirqlspanspan-idspecifyingmaximumandminimumirqlspanspecifying-maximum-and-minimum-irql"></a><span id="Specifying_Maximum_and_Minimum_IRQL"></span><span id="specifying_maximum_and_minimum_irql"></span><span id="SPECIFYING_MAXIMUM_AND_MINIMUM_IRQL"></span>最大および最小の IRQL を指定します。

\_IRQL\_必要があります\_max\_と\_IRQL\_必要があります\_min\_注釈を指定、関数が、IRQL がから呼び出すことはできません指定した値より高いまたは低い。 たとえば、PREfast に表示される一連の関数呼び出しが変わりません、IRQL のいずれか見つかった場合、 \_IRQL\_必要があります\_max\_下にある値を近くにある\_IRQL\_必要があります\_min\_、検出すると、2 番目の呼び出しで、警告を報告します。 実際には、最初の呼び出しで発生したエラーメッセージは、残りの半分の競合が発生した場所を示します。

関数の注釈の IRQL をメンションし、明示的には適用されない場合\_IRQL\_必要があります\_max\_、コード分析ツールは、注釈を暗黙的に適用されます\_IRQL\_必要があります\_max\_(ディスパッチ\_レベル)、これはまれなケースを除き、通常は正しいです。 暗黙的にこの既定値として適用すること、多くの注釈の煩雑さを排除し、例外をはるかに参照できるようにします。

\_IRQL\_必要\_min\_(パッシブ\_レベル) の IRQL が下を移動しないために、注釈は常に暗黙的。 その結果、最小の IRQL についての対応する明示的なルールはありません。 関数はほとんど上限を設ける両方、ディスパッチ以外\_レベルとパッシブ以外の下限\_レベル。

呼び出された関数いくつかの最大値を超える IRQL を安全に引き上げることができないかより多くの場合、安全に下げることはできませんいくつかの最小値を下回ってのコンテキストでは、一部の関数が呼び出されます。 \_IRQL\_常に\_関数\_max\_と\_IRQL\_常に\_関数\_min\_注釈 PREfast のヘルプこれが意図せずケースを紹介します。

たとえば、ドライバーの種類の関数\_STARTIO が付けられている\_IRQL\_常に\_関数\_min\_(ディスパッチ\_レベル)。 これにより、ドライバーの実行中に\_STARTIO 関数では、ディスパッチの下の IRQL を低くとエラーには\_レベル。 その他の注釈は、関数の入力し、ディスパッチで終了する必要があることを示す\_レベル。

### <a name="span-idspecifyinganexplicitirqlspanspan-idspecifyinganexplicitirqlspanspan-idspecifyinganexplicitirqlspanspecifying-an-explicit-irql"></a><span id="Specifying_an_Explicit_IRQL"></span><span id="specifying_an_explicit_irql"></span><span id="SPECIFYING_AN_EXPLICIT_IRQL"></span>明示的な IRQL を指定します。

使用して、 \_IRQL\_発生\_または\_IRQL\_必要があります\_注釈 PREfast をより適切にヘルプをレポートする不整合が検出された\_IRQL\_必要があります\_max\_または\_IRQL\_必要があります\_min\_注釈にし、IRQL が認識しています。

\_IRQL\_発生\_注釈では、新しい値に設定の IRQL で関数が返すことを示します。 使用すると、 \_IRQL\_発生\_注釈も効果的に設定、 \_drv\_maxFunctionIRQL に注釈を同じ IRQL の値。 ただし、関数は、最終的な値よりも大きい IRQL を発生させますとし、最終的な値が低くなります、する必要がありますを追加する明示的な\_IRQL\_常に\_関数\_max\_注釈次、。\_IRQL\_発生\_高い IRQL の値を許容する注釈。

### <a name="span-idraisingorloweringirqlspanspan-idraisingorloweringirqlspanspan-idraisingorloweringirqlspanraising-or-lowering-irql"></a><span id="Raising_or_Lowering_IRQL"></span><span id="raising_or_lowering_irql"></span><span id="RAISING_OR_LOWERING_IRQL"></span>IRQL を下げるかコレクションを発生させる

\_IRQL\_発生\_注釈は、関数は IRQL を発生させる場合にのみ使用する必要があり、関数の構文は許可する場合でも、IRQL の削減に使用しないでを示します。 KeRaiseIrql は、IRQL を下げるには使用できないする必要があります関数の例に示します。

### <a name="span-idsavingandrestoringirqlspanspan-idsavingandrestoringirqlspanspan-idsavingandrestoringirqlspansaving-and-restoring-irql"></a><span id="Saving_and_Restoring_IRQL"></span><span id="saving_and_restoring_irql"></span><span id="SAVING_AND_RESTORING_IRQL"></span>保存と復元の IRQL

使用して、 \_IRQL\_保存\_と\_IRQL\_復元\_(かどうかが認識されます約のみかを正確に) 現在の IRQL に保存またはから復元されたことを示すの注釈注釈付きパラメーター。

一部の関数は、保存し、IRQL を暗黙的に復元します。 など ExAcquireFastMutex システム関数を最初のパラメーターが識別する; 高速なミュー テックス オブジェクトに関連付けられた非透過の場所に、IRQL を保存します.高速なミュー テックス オブジェクトの対応する ExReleaseFastMutex 関数では、保存した IRQL が復元されます。 これらのアクションを明示的に示すために使用、 \_IRQL\_保存\_グローバル\_と\_IRQL\_復元\_グローバル\_注釈。 *種類*と*param* IRQL の値が保存されているパラメーターを示します。 値が保存されている場所はありませんを正確に指定された注釈を保存し、値の復元が一貫性のある限り。

### <a name="span-idmaintainingthesameirqlspanspan-idmaintainingthesameirqlspanspan-idmaintainingthesameirqlspanmaintaining-the-same-irql"></a><span id="Maintaining_the_Same_IRQL"></span><span id="maintaining_the_same_irql"></span><span id="MAINTAINING_THE_SAME_IRQL"></span>同じ IRQL を維持

いずれかを使用して IRQL を変更するには、ドライバーを作成する関数の注釈を設定する必要があります、 \_IRQL\_必要\_同じ\_注釈またはその他の IRQL の IRQL で変更があることを示す注釈のいずれか必要です。 コード分析ツールでは IRQL での変更を示すの注釈がない場合は、関数が入力される同じ IRQL で終了しない任意の関数の警告が発行されます。 IRQL で変更する場合、エラーを抑制する適切な注釈を追加します。 、IRQL の変更が意図していない場合は、コードを修正する必要があります。

### <a name="span-idsavingandrestoringirqlforiocancellationroutinesspanspan-idsavingandrestoringirqlforiocancellationroutinesspanspan-idsavingandrestoringirqlforiocancellationroutinesspansaving-and-restoring-irql-for-io-cancellation-routines"></a><span id="Saving_and_Restoring_IRQL_for_I_O_Cancellation_Routines"></span><span id="saving_and_restoring_irql_for_i_o_cancellation_routines"></span><span id="SAVING_AND_RESTORING_IRQL_FOR_I_O_CANCELLATION_ROUTINES"></span>保存と入出力キャンセル ルーチンの IRQL を復元

使用して、 \_IRQL\_使用\_キャンセル\_注釈付きのパラメーターが、ドライバーによって復元する必要があります、IRQL の値であることを示すの注釈\_CANCEL callback 関数。 この注釈は、関数がキャンセル ルーチンから呼び出されるユーティリティであること、およびドライバーで行われた要求が完了したことを示します\_キャンセル関数 (つまり、その放電されるため、呼び出し元の義務)。

ドライバーの宣言は、次の例では、\_キャンセル コールバック関数の型。 パラメーターの 1 つは、この関数によって復元する必要がありますの IRQL です。 注釈には、すべてのキャンセル関数の要件を示します。

```ManagedCPlusPlus
// Define driver cancel routine type.  //    
__drv_functionClass(DRIVER_CANCEL)  
_Requires_lock_held_(_Global_cancel_spin_lock_)  
_Releases_lock_(_Global_cancel_spin_lock_)  
_IRQL_requires_min_(DISPATCH_LEVEL)  
_IRQL_requires_(DISPATCH_LEVEL)  
typedef  
VOID  
DRIVER_CANCEL (  
    _Inout_ struct _DEVICE_OBJECT *DeviceObject,  
    _Inout_ _IRQL_uses_cancel_ struct _IRP *Irp  
    );  
  
typedef DRIVER_CANCEL *PDRIVER_CANCEL;  
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[SAL 2.0 注釈ドライバー](sal-2-annotations-for-windows-drivers.md)

 

 






