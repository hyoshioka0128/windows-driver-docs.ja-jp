---
title: 文字列オブジェクトの使用
description: このトピックでは、Windows Driver Frameworks (WDF) が文字列オブジェクトを提供するサポートについて説明します。 両方のカーネル モード ドライバー フレームワーク (KMDF) に適用されます。
ms.assetid: b1d52a18-ebd5-4ba7-b5c7-3ef3d298c82e
keywords:
- WDK KMDF の string オブジェクト
- フレームワークは、WDK KMDF、文字列オブジェクトをオブジェクトします。
- WDK KMDF の Unicode 文字列します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c84f1261ac9b812ef5e4aee8d33c15aa15a83f5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372212"
---
# <a name="using-string-objects"></a>文字列オブジェクトの使用


このトピックでは、Windows Driver Frameworks (WDF) が文字列オブジェクトを提供するサポートについて説明します。 カーネル モード ドライバー フレームワーク (KMDF) ドライバーとバージョン 2 でユーザー モード ドライバー フレームワーク (UMDF) ドライバーの両方に適用されます。




WDF では、Unicode 文字列のみを使用します。 すべての framework オブジェクトによって定義されているメソッドには、Unicode 文字列だけがそのまま使用します。

フレームワークの定義、 *framework の string オブジェクト*KMDF および UMDF ドライバーを使用して Unicode 文字列を表現します。

ドライバーが呼び出せる[ **WdfStringCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfstring/nf-wdfstring-wdfstringcreate)文字列オブジェクトを作成し、必要に応じて Unicode 文字列をオブジェクトに割り当てます。

フレームワークのいくつかのオブジェクト メソッド、 [ **WdfRegistryQueryString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistryquerystring)で入力として文字列オブジェクトのハンドルに同意し、文字列、文字列オブジェクトを割り当てます。

文字列オブジェクトに割り当てられている文字列にアクセスするには、ドライバーを呼び出すことができます[ **WdfStringGetUnicodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfstring/nf-wdfstring-wdfstringgetunicodestring)します。

 

 





