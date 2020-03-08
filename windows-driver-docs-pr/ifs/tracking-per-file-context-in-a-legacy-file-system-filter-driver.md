---
title: レガシ ファイル システム フィルター ドライバー内のファイル別コンテキストの追跡
description: レガシ ファイル システム フィルター ドライバー内のファイル別コンテキストの追跡
ms.assetid: 6be3ff10-47e4-47f5-8f15-88a80a16f451
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e991bb3148fb552f93196f8fface4891c6956d3
ms.sourcegitcommit: 8c898615009705db7633649a51bef27a25d72b26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/07/2020
ms.locfileid: "78910453"
---
# <a name="tracking-per-file-context-in-a-legacy-file-system-filter-driver"></a>レガシ ファイル システム フィルター ドライバー内のファイル別コンテキストの追跡

> [!NOTE]
> 最適な信頼性とパフォーマンスを得るには、従来のファイルシステムフィルタードライバーではなく、フィルターマネージャーをサポートする[ファイルシステムミニフィルタードライバー](https://docs.microsoft.com/windows-hardware/drivers/ifs/filter-manager-concepts)を使用します。 レガシドライバーをミニフィルタードライバーに移植する方法については、「[レガシフィルタードライバーを移植するためのガイドライン](guidelines-for-porting-legacy-filter-drivers.md)」を参照してください。

レガシファイルシステムフィルタードライバーは、 [**FSRTL_PER_FILE_CONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsrtl_per_file_context)オブジェクトをユーザー定義のコンテキスト情報構造に関連付けることによって、ファイルのコンテキスト情報を記録できます。

> [!NOTE]
> すべてのファイルシステムでファイルごとのコンテキストオブジェクトがサポートされるわけではありません。 ファイルがサポートされているファイルシステムに関連付けられているかどうかを確認するには、 [**Fsrtlsupportsperfilecontexts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlsupportsperfilecontexts)マクロを使用します。

[**Fsrtlinitperfilecontext**](https://docs.microsoft.com/previous-versions/ff546161(v=vs.85))マクロを使用して、FSRTL_PER_FILE_CONTEXT オブジェクトを初期化します。 次に、 [**Fsrtlinsertperfilecontext**](https://msdn.microsoft.com/library/windows/hardware/ff546184)ルーチンを使用して、ファイルを任意のコンテキストオブジェクトに関連付けます。

ファイルシステムランタイムライブラリ (FSRTL) パッケージでファイルコンテキストを追跡するために使用されるポインターを取得するには、 [**FsRtlGetPerFileContextPointer**](https://docs.microsoft.com/previous-versions/ff546051(v=vs.85))マクロを使用します。

フィルタードライバーは、 [**FsRtlLookupPerFileContext**](https://msdn.microsoft.com/library/windows/hardware/ff546930)ルーチンを使用して、ファイルに関連付けられているファイルコンテキストオブジェクトを見つけることができます。 ルーチンでは、構造体の所有者または構造体のインスタンスを指定して、検索を絞り込むことができます。

フィルタードライバーは、 [**Fsrtlremoveperfilecontext**](https://msdn.microsoft.com/library/windows/hardware/ff547226)を使用してコンテキストオブジェクトを削除できます。 ルーチンでは、構造体の所有者または構造体のインスタンスを指定して、検索を絞り込むことができます。

> [!NOTE]
> ファイルがまだ開いている間は、 [**Fsrtlremoveperfilecontext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlremoveperfilecontext)ルーチンを使用してコンテキストオブジェクトを削除してください。 [**FsRtlTeardownPerFileContexts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlteardownperfilecontexts)と混同しないようにしてください。

ファイルシステムは[**FsRtlTeardownPerFileContexts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlteardownperfilecontexts)を呼び出して、ファイル制御ブロック構造 (FCB) に関連付けられているすべてのフィルターコンテキストが解放されるのを解放します。 **FsRtlTeardownPerFileContexts**ルーチンは、各フィルターコンテキストの FSRTL_PER_FILE_CONTEXT オブジェクトに指定されている[**FreeCallback**](https://docs.microsoft.com/windows-hardware/drivers/ifs/pfree-function)ルーチンを呼び出します。
