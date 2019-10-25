---
title: ストリームごとのコンテキストのファイルストリームへの関連付け
description: ストリームごとのコンテキストのファイルストリームへの関連付け
ms.assetid: 99c93574-2ba6-417a-89a4-a5b9a350a8da
keywords:
- フィルタードライバー WDK ファイルシステム、ストリームごとのコンテキスト追跡
- ファイルシステムフィルタードライバー WDK、ストリームごとのコンテキスト追跡
- ストリームごとのコンテキスト追跡 WDK ファイルシステム
- ストリームごとのコンテキストの追跡 WDK ファイルシステム
- ストリームごとのコンテキストの関連付け WDK ファイルシステム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d4f928ad63f8075ad9ba4768f6ec64ae289d4ab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841492"
---
# <a name="associating-a-per-stream-context-with-a-file-stream"></a>ストリームごとのコンテキストのファイルストリームへの関連付け


## <span id="ddk_associating_a_per_stream_context_with_a_file_stream_if"></span><span id="DDK_ASSOCIATING_A_PER_STREAM_CONTEXT_WITH_A_FILE_STREAM_IF"></span>


ストリームごとのコンテキスト構造は、ファイルシステムが[**IRP\_MJ\_CREATE**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)要求を正常に処理してストリームを開くと、ファイルストリームに関連付けることができます。 これは、ファイルシステムが create 要求を処理した後に、ファイルシステムフィルタードライバーによってファイルオブジェクトの FsContext ポインターが有効と見なされることがあるためです。 FsContext ポインターはファイルストリームを一意に識別するため、ファイルオブジェクトが既に表示されているファイルストリームを表しているかどうかを確認する必要があります。この場合、フィルターは既にストリームごとのコンテキストを作成しています。 このため、create dispatch (または "事前作成") パスにストリームごとのコンテキストを作成するフィルターは、重複していると判明しているため、作成完了 (または "作成後") パスでのみ削除することは珍しくありません。

同じファイルストリームを使用して、ストリームごとに別のコンテキストが既に関連付けられているかどうかを確認するために、ファイルシステムフィルタードライバーは[**FsRtlLookupPerStreamContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtllookupperstreamcontext)を呼び出します。

[**FsRtlLookupPerStreamContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtllookupperstreamcontext)が同じファイルストリームのストリームごとの既存のコンテキストを検出した場合、フィルターは、新しく作成されたストリームごとのコンテキストを削除する必要があります。

[**FsRtlLookupPerStreamContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtllookupperstreamcontext)が、ファイルストリーム用に既に作成済みのストリームコンテキストを検出できない場合、フィルターは[**Fsrtlinsertperstreamcontext**](https://msdn.microsoft.com/library/windows/hardware/ff546194)を呼び出して、新しく作成されたストリームコンテキストをファイルストリーム。

ストリームごとのコンテキストに対して[**Fsrtlinsertperstreamcontext**](https://msdn.microsoft.com/library/windows/hardware/ff546194)が呼び出された後、ファイルシステムはそのコンテキストを削除して解放することを前提としています。 フィルタードライバーがストリームごとのコンテキストを割り当て、それに対して**Fsrtlinsertperstreamcontext**を呼び出さない場合でも、フィルタードライバーは、 [**exfreepool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)を呼び出すことによってそれを解放する必要があります。

 

 




