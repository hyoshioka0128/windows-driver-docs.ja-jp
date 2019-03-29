---
title: コールアウト ドライバーの初期化
description: コールアウト ドライバーの初期化
ms.assetid: c9fbc3d9-fcb9-4087-a3d9-d97c64711305
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d11b2f02ff7702e9d77b5ce201b11ee87e1d68e9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578610"
---
# <a name="initializing-a-callout-driver"></a>コールアウト ドライバーの初期化


コールアウト ドライバーの初期化自体内でその[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)関数。 メインの初期化タスクは次のとおりです。

-   [アンロード、関数を指定します。](specifying-an-unload-function.md)

-   [デバイス オブジェクトを作成します。](creating-a-device-object.md)

-   [フィルター エンジンとコールアウトを登録します。](registering-callouts-with-the-filter-engine.md)

 

 





