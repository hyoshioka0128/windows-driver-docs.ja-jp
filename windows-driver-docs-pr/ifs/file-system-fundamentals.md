---
title: ファイル システムの基礎
description: ファイル システムの基礎
ms.assetid: 29f0d7cb-9574-489c-affd-31ffdce6abdc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b6c2641f7ae5e26172fe8ca8816b732c1229b06
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552944"
---
# <a name="file-system-fundamentals"></a>ファイル システムの基礎


## <span id="ddk_file_system_fundamentals_if"></span><span id="DDK_FILE_SYSTEM_FUNDAMENTALS_IF"></span>


<div class="alert">
<strong>注</strong>最適な信頼性とパフォーマンスは、使用はお勧め<a href="filter-manager-and-minifilter-driver-architecture.md" data-raw-source="[file system minifilter drivers](filter-manager-and-minifilter-driver-architecture.md)">ファイル システム ミニフィルター ドライバー</a>従来のファイル システム フィルター ドライバーの代わりにします。 また、従来のファイル システム フィルター ドライバーは、directaccess (DAX) ボリュームにアタッチできません。 詳細については、ファイル システム ミニフィルター ドライバーは、次を参照してください。<a href="advantages-of-the-filter-manager-model.md" data-raw-source="[Advantages of the Filter Manager Model](advantages-of-the-filter-manager-model.md)">フィルター マネージャー モデルの利点</a>します。 ミニフィルター ドライバーは従来、ドライバーを移植するには、次を参照してください。<a href="guidelines-for-porting-legacy-filter-drivers.md" data-raw-source="[Guidelines for Porting Legacy Filter Drivers](guidelines-for-porting-legacy-filter-drivers.md)">レガシ フィルター ドライバーを移植するためのガイドライン</a>します。
</div>
 

このセクションには、ファイル システム フィルター ドライバーの開発者にとって重要な基本的なファイル システム ドライバーの概念が導入されています。 次のトピックがについて説明します。

[ドライバーが読み込まれるときにどのようにして決まります](what-determines-when-a-driver-is-loaded.md)

[システムの起動中にファイル システムを処理します。](what-happens-to-file-systems-during-system-boot.md)

[記憶域ボリューム、ストレージ デバイス スタック、およびファイル システム スタック](storage-device-stacks--storage-volumes--and-file-system-stacks.md)

[ボリュームのマウント](mounting-a-volume.md)

 

 




