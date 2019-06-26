---
title: フレームワーク ベース オブジェクト
description: フレームワーク ベース オブジェクト
ms.assetid: 9d400192-faf0-4d8f-849b-6b955105e21a
keywords:
- UMDF オブジェクト WDK、ベース オブジェクト
- フレームワークは、WDK UMDF、ベース オブジェクトをオブジェクトします。
- ベース オブジェクトの WDK UMDF
- IWDFObject
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6587b58b85a5d32710cb4ff16b620c63460c1541
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368686"
---
# <a name="framework-base-object"></a>フレームワーク ベース オブジェクト


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

フレームワークのベース オブジェクトがによってドライバーに公開される、 [IWDFObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfobject)インターフェイス。 すべての framework オブジェクト型の間で共通する基本的な機能を提供します。 フレームワークのすべてのオブジェクトは、このルート オブジェクトから派生します。

ときにドライバー フレームワーク ベース オブジェクトを作成することによって、 [ **IWDFDriver::CreateWdfObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdriver-createwdfobject)メソッドでは、最初に登録する、 [IObjectCleanup](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iobjectcleanup)オブジェクトが破棄されようとしているときに、フレームワークが、ドライバーに通知するためのインターフェイスします。 ドライバーを後で、使用することができます、 [ **IWDFObject::AssignContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfobject-assigncontext)フレームワーク ベース オブジェクトのインスタンス上の通知を受け取る方法を変更するメソッド。

 

 





