---
title: UMDF のオブジェクトとインターフェイス
description: UMDF のオブジェクトとインターフェイス
ms.assetid: da816fef-a24f-4456-9d4a-36f291afe8b5
keywords:
- ユーザーモードドライバーフレームワーク WDK、オブジェクト
- ユーザーモードドライバー WDK UMDF、オブジェクト
- オブジェクト WDK UMDF
- UMDF オブジェクト WDK
- インターフェイス WDK UMDF
- フレームワークオブジェクト WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7f60445bcf90e2d9ccbf3209187e5eb4a92dc11
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210724"
---
# <a name="umdf-objects-and-interfaces"></a>UMDF のオブジェクトとインターフェイス


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

ユーザーモードドライバーフレームワーク (UMDF) は、連携するオブジェクトのセットで構成されます。 UMDF は、ユーザーモードデバイスドライバーに公開されている一連のオブジェクトを作成および管理します。 これらのオブジェクトの一部は、アプリケーションによってトリガーされる操作 (i/o 要求など) への応答として、UMDF によって作成されます。一方、ドライバーが UMDF インターフェイスメソッドを呼び出すと、他の UMDF オブジェクトが作成されます。 たとえば、i/o queue オブジェクトを作成するために、ドライバーは[**Iwdfdevice:: CreateIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createioqueue)メソッドを呼び出します。

次のトピックでは、主要なフレームワークオブジェクト、基になるコンポーネントオブジェクトモデル (COM) のサブセット、および UMDF DDI プログラミングモデルについて説明します。

-   [フレームワークオブジェクト](framework-objects.md)
-   [フレームワークオブジェクト階層](framework-object-hierarchy.md)
-   [COM サブセットに基づく UMDF](umdf-based-on-com-subset.md)
-   [UMDF DDI プログラミングモデル](umdf-ddi-programming-model.md)
-   [オブジェクトの有効期間の管理](managing-the-lifetime-of-objects.md)

 

 





