---
title: コールアウト ドライバーの初期化
description: コールアウト ドライバーの初期化
ms.assetid: c9fbc3d9-fcb9-4087-a3d9-d97c64711305
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95829f01fecd01f92967e301510f8d3e8d73fc0d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824606"
---
# <a name="initializing-a-callout-driver"></a>コールアウト ドライバーの初期化


コールアウトドライバーは、その[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)関数内で自動的に初期化します。 メインの初期化タスクは次のとおりです。

-   [Unload 関数の指定](specifying-an-unload-function.md)

-   [デバイスオブジェクトの作成](creating-a-device-object.md)

-   [フィルターエンジンを使用したコールアウトの登録](registering-callouts-with-the-filter-engine.md)

 

 





