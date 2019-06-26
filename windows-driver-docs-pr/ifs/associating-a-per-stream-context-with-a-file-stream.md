---
title: ストリーム別コンテキストとファイル ストリームの関連付け
description: ストリーム別コンテキストとファイル ストリームの関連付け
ms.assetid: 99c93574-2ba6-417a-89a4-a5b9a350a8da
keywords:
- フィルター ドライバー WDK ファイル システム、ストリームのコンテキストの追跡
- ファイル システム フィルター ドライバー WDK、ストリームのコンテキストの追跡
- ストリーム コンテキストを追跡 WDK ファイル システム
- 追跡のストリーム コンテキスト WDK ファイル システム
- ストリーム コンテキスト WDK ファイル システムの関連付け
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01be117e5aa2767536a957ee8f0640ed16a7b77e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385945"
---
# <a name="associating-a-per-stream-context-with-a-file-stream"></a>ストリーム別コンテキストとファイル ストリームの関連付け


## <span id="ddk_associating_a_per_stream_context_with_a_file_stream_if"></span><span id="DDK_ASSOCIATING_A_PER_STREAM_CONTEXT_WITH_A_FILE_STREAM_IF"></span>


ファイル システムが正常に処理後にのみ、ストリームごとの context 構造がファイル ストリームを関連付けることができます、 [ **IRP\_MJ\_作成**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)を開く要求をストリーム。 これは、ファイル システムが、ファイル オブジェクトの FsContext ポインターできます有効と見なされる、ファイル システム フィルター ドライバーによって作成要求を処理した後にのみであります。 FsContext ポインターでは、ファイル ストリームを一意に識別されるため、ファイル オブジェクトが、フィルターが既に認識して - ファイル ストリームを表すかどうかを判断する必要があるし、をフィルターが既に作成のストリーム コンテキスト。 このため、これは重複してわかった作成の完了 (または「作成後の」) のパスの削除にのみ、作成ディスパッチ (または「事前作成」) パスでのストリーム コンテキストを作成するフィルターの珍しくありません。

ファイル システム フィルター ドライバーを呼び出すかどうかが既に別のストリームのコンテキストに関連付けられている同じファイル ストリームを確認する[ **FsRtlLookupPerStreamContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-fsrtllookupperstreamcontext)します。

場合[ **FsRtlLookupPerStreamContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-fsrtllookupperstreamcontext)検索は、次のように同じファイル ストリーム フィルターの既存のストリーム コンテキストは、ストリームごとの新しく作成されたコンテキストを削除する必要があります。

場合[ **FsRtlLookupPerStreamContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-fsrtllookupperstreamcontext)は検索あたりストリーム コンテキストではなく、フィルターが既に作成されて、ファイル ストリームをフィルターを呼び出すことができます[ **FsRtlInsertPerStreamContext** ](https://msdn.microsoft.com/library/windows/hardware/ff546194)に新しく作成されたストリーム コンテキストをファイル ストリームに関連付けます。

後[ **FsRtlInsertPerStreamContext** ](https://msdn.microsoft.com/library/windows/hardware/ff546194)呼びますのストリームのコンテキストで、ファイル システムを削除して解放を担当する前提としています。 かどうか、フィルター ドライバーがのストリーム コンテキストを割り当てます、呼び出しません**FsRtlInsertPerStreamContext** 、フィルター ドライバーは呼び出すことによって解放の役目、 [ **ExFreePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exfreepool).

 

 




