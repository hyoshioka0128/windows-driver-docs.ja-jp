---
title: ファイル システム フィルター ドライバーの概要
description: ファイル システム フィルター ドライバーの概要
ms.assetid: 7947aaa9-57d4-4adf-8214-151a4755939b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8362985cd6818e65fe9504d437ba8a9365a16cae
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379726"
---
# <a name="introduction-to-file-system-filter-drivers"></a>ファイル システム フィルター ドライバーの概要


## <span id="ddk_introduction_to_file_system_filter_drivers_if"></span><span id="DDK_INTRODUCTION_TO_FILE_SYSTEM_FILTER_DRIVERS_IF"></span>


<div class="alert">
<strong>注</strong>最適な信頼性とパフォーマンスは、使用はお勧め<a href="filter-manager-and-minifilter-driver-architecture.md" data-raw-source="[file system minifilter drivers](filter-manager-and-minifilter-driver-architecture.md)">ファイル システム ミニフィルター ドライバー</a>従来のファイル システム フィルター ドライバーの代わりにします。 また、従来のファイル システム フィルター ドライバーは、directaccess (DAX) ボリュームにアタッチできません。 詳細については、ファイル システム ミニフィルター ドライバーは、次を参照してください。<a href="advantages-of-the-filter-manager-model.md" data-raw-source="[Advantages of the Filter Manager Model](advantages-of-the-filter-manager-model.md)">フィルター マネージャー モデルの利点</a>します。 ミニフィルター ドライバーは従来、ドライバーを移植するには、次を参照してください。<a href="guidelines-for-porting-legacy-filter-drivers.md" data-raw-source="[Guidelines for Porting Legacy Filter Drivers](guidelines-for-porting-legacy-filter-drivers.md)">レガシ フィルター ドライバーを移植するためのガイドライン</a>します。
</div>
 

このセクションでは、ファイル システム フィルター ドライバーについて説明します。 次のトピックがあります。

[ファイル システム フィルター ドライバーとは何ですか。](what-is-a-file-system-filter-driver-.md)

[ファイル システム フィルター ドライバーは、デバイス ドライバーではありません。](file-system-filter-drivers-are-not-device-drivers.md)

[ファイル システム フィルター ドライバーをインストールします。](installing-a-file-system-filter-driver.md)

[ファイル システム フィルター ドライバーの初期化](initializing-a-file-system-filter-driver.md)

[ファイル システムまたはボリュームへのフィルターのアタッチ](attaching-a-filter-to-a-file-system-or-volume.md)

 

 




