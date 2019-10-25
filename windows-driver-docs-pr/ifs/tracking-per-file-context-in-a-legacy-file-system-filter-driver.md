---
title: レガシ ファイル システム フィルター ドライバー内のファイル別コンテキストの追跡
description: レガシ ファイル システム フィルター ドライバー内のファイル別コンテキストの追跡
ms.assetid: 6be3ff10-47e4-47f5-8f15-88a80a16f451
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be0a78af1a8bbd352c3f17c43c0a36a694ffd3bd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840949"
---
# <a name="tracking-per-file-context-in-a-legacy-file-system-filter-driver"></a>レガシ ファイル システム フィルター ドライバー内のファイル別コンテキストの追跡


<div class="alert">
<strong>メモ</strong>  最適な信頼性とパフォーマンスを得るには、従来のファイルシステムフィルタードライバーではなく、<a href="filter-manager-and-minifilter-driver-architecture.md" data-raw-source="[file system minifilter drivers](filter-manager-and-minifilter-driver-architecture.md)">ファイルシステムミニフィルタードライバー</a>を使用することをお勧めします。 また、レガシファイルシステムフィルタードライバーは、直接アクセス (DAX) ボリュームにアタッチできません。 ファイルシステムミニフィルタードライバーの詳細については、「<a href="advantages-of-the-filter-manager-model.md" data-raw-source="[Advantages of the Filter Manager Model](advantages-of-the-filter-manager-model.md)">フィルターマネージャーモデルの利点</a>」を参照してください。 レガシドライバーをミニフィルタードライバーに移植する方法については、「<a href="guidelines-for-porting-legacy-filter-drivers.md" data-raw-source="[Guidelines for Porting Legacy Filter Drivers](guidelines-for-porting-legacy-filter-drivers.md)">レガシフィルタードライバーを移植するためのガイドライン</a>」を参照してください。
</div>
 

レガシファイルシステムフィルタードライバーでは、 [ **\_ファイル\_コンテキストオブジェクトの FSRTL\_** ](https://msdn.microsoft.com/library/windows/hardware/ff547352)をユーザー定義のコンテキスト情報構造に関連付けることによって、ファイルのコンテキスト情報を記録できます。

<div class="alert">
<strong>メモ</strong>  すべてのファイルシステムでファイルごとのコンテキストオブジェクトがサポートされるわけではありません。 ファイルがサポートされているファイルシステムに関連付けられているかどうかを確認するには、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlsupportsperfilecontexts" data-raw-source="[**FsRtlSupportsPerFileContexts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlsupportsperfilecontexts)"><strong>Fsrtlsupportsperfilecontexts</strong></a>マクロを使用します。
</div>
 

[**Fsrtlinitperfilecontext**](https://docs.microsoft.com/previous-versions/ff546161(v=vs.85))マクロを使用して、\_ファイル\_コンテキストオブジェクトごとに FSRTL\_を初期化します。 次に、 [**Fsrtlinsertperfilecontext**](https://msdn.microsoft.com/library/windows/hardware/ff546184)ルーチンを使用して、ファイルを任意のコンテキストオブジェクトに関連付けます。

ファイルシステムランタイムライブラリ (FSRTL) パッケージでファイルコンテキストを追跡するために使用されるポインターを取得するには、 [**FsRtlGetPerFileContextPointer**](https://docs.microsoft.com/previous-versions/ff546051(v=vs.85))マクロを使用します。

フィルタードライバーは、 [**FsRtlLookupPerFileContext**](https://msdn.microsoft.com/library/windows/hardware/ff546930)ルーチンを使用して、ファイルに関連付けられているファイルコンテキストオブジェクトを見つけることができます。 ルーチンでは、構造体の所有者または構造体のインスタンスを指定して、検索を絞り込むことができます。

フィルタードライバーは、 [**Fsrtlremoveperfilecontext**](https://msdn.microsoft.com/library/windows/hardware/ff547226)を使用してコンテキストオブジェクトを削除できます。 ルーチンでは、構造体の所有者または構造体のインスタンスを指定して、検索を絞り込むことができます。

<div class="alert">
<strong>メモ</strong>  ファイルがまだ開いている間は、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff547226" data-raw-source="[**FsRtlRemovePerFileContext**](https://msdn.microsoft.com/library/windows/hardware/ff547226)"><strong>Fsrtlremoveperfilecontext</strong></a>ルーチンを使用してコンテキストオブジェクトを削除してください。 <a href="https://msdn.microsoft.com/library/windows/hardware/ff547290" data-raw-source="[**FsRtlTeardownPerFileContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547290)"><strong>FsRtlTeardownPerFileContexts</strong></a>と混同しないようにしてください。
</div>
 

ファイルシステムは[**FsRtlTeardownPerFileContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547290)を呼び出して、ファイル制御ブロック構造 (FCB) に関連付けられているすべてのフィルターコンテキストが解放されるのを解放します。 **FsRtlTeardownPerFileContexts**ルーチンは、各フィルターコンテキストの\_ファイル\_context オブジェクトの FSRTL\_に指定されている[**FreeCallback**](https://docs.microsoft.com/windows-hardware/drivers/ifs/pfree-function)ルーチンを呼び出します。

 

 




