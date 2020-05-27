---
title: ドライバーの IRQL 注釈
description: ドライバーコードに IRQL 注釈がある場合、コード分析ツールを使用すると、関数を実行するレベルの範囲をより正確に推定し、エラーをより正確に見つけることができます。
ms.assetid: E4C1D490-BE06-483A-90E4-6F3223E269A3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5de19094f3914b68ad830e798019ba9965897e51
ms.sourcegitcommit: 9111f8ebcefc41d3a10e8db241d45003a79bec56
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83864710"
---
# <a name="irql-annotations-for-drivers"></a>ドライバーの IRQL 注釈

すべてのドライバー開発者は、割り込み要求レベル (IRQLs) を考慮する必要があります。 IRQL は、0 ~ 31 の整数です。\_一般に、パッシブレベル、ディスパッチ \_ レベル、および APC \_ レベルは、シンボルと呼ばれ、他のレベルは数値によって参照されます。 IRQL の発生と減少は、厳密なスタックの統制に従う必要があります。 関数は、呼び出されたのと同じ IRQL でを返すことを目的としています。 IRQL 値は、スタック内で減少しないようにする必要があります。 関数は、最初に発生させることなく、IRQL を下げることはできません。 IRQL 注釈は、これらの規則を強制するためのものです。

ドライバーコードに IRQL 注釈がある場合、コード分析ツールを使用すると、関数を実行するレベルの範囲をより正確に推定し、エラーをより正確に見つけることができます。 たとえば、関数を呼び出すことができる最大の IRQL を指定する注釈を追加できます。関数が高い IRQL で呼び出された場合、コード分析ツールは不整合を識別できます。

ドライバー関数は、適切な IRQL に関する情報で注釈を付ける必要があります。 追加情報が使用可能な場合は、呼び出し元の関数と呼び出された関数の両方の後続のチェックで、コード分析ツールに役立ちます。 場合によっては、注釈を追加することで、偽陽性を抑制することができます。 ユーティリティ関数などの一部の関数は、任意の IRQL で呼び出すことができます。 この場合、IRQL 注釈がないと、適切な注釈が付けられます。

IRQL に対して関数に注釈を付けるときは、現在の実装だけでなく、関数がどのように進化するかを考慮することが特に重要です。 たとえば、実装されている関数は、設計者よりも高い IRQL で正しく動作する可能性があります。 関数は、実際のコードに基づいて注釈を付けることができますが、将来の機能強化または保留中のシステム要件の最大 IRQL を低くする必要があるなど、将来の要件に対応している可能性があります。 注釈は、実際の実装ではなく、関数デザイナーの目的から派生する必要があります。

次の表の注釈を使用すると、関数とそのパラメーターの正しい IRQL を示すことができます。 IRQL 値は、Wdm で定義されています。

|IRQL 注釈|説明|
|--- |--- |
|\_IRQL_requires_max_ (_irql_)|_Irql_は、関数を呼び出すことができる最大 irql です。|
|\_IRQL_requires_min_ (_irql_)|_Irql_は、関数を呼び出すことができる最小 irql です。|
|\_IRQL_requires_ (_irql_)|関数は、 _irql_によって指定された irql で入力する必要があります。|
|\_IRQL_raises_ (_irql_)|関数は、指定された_irql_で終了しますが、この関数を呼び出すことができるのは、現在の irql を上げる (低い) ことだけです。|
|\_IRQL_saves_|注釈付きパラメーターは、後で復元するために現在の IRQL を保存します。|
|\_IRQL_restores_|注釈付きパラメーターには、関数がを返したときに復元される_IRQL_saves_からの IRQL 値が含まれています。|
|\_IRQL_saves_global_ (kind, param)|現在の IRQL は、IRQL が復元されるコード分析ツールの内部の場所に保存されます。 この注釈は、関数に注釈を付けるために使用されます。 この場所は、種類によって識別され、さらに param によって絞り込まれます。 たとえば、OldIrql は種類であり、FastMutex はその古い IRQL 値を保持するパラメーターである可能性があります。|
|\_IRQL_restores_global_ (_kind_, _param_)|IRQL_saves_global で注釈が付けられた関数によって保存される IRQL は、コード分析ツールの内部の場所から復元されます。|
|\_IRQL_always_function_min_ (_値_)|IRQL 値は、関数が IRQL を下げることができる最小値です。|
|\_IRQL_always_function_max_ (_値_)|IRQL 値は、関数が IRQL を発生させることができる最大値です。|
|\_IRQL_requires_same_|注釈が付けられた関数は、同じ IRQL でを入力して終了する必要があります。 関数は IRQL を変更できますが、終了する前に、IRQL を元の値に復元する必要があります。|
|\_IRQL_uses_cancel_|注釈付きパラメーターは、DRIVER_CANCEL コールバック関数によって復元される必要がある IRQL 値です。 ほとんどの場合、代わりに IRQL_is_cancel 注釈を使用します。|
 

## <a name="span-idannotations_for_driver_cancelspanspan-idannotations_for_driver_cancelspanspan-idannotations_for_driver_cancelspanannotations-for-driver_cancel"></a><span id="Annotations_for_DRIVER_CANCEL"></span><span id="annotations_for_driver_cancel"></span><span id="ANNOTATIONS_FOR_DRIVER_CANCEL"></span>ドライバーキャンセルの注釈 \_


Irql には \_ \_ cancel が使用され \_ 、 \_ \_ irql \_ はキャンセル \_ 注釈 \_ という違いがあります。 \_IRQL は \_ cancel 注釈を使用し \_ \_ ます。注釈付きパラメーターは、ドライバーキャンセルコールバック関数によって復元される IRQL 値であることを指定し \_ ます。 \_Irql \_ is cancel は、irql で \_ \_ 構成される複合注釈です。また、ドライバーのキャンセルの \_ \_ \_ \_ \_ コールバックユーティリティ関数が正しく動作するように、他のいくつかの注釈を使用します。 それ自体では、 \_ irql は \_ cancel 注釈を使用するだけで便利です \_ \_ 。たとえば、irql によって説明されている義務の残りの部分が \_ 既に \_ \_ \_ 何らかの方法で既に満たされている場合などです。

|IRQL 注釈|説明|
|--- |--- |
|IRQL_is_cancel|注釈付きパラメーターは、DRIVER_CANCEL コールバック関数への呼び出しの一部として渡される IRQL です。 この注釈は、関数がキャンセルルーチンから呼び出され、キャンセルスピンロックのリリースなどの DRIVER_CANCEL 関数の要件を完了するユーティリティであることを示します。|


## <a name="span-idhow_irql_annotations_interactspanspan-idhow_irql_annotations_interactspanspan-idhow_irql_annotations_interactspanhow-irql-annotations-interact"></a><span id="How_IRQL_Annotations_Interact"></span><span id="how_irql_annotations_interact"></span><span id="HOW_IRQL_ANNOTATIONS_INTERACT"></span>IRQL 注釈の相互作用


IRQL 値は、呼び出されたさまざまな関数によって設定、リセット、保存、および復元されるため、IRQL パラメーター注釈は他の注釈と相互にやり取りします。

### <a name="span-idspecifying_maximum_and_minimum_irqlspanspan-idspecifying_maximum_and_minimum_irqlspanspan-idspecifying_maximum_and_minimum_irqlspanspecifying-maximum-and-minimum-irql"></a><span id="Specifying_Maximum_and_Minimum_IRQL"></span><span id="specifying_maximum_and_minimum_irql"></span><span id="SPECIFYING_MAXIMUM_AND_MINIMUM_IRQL"></span>最大値と最小 IRQL の指定

Irql には \_ \_ max と irql が必要です \_ \_ 。 min 注釈では、 \_ 指定された \_ \_ \_ 値よりも大きい、または小さい irql から関数を呼び出すことができないことを指定します。 たとえば、PREfast が irql を変更しない一連の関数呼び出しを認識した場合、irql があることを検出すると、近くにある \_ \_ \_ \_ irql の下にある max 値には \_ min が必要です。これは、 \_ \_ \_ 2 回目に発生した呼び出しに対して警告を報告します。 最初の呼び出しでエラーが発生することがあります。メッセージには、競合の残りの半分が発生した場所が示されます。

関数の注釈が IRQL に言及し、irql を明示的に適用しない場合、 \_ \_ \_ 最大値が必要になるため、 \_ コード分析ツールによって注釈 irql が暗黙的に適用され \_ \_ \_ \_ \_ ます。これは通常、まれな例外で適切です。 これを既定値として暗黙的に適用すると、注釈が多くなり、例外がより見やすくなります。

Irql \_ は \_ \_ min \_ (パッシブレベル) の注釈を必要とします \_ 。これは、irql が低くなる可能性があるためです。したがって、最小 irql に関する明示的な規則はありません。 ほとんどの関数にはディスパッチレベル以外の上限 \_ とパッシブレベル以外の下限の両方があり \_ ます。

いくつかの関数は、呼び出された関数が最大値を超えて IRQL を安全に上げることができないコンテキストで呼び出される場合があります。また、より多くの場合、少なくとも少なくとも少なくとも低い方法で低コストにすることは Irql は常に最大値を返し、 \_ \_ irql は \_ \_ \_ \_ \_ 常に \_ min 注釈によって機能し、 \_ \_ これが意図せずに発生するケースを PREfast 検索します。

たとえば、DRIVER STARTIO 型の関数に \_ は、IRQL が " \_ \_ 常に \_ \_ 最小値 \_ (ディスパッチ \_ レベル)" で注釈が付けられます。 つまり、ドライバー STARTIO 関数の実行中に \_ 、ディスパッチレベル以下の IRQL を下げるとエラーになり \_ ます。 他の注釈は、ディスパッチレベルで関数を入力して終了する必要があることを示し \_ ます。

### <a name="span-idspecifying_an_explicit_irqlspanspan-idspecifying_an_explicit_irqlspanspan-idspecifying_an_explicit_irqlspanspecifying-an-explicit-irql"></a><span id="Specifying_an_Explicit_IRQL"></span><span id="specifying_an_explicit_irql"></span><span id="SPECIFYING_AN_EXPLICIT_IRQL"></span>明示的な IRQL の指定

PREfast を使用すると、irql があることを確認 \_ \_ するため \_ \_ \_ に注釈が必要です \_ 。 irql で検出された不整合については、 \_ \_ \_ max \_ または irql には \_ \_ \_ \_ 、irql を認識しているため、min 注釈が必要です。

\_Irql \_ 発生注釈は、 \_ irql が新しい値に設定された状態で関数がを返すことを示します。 Irql 発生の注釈を使用すると \_ \_ \_ 、 \_ \_ 同じ irql 値に対して、drv の maxfunctionirql 注釈も効果的に設定されます。 ただし、関数が最終的な値よりも大きい IRQL を発生させて最終的な値に下げる場合は、irql の発生後に明示的な irql 関数 max 注釈を追加して、 \_ \_ \_ \_ \_ \_ \_ \_ 高い irql 値を許可する必要があります。

### <a name="span-idraising_or_lowering_irqlspanspan-idraising_or_lowering_irqlspanspan-idraising_or_lowering_irqlspanraising-or-lowering-irql"></a><span id="Raising_or_Lowering_IRQL"></span><span id="raising_or_lowering_irql"></span><span id="RAISING_OR_LOWERING_IRQL"></span>IRQL の発生または減少

Irql が発生する注釈は、関数 \_ \_ の構文で許可されてい \_ ても、irql を上げるためにのみ使用する必要があることを示します。 KeRaiseIrql は、IRQL を低くするために使用すべきではない関数の一例です。

### <a name="span-idsaving_and_restoring_irqlspanspan-idsaving_and_restoring_irqlspanspan-idsaving_and_restoring_irqlspansaving-and-restoring-irql"></a><span id="Saving_and_Restoring_IRQL"></span><span id="saving_and_restoring_irql"></span><span id="SAVING_AND_RESTORING_IRQL"></span>IRQL の保存と復元

Irql の \_ \_ 保存と irql 復元の注釈を使用して、注釈 \_ \_ \_ \_ 付きパラメーターに対して現在の irql (厳密には、または概数のみ) が保存または復元されることを示します。

一部の関数は、IRQL を暗黙的に保存および復元します。 たとえば、ExAcquireFastMutex システム関数は、最初のパラメーターが識別する fast mutex オブジェクトに関連付けられている不透明な場所に IRQL を保存します。保存された IRQL は、その高速ミューテックスオブジェクトの対応する ExReleaseFastMutex 関数によって復元されます。 これらのアクションを明示的に指定するには、グローバルと irql の復元のグローバル注釈を保存する irql を使用し \_ \_ \_ \_ \_ \_ \_ \_ ます。 *Kind*および*param*パラメーターは、IRQL 値が保存される場所を示します。 値を保存して復元する注釈が一貫している限り、値を保存する場所を正確に指定する必要はありません。

### <a name="span-idmaintaining_the_same_irqlspanspan-idmaintaining_the_same_irqlspanspan-idmaintaining_the_same_irqlspanmaintaining-the-same-irql"></a><span id="Maintaining_the_Same_IRQL"></span><span id="maintaining_the_same_irql"></span><span id="MAINTAINING_THE_SAME_IRQL"></span>同じ IRQL の維持

Irql の変更が予期されることを示すために、ドライバーが作成するすべての関数に対して、irql が同じ注釈を必要とするか \_ \_ \_ \_ 、他の irql 注釈の1つを使用して、irql を変更するように注釈を付ける必要があります。 IRQL が変更されたことを示す注釈がない場合、コード分析ツールは、関数が入力されたのと同じ IRQL で終了しないすべての関数に対して警告を発行します。 IRQL の変更が意図されている場合は、適切な注釈を追加してエラーを抑制します。 IRQL の変更が意図されていない場合は、コードを修正する必要があります。

### <a name="span-idsaving_and_restoring_irql_for_i_o_cancellation_routinesspanspan-idsaving_and_restoring_irql_for_i_o_cancellation_routinesspanspan-idsaving_and_restoring_irql_for_i_o_cancellation_routinesspansaving-and-restoring-irql-for-io-cancellation-routines"></a><span id="Saving_and_Restoring_IRQL_for_I_O_Cancellation_Routines"></span><span id="saving_and_restoring_irql_for_i_o_cancellation_routines"></span><span id="SAVING_AND_RESTORING_IRQL_FOR_I_O_CANCELLATION_ROUTINES"></span>I/o キャンセルルーチンの IRQL の保存と復元

Irql を使用して、 \_ \_ \_ \_ 注釈付きパラメーターがドライバーキャンセルコールバック関数によって復元される IRQL 値であることを示し \_ ます。 この注釈は、関数がキャンセルルーチンから呼び出されるユーティリティであり、ドライバーの \_ キャンセル機能 (つまり、呼び出し元の義務を退院) に対して行われた要件を完了することを示します。

たとえば、DRIVER CANCEL コールバック関数の型の宣言を次に示し \_ ます。 パラメーターの1つは、この関数によって復元される必要がある IRQL です。 注釈は、cancel 関数のすべての要件を示します。

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

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[ドライバーの SAL 2.0 注釈](sal-2-annotations-for-windows-drivers.md)

 

 






