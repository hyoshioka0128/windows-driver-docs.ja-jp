---
title: 要求オブジェクトのコンテキストを使用
description: 要求オブジェクトのコンテキストを使用
ms.assetid: befb4a22-0640-45e3-890e-6ff17969b017
keywords:
- 要求オブジェクト WDK KMDF、コンテキストの領域
- コンテキスト領域 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1fdd1d11b7277e6d194063b7800b5afeb75ba343
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560397"
---
# <a name="using-request-object-context"></a>要求オブジェクトのコンテキストを使用





すべての framework 要求オブジェクト、または、ドライバー、フレームワークによって作成されたかどうかがドライバーによって定義されたコンテキストの領域を含めることができます。 フレームワーク ベースのドライバーでは、framework デバイス オブジェクトを初期化します、ドライバーを呼び出して[ **WdfDeviceInitSetRequestAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff546786)を指定する、 [ **WDF\_オブジェクト\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff552400)コンテキスト場所、デバイスの要求オブジェクトを記述する構造体。

フレームワークは、次のように、要求オブジェクトのコンテキストの領域を割り当てます。

-   ドライバーは、呼び出されたときに指定されたサイズとコンテキストの領域を割り当てますフレームワークでは、ドライバーの要求オブジェクトを作成するときに**WdfDeviceInitSetRequestAttributes**します。

-   ドライバーは、呼び出すことによって追加の要求オブジェクトを作成する場合[ **WdfRequestCreate**](https://msdn.microsoft.com/library/windows/hardware/ff549951)、コンテキストのサイズを指定するには、WDF を提供することで\_オブジェクト\_属性の構造体。

詳細については、framework のオブジェクトのコンテキストの領域へのアクセスの割り当てとは、次を参照してください。[フレームワーク オブジェクト コンテキストの空間](framework-object-context-space.md)します。

 

 





