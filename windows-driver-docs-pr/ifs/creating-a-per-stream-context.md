---
title: ストリーム別コンテキストの作成
description: ストリーム別コンテキストの作成
ms.assetid: e33dba3b-50f7-43d8-b7e8-b7c2c9034d51
keywords:
- フィルター ドライバー WDK ファイル システム、ストリームのコンテキストの追跡
- ファイル システム フィルター ドライバー WDK、ストリームのコンテキストの追跡
- ストリーム コンテキストを追跡 WDK ファイル システム
- 追跡のストリーム コンテキスト WDK ファイル システム
- ストリーム コンテキストを割り当てる
- ストリーム コンテキストを初期化しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a56d96061f2eef94ebe54ba4116adc6f1a767bfd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363544"
---
# <a name="creating-a-per-stream-context"></a>ストリーム別コンテキストの作成


## <span id="ddk_creating_a_per_stream_context_if"></span><span id="DDK_CREATING_A_PER_STREAM_CONTEXT_IF"></span>


通常、ファイル システム フィルター ドライバーを作成、[ストリーム コンテキスト構造](file-streams--stream-contexts--and-per-stream-contexts.md)ファイル ストリーム ファイル ストリームが最初に開かれています。 ただし、構造体のストリーム コンテキストを作成され、操作中にファイル ストリームに関連付けられています。

### <a name="span-idallocatingtheper-streamcontextspanspan-idallocatingtheper-streamcontextspanspan-idallocatingtheper-streamcontextspanallocating-the-per-stream-context"></a><span id="Allocating_the_Per-Stream_Context"></span><span id="allocating_the_per-stream_context"></span><span id="ALLOCATING_THE_PER-STREAM_CONTEXT"></span>Stream あたりのコンテキストの割り当てください。

ストリーム コンテキストの構造体は、ページまたは非ページ プールから割り当てられることができます。 ストリーム コンテキストを割り当てるには、呼び出す[ **exallocatepoolwithtag に**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtag)次の例に示すようにします。

```cpp
contextSize = sizeof(SPY_STREAM_CONTEXT) + fileName.Length;
ctx = ExAllocatePoolWithTag(NonPagedPool, 
                            contextSize,
                            MYLEGACYFILTER_CONTEXT_TAG);
```

**注**  呼び出すことができない場合は、フィルターは、ページ プールからのストリーム コンテキスト構造体を割り当て、 [ **exallocatepoolwithtag に**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtag)からその完了ルーチンを作成します。 これは、IRQL のディスパッチの完了ルーチンを呼び出すことができるため\_レベル。

 

### <a name="span-idinitializingtheper-streamcontextspanspan-idinitializingtheper-streamcontextspanspan-idinitializingtheper-streamcontextspaninitializing-the-per-stream-context"></a><span id="Initializing_the_Per-Stream_Context"></span><span id="initializing_the_per-stream_context"></span><span id="INITIALIZING_THE_PER-STREAM_CONTEXT"></span>Stream あたりのコンテキストを初期化しています

ファイル システム フィルター ドライバー呼び出し[ **FsRtlInitPerStreamContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-fsrtlinitperstreamcontext)構造体のストリーム コンテキストを初期化します。 このルーチンは初期化、FSRTL\_1 秒あたり\_ストリーム\_context 構造体のコンテキストの一部です。 (構造体の残りの部分は、フィルター ドライバー固有です)。

**注**  渡すか、フィルター ドライバーは、ファイル ストリームごとの 1 つだけのストリーム コンテキスト構造を作成する場合**NULL**の*InstanceId*パラメーターを[**FsRtlInitPerStreamContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-fsrtlinitperstreamcontext)します。

 

フィルター ドライバーは、いつでものストリーム コンテキストを初期化できます。 ただし、ファイル ストリームとコンテキストを関連付ける前にする必要があります。

 

 




