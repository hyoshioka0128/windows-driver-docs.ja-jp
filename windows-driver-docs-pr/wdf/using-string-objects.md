---
title: 文字列オブジェクトを使用します。
description: このトピックでは、Windows Driver Frameworks (WDF) が文字列オブジェクトを提供するサポートについて説明します。 両方のカーネル モード ドライバー フレームワーク (KMDF) に適用されます。
ms.assetid: b1d52a18-ebd5-4ba7-b5c7-3ef3d298c82e
keywords:
- WDK KMDF の string オブジェクト
- フレームワークは、WDK KMDF、文字列オブジェクトをオブジェクトします。
- WDK KMDF の Unicode 文字列します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7fb8a6cf1d5664e421e47d491e09af7b26bb4eca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551258"
---
# <a name="using-string-objects"></a>文字列オブジェクトを使用します。


このトピックでは、Windows Driver Frameworks (WDF) が文字列オブジェクトを提供するサポートについて説明します。 カーネル モード ドライバー フレームワーク (KMDF) ドライバーとバージョン 2 でユーザー モード ドライバー フレームワーク (UMDF) ドライバーの両方に適用されます。




WDF では、Unicode 文字列のみを使用します。 すべての framework オブジェクトによって定義されているメソッドには、Unicode 文字列だけがそのまま使用します。

フレームワークの定義、 *framework の string オブジェクト*KMDF および UMDF ドライバーを使用して Unicode 文字列を表現します。

ドライバーが呼び出せる[ **WdfStringCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff550046)文字列オブジェクトを作成し、必要に応じて Unicode 文字列をオブジェクトに割り当てます。

フレームワークのいくつかのオブジェクト メソッド、 [ **WdfRegistryQueryString**](https://msdn.microsoft.com/library/windows/hardware/ff549923)で入力として文字列オブジェクトのハンドルに同意し、文字列、文字列オブジェクトを割り当てます。

文字列オブジェクトに割り当てられている文字列にアクセスするには、ドライバーを呼び出すことができます[ **WdfStringGetUnicodeString**](https://msdn.microsoft.com/library/windows/hardware/ff550049)します。

 

 





