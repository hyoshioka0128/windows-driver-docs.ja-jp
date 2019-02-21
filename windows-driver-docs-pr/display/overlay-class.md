---
title: オーバーレイ クラス
description: オーバーレイ クラス
ms.assetid: 698eb8af-ff9a-4c11-b764-6e5773886aaa
keywords:
- オーバーレイ クラス WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82cb57a4a957ab75a5de2efc53946a2f86b34c22
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527924"
---
# <a name="overlay-class"></a>オーバーレイ クラス


Windows Display Driver Model (WDDM) には、再入可能な形式でのオーバーレイ クラスの関数のいずれかへの呼び出しを許可されていません。 つまりが最大で 1 つのスレッド実行できる内で、次の関数のいずれかの特定の時点で。

-   [*DxgkDdiCreateOverlay*](https://msdn.microsoft.com/library/windows/hardware/ff559616)

-   [*DxgkDdiDestroyOverlay*](https://msdn.microsoft.com/library/windows/hardware/ff559642)

-   [*DxgkDdiFlipOverlay*](https://msdn.microsoft.com/library/windows/hardware/ff559655)

-   [*DxgkDdiUpdateOverlay*](https://msdn.microsoft.com/library/windows/hardware/ff560804)

 

 





