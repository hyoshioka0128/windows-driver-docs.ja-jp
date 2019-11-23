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
ms.openlocfilehash: a2a5435647c97777c7443356eb952e0783b09d06
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841451"
---
# <a name="creating-a-per-stream-context"></a>ストリーム別コンテキストの作成


## <span id="ddk_creating_a_per_stream_context_if"></span><span id="DDK_CREATING_A_PER_STREAM_CONTEXT_IF"></span>


ファイルシステムフィルタードライバーは、通常、ファイルストリームが最初に開かれたときに、ファイルストリームの[ストリームごとのコンテキスト構造](file-streams--stream-contexts--and-per-stream-contexts.md)を作成します。 ただし、任意の操作中に、ストリームごとのコンテキスト構造を作成し、ファイルストリームに関連付けることができます。

### <a name="span-idallocating_the_per-stream_contextspanspan-idallocating_the_per-stream_contextspanspan-idallocating_the_per-stream_contextspanallocating-the-per-stream-context"></a><span id="Allocating_the_Per-Stream_Context"></span><span id="allocating_the_per-stream_context"></span><span id="ALLOCATING_THE_PER-STREAM_CONTEXT"></span>ストリームごとのコンテキストの割り当て

ストリームごとのコンテキスト構造は、ページングされたプールまたは非ページプールから割り当てることができます。 ストリームごとのコンテキストを割り当てるには、次の例に示すように、 [**Exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)を呼び出します。

```cpp
contextSize = sizeof(SPY_STREAM_CONTEXT) + fileName.Length;
ctx = ExAllocatePoolWithTag(NonPagedPool, 
                            contextSize,
                            MYLEGACYFILTER_CONTEXT_TAG);
```

**注**  は、ページプールからストリームごとのコンテキスト構造を割り当てるフィルターでは、作成完了ルーチンから[**Exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)を呼び出すことはできません。 これは、完了ルーチンを IRQL ディスパッチ\_レベルで呼び出すことができるためです。

 

### <a name="span-idinitializing_the_per-stream_contextspanspan-idinitializing_the_per-stream_contextspanspan-idinitializing_the_per-stream_contextspaninitializing-the-per-stream-context"></a><span id="Initializing_the_Per-Stream_Context"></span><span id="initializing_the_per-stream_context"></span><span id="INITIALIZING_THE_PER-STREAM_CONTEXT"></span>ストリームごとのコンテキストの初期化

ファイルシステムフィルタードライバーは、ストリームごとのコンテキスト構造を初期化するために、 [**Fsrtlinitperstreamcontext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlinitperstreamcontext)を呼び出します。 このルーチンは、コンテキスト構造のコンテキスト部分\_\_ストリームごとに FSRTL\_を初期化します。 (構造体の残りの部分はフィルタードライバーに固有です)。

**注**  フィルタードライバーがファイルストリームごとにストリームごとのコンテキスト構造を1つだけ作成する場合は、 *InstanceId*パラメーターに**NULL**を渡す必要があり[**ます。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlinitperstreamcontext)

 

フィルタードライバーは、ストリームごとのコンテキストをいつでも初期化できます。 ただし、コンテキストをファイルストリームに関連付ける前に実行する必要があります。

 

 




