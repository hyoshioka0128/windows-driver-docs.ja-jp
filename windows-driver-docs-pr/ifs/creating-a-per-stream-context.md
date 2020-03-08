---
title: ストリーム別コンテキストの作成
description: ストリーム別コンテキストの作成
ms.assetid: e33dba3b-50f7-43d8-b7e8-b7c2c9034d51
keywords:
- フィルタードライバー WDK ファイルシステム、ストリームごとのコンテキスト追跡
- ファイルシステムフィルタードライバー WDK、ストリームごとのコンテキスト追跡
- ストリームごとのコンテキスト追跡 WDK ファイルシステム
- ストリームごとのコンテキストの追跡 WDK ファイルシステム
- ストリームコンテキストごとの割り当て
- ストリームごとのコンテキストの初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f1f8f8176f269a56f9fd1dcf487d5e7203ff59e
ms.sourcegitcommit: 8c898615009705db7633649a51bef27a25d72b26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/07/2020
ms.locfileid: "78910425"
---
# <a name="creating-a-per-stream-context"></a>ストリーム別コンテキストの作成

[**FSRTL_PER_STREAM_CONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsrtl_per_stream_context)構造体を含むストリームごとのコンテキスト構造を使用する従来のファイルシステムフィルタードライバーでは、MICROSOFT Windows XP 以降でのストリームごとのコンテキストサポートを利用できます。

ファイルシステムフィルタードライバーは、通常、ファイルストリームが最初に開かれたときに、ファイルストリームの[ストリームごとのコンテキスト構造](file-streams--stream-contexts--and-per-stream-contexts.md)を作成します。 ただし、任意の操作中に、ストリームごとのコンテキスト構造を作成し、ファイルストリームに関連付けることができます。

## <a name="allocating-the-per-stream-context"></a>ストリームごとのコンテキストの割り当て

ストリームごとのコンテキスト構造は、ページングされたプールまたは非ページプールから割り当てることができます。 ストリームごとのコンテキストを割り当てるには、次の例に示すように、 [**Exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)を呼び出します。

```cpp
contextSize = sizeof(SPY_STREAM_CONTEXT) + fileName.Length;
ctx = ExAllocatePoolWithTag(NonPagedPool,
                            contextSize,
                            MYLEGACYFILTER_CONTEXT_TAG);
```

> [!NOTE]
> フィルターが、ストリームごとのコンテキスト構造をページプールから割り当てた場合、その作成完了ルーチンから[**Exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)を呼び出すことはできません。 これは、完了ルーチンは IRQL DISPATCH_LEVEL で呼び出すことができるためです。

### <a name="initializing-the-per-stream-context"></a>ストリームごとのコンテキストの初期化

ファイルシステムフィルタードライバーは、ストリームごとのコンテキスト構造を初期化するために、 [**Fsrtlinitperstreamcontext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlinitperstreamcontext)を呼び出します。 このルーチンは、コンテキスト構造の FSRTL_PER_STREAM_CONTEXT の部分を初期化します。 (構造体の残りの部分はフィルタードライバーに固有です)。

> [!NOTE]
> フィルタードライバーがファイルストリームごとにストリームごとのコンテキスト構造を1つだけ作成する場合は、 *InstanceId*パラメーターに**NULL**を渡す必要が[**あります。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlinitperstreamcontext)

フィルタードライバーは、ストリームごとのコンテキストをいつでも初期化できます。 ただし、コンテキストをファイルストリームに関連付ける前に実行する必要があります。
