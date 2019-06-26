---
title: ファイル ストリーム、ストリーム コンテキスト、ストリーム別コンテキスト
description: ファイル ストリーム、ストリーム コンテキスト、ストリーム別コンテキスト
ms.assetid: baea4967-f0d6-4096-aac4-fd38c117b4c6
keywords:
- フィルター ドライバー WDK ファイル システム、ストリームのコンテキストの追跡
- ファイル システム フィルター ドライバー WDK、ストリームのコンテキストの追跡
- ストリーム コンテキストを追跡 WDK ファイル システム
- 追跡のストリーム コンテキスト WDK ファイル システム
- ファイル ストリーム WDK
- ストリームのコントロール ブロックの WDK ファイル システム
- SCB WDK ファイル システム
- ストリーム コンテキスト WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5ca0a1fd9b90ec12a3e0f5e1e66de94507225da
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385555"
---
# <a name="file-streams-stream-contexts-and-per-stream-contexts"></a>ファイル ストリーム、ストリーム コンテキスト、ストリーム別コンテキスト


## <span id="ddk_file_streams_stream_contexts_and_per_stream_contexts_if"></span><span id="DDK_FILE_STREAMS_STREAM_CONTEXTS_AND_PER_STREAM_CONTEXTS_IF"></span>


A*ファイル ストリーム*ファイル データを保持するために使用されるバイトのシーケンスです。 通常、ファイルには、1 つのみのファイル ストリームは、ファイルの既定のデータ ストリーム namely があります。 ただし、複数のデータ ストリームをサポートするファイル システム上の各ファイルは、複数のファイル ストリームを持つことができます。 1 つは、既定のデータ ストリームには名前がありません。 代替データ ストリームを他のユーザーは、. します。 ファイルを開くときに実際には、指定されたファイルのストリームを開いています。

ファイル システムでは、最初にファイル ストリームを開き、ファイル システム固有が作成されます*ストリーム コンテキスト*ファイル制御ブロック (FCB) またはストリーム制御ブロック (SCB) など、構造体であり、でこの構造体のアドレスを格納します。**FsContext**結果のファイル オブジェクトのメンバー。

ローカル ファイル システムでは、I/O サブシステム作成別のファイル オブジェクト (共有読み取りアクセス用など)、もう一度、既に開かれたファイル ストリームが開いている場合がファイル システムが新しいストリーム コンテキストを作成できません。 両方のファイル オブジェクトは、同じストリーム コンテキスト構造体のアドレスを受け取ります。 そのため、ローカル ファイル システムでは、ストリームのコンテキストのポインターを一意に識別ファイル ストリーム。

ストリームをサポートするネットワーク ファイル システムのコンテキスト、もう一度同じネットワークを使用して既に開かれているファイル ストリームが開いている場合は共有名または IP アドレス、動作は、同じローカル ファイル システムです。 I/O サブシステムが、新しいファイル オブジェクトを作成しますが、ファイル システムが新しいストリーム コンテキストを作成できません。 代わりに、同じ割り当てます**FsContext**両方のファイル オブジェクトへのポインターの値。 ただし、別のパス (たとえば、別の共有名、または以前に共有名を使用して開かれたファイルの IP アドレス) を使用して、ファイル ストリームが開かれる場合、ファイル システムは新しいストリーム コンテキストを作成します。 したがって、ストリームごとのコンテキストをサポートするネットワーク ファイル システムの**FsContext**ポインターがファイル ストリームを一意に識別されません。

A*のストリーム コンテキスト*フィルター定義の構造体であるは、 [ **FSRTL\_1 秒あたり\_ストリーム\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff547357)構造体そのメンバーの 1 つとして。 フィルター ドライバーは、各ファイル システムによって開かれたファイル ストリームに関する情報を追跡するためにこの構造体を使用します。

### <a name="span-idfilesystemsupportforper-streamcontextsspanspan-idfilesystemsupportforper-streamcontextsspanspan-idfilesystemsupportforper-streamcontextsspanfile-system-support-for-per-stream-contexts"></a><span id="File_System_Support_for_Per-Stream_Contexts"></span><span id="file_system_support_for_per-stream_contexts"></span><span id="FILE_SYSTEM_SUPPORT_FOR_PER-STREAM_CONTEXTS"></span>Stream あたりのコンテキストのファイル システムのサポート

Microsoft Windows XP で以降のストリーム コンテキストをサポートするファイル システムが含まれているストリームのコンテキストの構造を使用する必要があります、 [ **FSRTL\_詳細\_FCB\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsrtl_advanced_fcb_header)構造体。

関連付けられた特定のファイル ストリームのストリーム コンテキストのグローバル リストは、ファイル システムが所有します。 ファイル システムが新しいストリーム コンテキストを作成します (FSRTL\_[詳細設定]\_FCB\_ヘッダー オブジェクト)、ファイル ストリーム呼び出し[ **FsRtlSetupAdvancedHeader** ](https://msdn.microsoft.com/library/windows/hardware/ff547257)にこのリストを初期化します。 ファイル システム フィルター ドライバーを呼び出すと[ **FsRtlInsertPerStreamContext**](https://msdn.microsoft.com/library/windows/hardware/ff546194)、フィルターによって作成された、ストリームのコンテキストは、グローバル リストに追加されます。

ファイル ストリームの場合は、そのストリーム コンテキストを削除すると、ファイル システムを呼び出します[ **FsRtlTeardownPerStreamContexts** ](https://msdn.microsoft.com/library/windows/hardware/ff547295)フィルターは、ファイル ストリームに関連付けられているすべてのストリーム コンテキストを解放します。 このルーチンを呼び出す、 [ **FreeCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff547357)グローバル リストの各ストリームごとのコンテキストのルーチンです。 なお、 **FreeCallback**ルーチンでは、ファイル ストリームのファイル オブジェクトが既に解放されていると仮定する必要があります。

クエリを実行するかどうか、ファイル システムのストリーム コンテキストの指定されたファイル オブジェクトによって表されるファイル ストリームのサポートを呼び出す[ **FsRtlSupportsPerStreamContexts** ](https://docs.microsoft.com/previous-versions/ff547285(v=vs.85))ファイル オブジェクト。 ファイルの種類によっては、他のユーザーではなく、ファイル システムのストリーム コンテキストをサポート可能性がありますに注意してください。 たとえば、NTFS および FAT は現在できませんのストリーム コンテキスト ページング ファイルの。 そのため場合**FsRtlSupportsPerStreamContexts**返します**TRUE** 、1 つのファイル ストリーム用わけではありませんが返される**TRUE**すべてのファイル ストリーム。

 

 




