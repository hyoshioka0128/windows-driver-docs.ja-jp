---
title: フィルター マネージャーとミニフィルター ドライバー アーキテクチャ
description: フィルター マネージャーとミニフィルター ドライバー アーキテクチャ
ms.assetid: d3fde421-3475-4327-95cf-eaa520f5c132
keywords:
- ファイル システム ミニフィルター ドライバー WDK、アーキテクチャ
- ミニフィルター ドライバー WDK、アーキテクチャ
- フィルター マネージャー WDK ファイル システム ミニフィルター
- ファイル システム ミニフィルター ドライバー WDK、フィルター マネージャー
- ミニフィルター ドライバー WDK、フィルター マネージャー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7ecc93c9a3dd9ae42b4b0fe444155b6a959fcf5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341505"
---
# <a name="filter-manager-and-minifilter-driver-architecture"></a>フィルター マネージャーとミニフィルター ドライバー アーキテクチャ


## <span id="ddk_writing_a_driverentry_routine_for_a_minifilter_driver_if"></span><span id="DDK_WRITING_A_DRIVERENTRY_ROUTINE_FOR_A_MINIFILTER_DRIVER_IF"></span>


フィルター マネージャーは、従来のファイル システム フィルターのモデルに準拠しているファイル システム フィルター ドライバーで一般的に必要な機能を公開するカーネル モード ドライバーです。 この機能を利用して、サード パーティの開発者は、特定質の高いより堅牢なドライバーを開発している間、開発プロセスを短縮されミニフィルター ドライバーは、開発が簡単により、従来のファイル システム フィルター ドライバーを記述できます。

このセクションの内容:

[フィルター マネージャーの概念](filter-manager-concepts.md)

[フィルター マネージャー モデルの利点](advantages-of-the-filter-manager-model.md)

[ミニフィルター ドライバーのフィルター マネージャー サポート](filter-manager-support-for-minifilter-drivers.md)

[フィルター マネージャーの操作を制御します。](controlling-filter-manager-operation.md)

[開発/テスト ツール](development-and-testing-tools.md)

[レガシ フィルター ドライバーを移植するためのガイドライン](guidelines-for-porting-legacy-filter-drivers.md)

 

 


