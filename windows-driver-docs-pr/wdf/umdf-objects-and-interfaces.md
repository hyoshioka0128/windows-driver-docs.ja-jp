---
title: UMDF オブジェクトとインターフェイス
description: UMDF オブジェクトとインターフェイス
ms.assetid: da816fef-a24f-4456-9d4a-36f291afe8b5
keywords:
- ユーザー モード ドライバー フレームワーク WDK のオブジェクト
- ユーザー モード ドライバー WDK UMDF、オブジェクト
- WDK UMDF オブジェクト
- UMDF オブジェクト WDK
- WDK UMDF インターフェイス
- framework オブジェクト WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5853aaf9a1e60e7333ba9675830149eb101712e7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528358"
---
# <a name="umdf-objects-and-interfaces"></a>UMDF オブジェクトとインターフェイス


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

ユーザー モード ドライバー フレームワーク (UMDF) は、協調動作するオブジェクトのセットで構成されます。 UMDF は作成し、一連のユーザー モード デバイス ドライバーに公開されているオブジェクトを管理します。 これらのオブジェクトの一部には、ドライバーは、UMDF インターフェイスのメソッドを呼び出すとその他の UMDF オブジェクトが作成中に、I/O 要求などのアプリケーションによってトリガーされる操作に対する応答で UMDF によって作成されます。 たとえば、I/O キュー オブジェクトを作成するには、ドライバーは、 [ **IWDFDevice::CreateIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff557020)メソッド。

次のトピックでは、core framework のオブジェクト、コンポーネント オブジェクト モデル (COM) は基になる、および UMDF DDI プログラミング モデルのサブセットについて説明します。

-   [Framework のオブジェクト](framework-objects.md)
-   [Framework のオブジェクト階層](framework-object-hierarchy.md)
-   [COM のサブセットに基づく UMDF](umdf-based-on-com-subset.md)
-   [UMDF DDI プログラミング モデル](umdf-ddi-programming-model.md)
-   [オブジェクトの有効期間を管理します。](managing-the-lifetime-of-objects.md)

 

 





