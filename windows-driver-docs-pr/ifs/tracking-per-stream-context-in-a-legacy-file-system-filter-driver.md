---
title: レガシ ファイル システム フィルター ドライバーでの Stream あたりのコンテキストの追跡
description: レガシ ファイル システム フィルター ドライバーでの Stream あたりのコンテキストの追跡
ms.assetid: d908ee30-a433-460c-8c14-883702b4f810
keywords:
- WDK のファイル システムの追跡コンテキスト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76700da337bb0b7d4b6a95c1cfc69f76f95e83b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537150"
---
# <a name="tracking-per-stream-context-in-a-legacy-file-system-filter-driver"></a>レガシ ファイル システム フィルター ドライバーでの Stream あたりのコンテキストの追跡


## <span id="ddk_tracking_per_stream_context_in_a_file_system_filter_driver_if"></span><span id="DDK_TRACKING_PER_STREAM_CONTEXT_IN_A_FILE_SYSTEM_FILTER_DRIVER_IF"></span>


<div class="alert">
<strong>注</strong>最適な信頼性とパフォーマンスは、使用はお勧め<a href="filter-manager-and-minifilter-driver-architecture.md" data-raw-source="[file system minifilter drivers](filter-manager-and-minifilter-driver-architecture.md)">ファイル システム ミニフィルター ドライバー</a>従来のファイル システム フィルター ドライバーの代わりにします。 また、従来のファイル システム フィルター ドライバーは、directaccess (DAX) ボリュームにアタッチできません。 詳細については、ファイル システム ミニフィルター ドライバーは、次を参照してください。<a href="advantages-of-the-filter-manager-model.md" data-raw-source="[Advantages of the Filter Manager Model](advantages-of-the-filter-manager-model.md)">フィルター マネージャー モデルの利点</a>します。 ミニフィルター ドライバーは従来、ドライバーを移植するには、次を参照してください。<a href="guidelines-for-porting-legacy-filter-drivers.md" data-raw-source="[Guidelines for Porting Legacy Filter Drivers](guidelines-for-porting-legacy-filter-drivers.md)">レガシ フィルター ドライバーを移植するためのガイドライン</a>します。
</div>
 

このセクションでは、Microsoft Windows XP およびそれ以降の OS バージョンの追跡のストリーム コンテキストについて説明します。 次のトピックがについて説明します。

[ファイル ストリーム、Stream のコンテキストや Stream ごと](file-streams--stream-contexts--and-per-stream-contexts.md)

[作成して、Stream あたりのコンテキストの構造体を使用](creating-and-using-per-stream-context-structures.md)

 

 




