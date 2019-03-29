---
title: ファイル システム フィルター ドライバー
description: ファイル システム フィルター ドライバー
ms.assetid: 9ea59c4a-d6be-4081-82e7-46539d0a1dbd
keywords:
- フィルター ドライバー WDK ファイル システム
- ファイル システム フィルター ドライバー WDK
- ファイル システム ドライバー WDK、フィルター ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2581ddb31c498e6bb6ffede13838654294c45c36
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574985"
---
# <a name="file-system-filter-drivers"></a>ファイル システム フィルター ドライバー


<div class="alert">
<strong>注</strong>最適な信頼性とパフォーマンスは、使用はお勧め<a href="filter-manager-and-minifilter-driver-architecture.md" data-raw-source="[file system minifilter drivers](filter-manager-and-minifilter-driver-architecture.md)">ファイル システム ミニフィルター ドライバー</a>従来のファイル システム フィルター ドライバーの代わりにします。 また、従来のファイル システム フィルター ドライバーは、directaccess (DAX) ボリュームにアタッチできません。 詳細については、ファイル システム ミニフィルター ドライバーは、次を参照してください。<a href="advantages-of-the-filter-manager-model.md" data-raw-source="[Advantages of the Filter Manager Model](advantages-of-the-filter-manager-model.md)">フィルター マネージャー モデルの利点</a>します。 ミニフィルター ドライバーは従来、ドライバーを移植するには、次を参照してください。<a href="guidelines-for-porting-legacy-filter-drivers.md" data-raw-source="[Guidelines for Porting Legacy Filter Drivers](guidelines-for-porting-legacy-filter-drivers.md)">レガシ フィルター ドライバーを移植するためのガイドライン</a>します。
</div>
 

このセクションには、ファイル システム フィルター ドライバーを記述する次のトピックが含まれています。

-   [ファイル システムの基礎](file-system-fundamentals.md)
-   [ファイル システム フィルター ドライバーの概要](introduction-to-file-system-filter-drivers.md)
-   [Irp と高速な I/O をフィルター処理](filtering-irps-and-fast-i-o.md)
-   [書き込み IRP ディスパッチ ルーチン](writing-irp-dispatch-routines.md)
-   [IRP の完了ルーチンを使用します。](using-irp-completion-routines.md)
-   [レガシ ファイル システム フィルター ドライバーでの Stream あたりのコンテキストの追跡](tracking-per-stream-context-in-a-legacy-file-system-filter-driver.md)
-   [レガシ ファイル システム フィルター ドライバーのファイルごとのコンテキストの追跡](tracking-per-file-context-in-a-legacy-file-system-filter-driver.md)
-   [従来のファイル システム フィルター ドライバーをブロック](blocking-file-system-filter-drivers.md)

 

 




