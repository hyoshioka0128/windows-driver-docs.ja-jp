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
ms.openlocfilehash: f1ac10b79e7937af15051f4702bba69ac0639dd3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573436"
---
# <a name="framework-base-object"></a>フレームワーク ベース オブジェクト


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

フレームワークのベース オブジェクトがによってドライバーに公開される、 [IWDFObject](https://msdn.microsoft.com/library/windows/hardware/ff560200)インターフェイス。 すべての framework オブジェクト型の間で共通する基本的な機能を提供します。 フレームワークのすべてのオブジェクトは、このルート オブジェクトから派生します。

ときにドライバー フレームワーク ベース オブジェクトを作成することによって、 [ **IWDFDriver::CreateWdfObject** ](https://msdn.microsoft.com/library/windows/hardware/ff558906)メソッドでは、最初に登録する、 [IObjectCleanup](https://msdn.microsoft.com/library/windows/hardware/ff556754)オブジェクトが破棄されようとしているときに、フレームワークが、ドライバーに通知するためのインターフェイスします。 ドライバーを後で、使用することができます、 [ **IWDFObject::AssignContext** ](https://msdn.microsoft.com/library/windows/hardware/ff560208)フレームワーク ベース オブジェクトのインスタンス上の通知を受け取る方法を変更するメソッド。

 

 





