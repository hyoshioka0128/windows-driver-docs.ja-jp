---
title: ファイル ストリーム、ストリーム コンテキスト、ストリーム別コンテキスト
description: ファイル ストリーム、ストリーム コンテキスト、ストリーム別コンテキスト
ms.assetid: baea4967-f0d6-4096-aac4-fd38c117b4c6
keywords:
- フィルタードライバー WDK ファイルシステム、ストリームごとのコンテキスト追跡
- ファイルシステムフィルタードライバー WDK、ストリームごとのコンテキスト追跡
- ストリームごとのコンテキスト追跡 WDK ファイルシステム
- ストリームごとのコンテキストの追跡 WDK ファイルシステム
- ファイルストリーム WDK
- ストリームコントロールが WDK ファイルシステムをブロックする
- SCB WDK ファイルシステム
- ストリームコンテキスト WDK ファイルシステム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0d256eea30827f95b7777ff6a18149c5f6d44ee
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841413"
---
# <a name="file-streams-stream-contexts-and-per-stream-contexts"></a>ファイル ストリーム、ストリーム コンテキスト、ストリーム別コンテキスト


## <span id="ddk_file_streams_stream_contexts_and_per_stream_contexts_if"></span><span id="DDK_FILE_STREAMS_STREAM_CONTEXTS_AND_PER_STREAM_CONTEXTS_IF"></span>


*ファイルストリーム*は、ファイルデータを保持するために使用されるバイトのシーケンスです。 通常、ファイルには、ファイルストリーム (ファイルの既定のデータストリーム) が1つだけあります。 ただし、複数のデータストリームをサポートするファイルシステムでは、各ファイルに複数のファイルストリームを含めることができます。 これらのうちの1つは、名前のない既定のデータストリームです。 その他の名前は代替データストリームです。 ファイルを開くと、実際には、指定されたファイルのストリームが開かれます。

ファイルシステムがファイルストリームを初めて開くと、ファイル制御ブロック (FCB) やストリーム制御ブロック (SCB) などのファイルシステム固有の*ストリームコンテキスト*構造が作成され、この構造体のアドレスが**fscontext**に格納されます。結果として得られるファイルオブジェクトのメンバー。

ローカルファイルシステムの場合、既に開いているファイルストリームが再び開かれた場合 (共有読み取りアクセスの場合など)、i/o サブシステムは別のファイルオブジェクトを作成しますが、ファイルシステムは新しいストリームコンテキストを作成しません。 両方のファイルオブジェクトは、同じストリームコンテキスト構造のアドレスを受け取ります。 したがって、ローカルファイルシステムの場合、ストリームコンテキストポインターはファイルストリームを一意に識別します。

ストリームごとのコンテキストをサポートするネットワークファイルシステムの場合、既に開いているファイルストリームが同じネットワーク共有名または IP アドレスを使用して再度開かれると、ローカルファイルシステムの場合と同じ動作になります。 I/o サブシステムは新しいファイルオブジェクトを作成しますが、ファイルシステムは新しいストリームコンテキストを作成しません。 代わりに、同じ**Fscontext**ポインター値が両方のファイルオブジェクトに割り当てられます。 ただし、ファイルストリームが別のパス (たとえば、共有名を使用して以前に開かれたファイルの IP アドレス) を使用して開かれている場合は、ファイルシステムによって新しいストリームコンテキストが作成されます。 このため、ストリームごとのコンテキストをサポートするネットワークファイルシステムでは、 **Fscontext**ポインターはファイルストリームを一意に識別しません。

*ストリームごとのコンテキスト*とは、そのメンバーの1つとして、 [ **\_ストリーム\_コンテキスト構造の FSRTL\_** ](https://msdn.microsoft.com/library/windows/hardware/ff547357)を含むフィルター定義の構造体です。 フィルタードライバーは、この構造を使用して、ファイルシステムによって開かれている各ファイルストリームに関する情報を追跡します。

### <a name="span-idfile_system_support_for_per-stream_contextsspanspan-idfile_system_support_for_per-stream_contextsspanspan-idfile_system_support_for_per-stream_contextsspanfile-system-support-for-per-stream-contexts"></a><span id="File_System_Support_for_Per-Stream_Contexts"></span><span id="file_system_support_for_per-stream_contexts"></span><span id="FILE_SYSTEM_SUPPORT_FOR_PER-STREAM_CONTEXTS"></span>ファイルシステムでのストリームごとのコンテキストのサポート

Microsoft Windows XP 以降では、ストリームごとのコンテキストをサポートするファイルシステムでは、 [**FSRTL\_ADVANCED\_FCB\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsrtl_advanced_fcb_header)構造を含むストリームコンテキスト構造を使用する必要があります。

特定のファイルストリームに関連付けられているストリームごとのコンテキストのグローバルリストは、ファイルシステムによって所有されています。 ファイルストリームの新しいストリームコンテキスト (FSRTL\_ADVANCED\_FCB\_HEADER オブジェクト) がファイルシステムによって作成されると、 [**Fsrtlsetupadvanced ヘッダー**](https://msdn.microsoft.com/library/windows/hardware/ff547257)が呼び出され、このリストが初期化されます。 ファイルシステムフィルタードライバーが[**Fsrtlinsertperstreamcontext**](https://msdn.microsoft.com/library/windows/hardware/ff546194)を呼び出すと、フィルターによって作成されたストリームごとのコンテキストがグローバルリストに追加されます。

ファイルストリームのストリームコンテキストを削除すると、ファイルシステムは[**FsRtlTeardownPerStreamContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547295)を呼び出し、フィルターがファイルストリームに関連付けたストリームごとのコンテキストをすべて解放します。 このルーチンは、グローバルリスト内のストリームごとのコンテキストごとに[**FreeCallback**](https://msdn.microsoft.com/library/windows/hardware/ff547357)ルーチンを呼び出します。 **FreeCallback**ルーチンは、ファイルストリームのファイルオブジェクトが既に解放されていることを前提としている必要があります。

ファイルシステムが、指定されたファイルオブジェクトによって表されるファイルストリームのストリームごとのコンテキストをサポートするかどうかを照会するには、ファイルオブジェクトに対して[**Fsrtlsupportsperstreamcontexts**](https://docs.microsoft.com/previous-versions/ff547285(v=vs.85))を呼び出します。 ファイルシステムでは、ファイルの種類によってはストリームごとのコンテキストがサポートされる場合がありますが、それ以外はサポートされないことに注意してください。 たとえば、NTFS および FAT では、現在、ページングファイルのストリームごとのコンテキストをサポートしていません。 したがって、 **Fsrtlsupportsperstreamcontexts**が1つのファイルストリームに対して**true**を返す場合、すべてのファイルストリームに対して**true**が返されるとは限りません。

 

 




