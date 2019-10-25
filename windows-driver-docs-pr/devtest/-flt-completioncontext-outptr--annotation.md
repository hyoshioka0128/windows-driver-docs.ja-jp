---
title: _Flt_CompletionContext_Outptr_ 注釈
description: ファイルシステムミニ操作のコールバック関数 PFLT_PRE_OPERATION_CALLBACK を宣言するときに、 _Flt_CompletionContext_Outptr_注釈を使用します。
ms.assetid: C3B285EA-0DAB-48D4-AE2F-CB4FBB30EF15
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 128024ede88da13d6bebe1f984cba627a1f354e8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839605"
---
# <a name="_flt_completioncontext_outptr_-annotation"></a>\_Flt\_完了\_Outptr\_ 注釈


ファイルシステムミニ操作コールバック関数[**PFLT\_pre\_operation\_callback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)を宣言するときに、 **\_Flt\_の完了\_outptr\_** 注釈を使用します。 この注釈を*完了パラメーターに配置します*。 この注釈は、コード分析ツールに対して、FLT\_PREOP\_CALLBACK\_STATUS 戻り値の*完了が正しい*ことを確認するように指示します。

操作前のコールバック関数 ([**PFLT\_preop 操作\_コールバック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)) が\_コールバックまたは FLT\_preop\_を使用して、FLT\_PREOP\_成功\_を返した場合は、完了後の値が NULL である可能性があります。 その他の FLT\_PREOP\_CALLBACK\_STATUS 戻り値については、完了後の値を NULL に*する必要が*あります。 [完了後] はフィルターで定義された*状態で、* フィルターの操作前コールバックから、対応する操作後のコールバック関数 ([**PFLT\_post\_操作\_コールバック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)) に渡されます。 操作後のコールバックが呼び出されるのは、フィルターが FLT\_PREOP\_SUCCESS\_を返した場合\_CALLBACK または FLT\_PREOP\_を操作前のコールバック関数から同期する場合のみです。 フィルターが、操作前のコールバック関数から操作後のコールバック関数に状態を渡さない場合、完了*後のコール*バック関数は null になります。したがって、操作後のコールバック関数の完了*後のコール*バック関数は null になります。 各フィルターでは、操作前のコールバック*関数から状態を返す*かどうかが決定されます。そのため、各フィルターは、操作*後のコールバックで完了*状態を確認する必要があるかどうかを確認します。プロシージャ.

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>よう


次の例は、 *SwapPreReadBuffers*と呼ばれる[**コールバック関数\_PFLT\_PRE\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)の関数プロトタイプを示しています。 完了*後パラメーターは、操作*後のコールバック関数に渡されるコンテキストを受け取ります。このパラメーターは、 **\_Flt\_完了\_outptr\_** 注釈を使用して宣言されます。

```ManagedCPlusPlus
FLT_PREOP_CALLBACK_STATUS
SwapPreReadBuffers(
    _Inout_ PFLT_CALLBACK_DATA Data,
    _In_ PCFLT_RELATED_OBJECTS FltObjects,
    _Flt_CompletionContext_Outptr_ PVOID *CompletionContext
    );
```

**\_Flt\_完了\_Outptr\_** 注釈は、specstrings. h で定義されています。 注釈を使用すると、コードにオーバーヘッドや複雑さを追加せずに、重要なエラーチェックを追加できます。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[**PFLT\_事前\_操作\_コールバック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)

[**PFLT\_POST\_操作\_コールバック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)

[Windows ドライバーの SAL 2.0 注釈](sal-2-annotations-for-windows-drivers.md)





