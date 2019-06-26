---
title: コールアウト ドライバーの初期化
description: コールアウト ドライバーの初期化
ms.assetid: c9fbc3d9-fcb9-4087-a3d9-d97c64711305
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1838df6b009087791ad9811ecdd702793b422412
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371850"
---
# <a name="initializing-a-callout-driver"></a>コールアウト ドライバーの初期化


コールアウト ドライバーの初期化自体内でその[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)関数。 メインの初期化タスクは次のとおりです。

-   [アンロード、関数を指定します。](specifying-an-unload-function.md)

-   [デバイス オブジェクトを作成します。](creating-a-device-object.md)

-   [フィルター エンジンとコールアウトを登録します。](registering-callouts-with-the-filter-engine.md)

 

 





