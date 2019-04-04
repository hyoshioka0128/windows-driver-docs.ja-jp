---
title: レガシ ファイル システム フィルター ドライバーのファイルごとのコンテキストの追跡
description: レガシ ファイル システム フィルター ドライバーのファイルごとのコンテキストの追跡
ms.assetid: 6be3ff10-47e4-47f5-8f15-88a80a16f451
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2de3dfb56ef892236ffba489ecc96a6bbc70e003
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558582"
---
# <a name="tracking-per-file-context-in-a-legacy-file-system-filter-driver"></a>レガシ ファイル システム フィルター ドライバーのファイルごとのコンテキストの追跡


<div class="alert">
<strong>注</strong>最適な信頼性とパフォーマンスは、使用はお勧め<a href="filter-manager-and-minifilter-driver-architecture.md" data-raw-source="[file system minifilter drivers](filter-manager-and-minifilter-driver-architecture.md)">ファイル システム ミニフィルター ドライバー</a>従来のファイル システム フィルター ドライバーの代わりにします。 また、従来のファイル システム フィルター ドライバーは、directaccess (DAX) ボリュームにアタッチできません。 詳細については、ファイル システム ミニフィルター ドライバーは、<a href="advantages-of-the-filter-manager-model.md" data-raw-source="[Advantages of the Filter Manager Model](advantages-of-the-filter-manager-model.md)">フィルター マネージャー モデルの利点</a>を参照してください。 ミニフィルター ドライバーは従来、ドライバーを移植するには、<a href="guidelines-for-porting-legacy-filter-drivers.md" data-raw-source="[Guidelines for Porting Legacy Filter Drivers](guidelines-for-porting-legacy-filter-drivers.md)">レガシ フィルター ドライバーを移植するためのガイドライン</a>を参照してください。
</div>
 

従来のファイル システム フィルター ドライバーは、関連付けることによってファイルのコンテキスト情報を記録できます、 [ **FSRTL\_1 秒あたり\_ファイル\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff547352)ユーザー定義のオブジェクトコンテキスト情報の構造体。

<div class="alert">
<strong>注</strong>ファイルあたりのコンテキスト オブジェクトをサポートしていないすべてのファイル システム。 ファイルがこれらをサポートするファイル システムに関連付けられているかどうかを確認するには、使用、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff547274" data-raw-source="[**FsRtlSupportsPerFileContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547274)"> <strong>FsRtlSupportsPerFileContexts</strong> </a>マクロ。
</div>
 

使用して、 [ **FsRtlInitPerFileContext** ](https://msdn.microsoft.com/library/windows/hardware/ff546161) 、FSRTL を初期化するためにマクロ\_1 秒あたり\_ファイル\_コンテキスト オブジェクト。 使用して、 [ **FsRtlInsertPerFileContext** ](https://msdn.microsoft.com/library/windows/hardware/ff546184)ルーチンにファイルを任意のコンテキスト オブジェクトに関連付けます。

使用して、 [ **FsRtlGetPerFileContextPointer** ](https://msdn.microsoft.com/library/windows/hardware/ff546051)マクロ ファイルのコンテキストを追跡するために、ファイル システムのランタイム ライブラリ (FSRTL) パッケージで使用されるポインターを取得します。

フィルター ドライバーを使用して、 [ **FsRtlLookupPerFileContext** ](https://msdn.microsoft.com/library/windows/hardware/ff546930)ルーチンをファイルに関連付けられているファイルのコンテキスト オブジェクトを検索します。 ルーチンは、検索を絞り込む、構造体または構造体のインスタンスの所有者を指定できます。

フィルター ドライバーを使用して、コンテキスト オブジェクトを削除できます[ **FsRtlRemovePerFileContext**](https://msdn.microsoft.com/library/windows/hardware/ff547226)します。 ルーチンは、検索を絞り込む、構造体または構造体のインスタンスの所有者を指定できます。

<div class="alert">
<strong>注</strong>のみを使用して、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff547226" data-raw-source="[**FsRtlRemovePerFileContext**](https://msdn.microsoft.com/library/windows/hardware/ff547226)"> <strong>FsRtlRemovePerFileContext</strong> </a>ルーチンは、ファイルがまだ開いている間は、コンテキスト オブジェクトを削除します。 混同しないでください<a href="https://msdn.microsoft.com/library/windows/hardware/ff547290" data-raw-source="[**FsRtlTeardownPerFileContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547290)"> <strong>FsRtlTeardownPerFileContexts</strong></a>します。
</div>
 

ファイル システム呼び出し[ **FsRtlTeardownPerFileContexts** ](https://msdn.microsoft.com/library/windows/hardware/ff547290)が破棄されているファイルごとのコントロール ブロック構造 (FCB) をまだ関連付けられているすべてのフィルター コンテキストを解放します。 **FsRtlTeardownPerFileContexts**ルーチンの呼び出し、 [ **FreeCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff551123) 、FSRTL で指定されているルーチン\_1 秒あたり\_ファイル\_各フィルター コンテキストのコンテキスト オブジェクト。

 

 




