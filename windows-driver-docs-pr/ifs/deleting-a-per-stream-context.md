---
title: ストリーム別コンテキストの削除
description: ストリーム別コンテキストの削除
ms.assetid: 293a2ba2-af8a-4c1b-bc35-5e37e6e84d57
keywords:
- フィルター ドライバー WDK ファイル システム、ストリームのコンテキストの追跡
- ファイル システム フィルター ドライバー WDK、ストリームのコンテキストの追跡
- ストリーム コンテキストを追跡 WDK ファイル システム
- 追跡のストリーム コンテキスト WDK ファイル システム
- ストリーム コンテキストを削除します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87cc07573c7c3d28011af77bf28a0ae66f39d7d2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381010"
---
# <a name="deleting-a-per-stream-context"></a>ストリーム別コンテキストの削除


## <span id="ddk_deleting_a_per_stream_context_if"></span><span id="DDK_DELETING_A_PER_STREAM_CONTEXT_IF"></span>


ファイル ストリームに関連付けられているのストリーム コンテキストを不要になったときは削除する必要があります。 2 つの方法のいずれかでは、Stream のコンテキストが削除されます。

-   フィルター ドライバーを呼び出すと、手動で[ **FsRtlRemovePerStreamContext**](https://msdn.microsoft.com/library/windows/hardware/ff547238)します。

-   ファイル システムを呼び出すと、自動的に[ **FsRtlTeardownPerStreamContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547295)、さらに、ストリームのコンテキストの呼び出し[ **FreeCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff547357)ルーチン。

### <a name="span-idwhenthefilterdeletestheper-streamcontextspanspan-idwhenthefilterdeletestheper-streamcontextspanspan-idwhenthefilterdeletestheper-streamcontextspanwhen-the-filter-deletes-the-per-stream-context"></a><span id="When_the_Filter_Deletes_the_Per-Stream_Context"></span><span id="when_the_filter_deletes_the_per-stream_context"></span><span id="WHEN_THE_FILTER_DELETES_THE_PER-STREAM_CONTEXT"></span>フィルターが Stream あたりのコンテキストを削除します

フィルター ドライバーがファイル ストリームの中にファイル ストリームの場合は、そのストリーム コンテキストを削除する必要がある場合は、開いたまま、最初に呼び出す[ **FsRtlRemovePerStreamContext** ](https://msdn.microsoft.com/library/windows/hardware/ff547238)グローバル リストから、コンテキストを削除するには指定されたファイルに関連付けられているコンテキスト。 呼び出した後**FsRtlRemovePerStreamContext**フィルターは、通常、context 構造体を解放します。

**注**   、フィルターの後にドライバーが呼び出されて[ **FsRtlInsertPerStreamContext** ](https://msdn.microsoft.com/library/windows/hardware/ff546194)ファイル ストリームを関連付けるのストリーム コンテキスト構造体には、これには、呼び出す必要があります[ **FsRtlRemovePerStreamContext** ](https://msdn.microsoft.com/library/windows/hardware/ff547238)の解放前にコンテキスト。 それ以外の場合、ファイル ストリームが閉じられたときに、システムがクラッシュします。

 

### <a name="span-idwhentheper-streamcontextsfreecallbackiscalledspanspan-idwhentheper-streamcontextsfreecallbackiscalledspanspan-idwhentheper-streamcontextsfreecallbackiscalledspanwhen-the-per-stream-contexts-freecallback-is-called"></a><span id="When_the_Per-Stream_Context_s_FreeCallback_Is_Called"></span><span id="when_the_per-stream_context_s_freecallback_is_called"></span><span id="WHEN_THE_PER-STREAM_CONTEXT_S_FREECALLBACK_IS_CALLED"></span>Stream あたりのコンテキストの FreeCallback が呼び出された場合

ファイル ストリームがされているときに閉じているか、削除、ファイル システムがファイル ストリームの独自のストリーム コンテキストを解放します。 ファイル システム、この時点で呼び出すも[ **FsRtlTeardownPerStreamContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547295)、さらに呼び出し、 [ **FreeCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff547357)ルーチンすべてのファイル ストリームのコンテキストのグローバル リストに含まれるのストリーム コンテキストを登録します。 (A **FreeCallback**ルーチンが、フィルター ドライバーを呼び出すときに登録されている[ **FsRtlInitPerStreamContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-fsrtlinitperstreamcontext)構造体のストリーム コンテキストを初期化します。 詳細については、次を参照してください**FSRTL\_1 秒あたり\_ストリーム\_コンテキスト**。)。

**注**   、フィルターの後にドライバーが呼び出されて[ **FsRtlInsertPerStreamContext** ](https://msdn.microsoft.com/library/windows/hardware/ff546194)ファイル システムのストリーム コンテキスト構造体、ファイル ストリームに関連付けるには、確認する責任を負います、 [ **FreeCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff547357)ストリームへの参照を開いている任意のされなくなったときに、フィルターのストリーム コンテキストは呼び出されるルーチン。

 

 

 




