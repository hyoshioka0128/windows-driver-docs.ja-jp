---
title: _Flt_CompletionContext_Outptr_ 注釈
description: 使用して、 _Flt_CompletionContext_Outptr_注釈ファイル システム ミニフィルターの前の操作のコールバック関数 PFLT_PRE_OPERATION_CALLBACK を宣言するときにします。
ms.assetid: C3B285EA-0DAB-48D4-AE2F-CB4FBB30EF15
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 956c70c6386e68c87b9a0b02da10485172c3b61b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364178"
---
# <a name="fltcompletioncontextoutptr-annotation"></a>\_Flt\_CompletionContext\_Outptr\_注釈


使用して、 **\_Flt\_CompletionContext\_Outptr\_** ファイル システム ミニフィルターの前の操作のコールバック関数を宣言するときに、注釈[ **PFLT\_PRE\_操作\_コールバック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_pre_operation_callback)します。 この注釈を配置、 *CompletionContext*パラメーター。 この注釈を設定することを確認するコード分析ツール、 *CompletionContext* 、FLT の正しい\_PREOP\_コールバック\_状態の戻り値。

前の操作のコールバック関数の場合 ([**PFLT\_前\_操作\_コールバック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_pre_operation_callback)) 返します FLT\_PREOP\_成功\_\_コールバックまたは FLT\_PREOP\_同期、 *CompletionContext*可能性がありますまたは NULL にできない場合があります。 その他の任意の FLT の\_PREOP\_コールバック\_状態の戻り値、 *CompletionContext* NULL にする必要があります。 *CompletionContext*フィルターの前の操作のコールバックから対応する後の操作のコールバック関数に渡されるフィルター定義の状態は、([**PFLT\_の投稿\_操作\_コールバック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_post_operation_callback))。 後の操作のコールバックは、フィルターが FLT を返す場合にのみ呼び出されます\_PREOP\_成功\_WITH\_コールバックまたは FLT\_PREOP\_その前の操作のコールバックから同期関数。 フィルターは、その前の操作のコールバック関数のいずれかの状態をその後の操作のコールバック関数に合格しなかった場合、 *CompletionContext*が null の場合、つまり*CompletionContext*でその後の操作のコールバック関数は NULL になります。 状態を返すかどうかを決定する個々 のフィルターは各*CompletionContext*から前の操作のコールバック関数の場合、これはそれぞれ個別のフィルターになるかどうかを知るまで*CompletionContext*でその後の操作のコールバック関数。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>例


次の例の関数のプロトタイプを[ **PFLT\_PRE\_操作\_コールバック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_pre_operation_callback)呼び出される関数*SwapPreReadBuffers*. *CompletionContext*パラメーターは、後の操作のコールバック関数に渡されるコンテキストを受信しで宣言されている **\_Flt\_CompletionContext\_Outptr\_** 注釈。

```ManagedCPlusPlus
FLT_PREOP_CALLBACK_STATUS
SwapPreReadBuffers(
    _Inout_ PFLT_CALLBACK_DATA Data,
    _In_ PCFLT_RELATED_OBJECTS FltObjects,
    _Flt_CompletionContext_Outptr_ PVOID *CompletionContext
    );
```

**\_Flt\_CompletionContext\_Outptr\_** specstrings.h で注釈が定義されています。 注釈を使用してコードにオーバーヘッドや複雑さを追加せずにチェックを貴重なエラーを追加できます。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[**PFLT\_PRE\_操作\_コールバック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_pre_operation_callback)

[**PFLT\_POST\_操作\_コールバック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_post_operation_callback)

[Windows ドライバーの SAL 2.0 注釈](sal-2-annotations-for-windows-drivers.md)





