---
title: フレームワーク ベース オブジェクト
description: フレームワーク ベース オブジェクト
ms.assetid: 9d400192-faf0-4d8f-849b-6b955105e21a
keywords:
- UMDF オブジェクト WDK、基本オブジェクト
- フレームワークオブジェクト WDK UMDF、基本オブジェクト
- base オブジェクト WDK UMDF
- IWDFObject
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ca01979829858282d761f17e4e94a8e901ef2e4
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210756"
---
# <a name="framework-base-object"></a>フレームワーク ベース オブジェクト


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

フレームワークベースオブジェクトは、 [Iwdfobject](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfobject)インターフェイスによってドライバーに公開されます。 すべてのフレームワークオブジェクトの種類で共通の基本的な機能が用意されています。 すべてのフレームワークオブジェクトは、このルートオブジェクトから派生します。

ドライバーが[**Iwdfdriver:: CreateWdfObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createwdfobject)メソッドの呼び出しを使用してフレームワークのベースオブジェクトを作成する場合、そのオブジェクトが破棄されようとしているときにフレームワークによってドライバーに通知されるように、最初に[IObjectCleanup](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iobjectcleanup)インターフェイスを登録できます。 後で、ドライバーは[**Iwdfobject:: 割り当てコンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-assigncontext)メソッドを使用して、フレームワークのベースオブジェクトインスタンスで通知を受信する方法を変更できます。

 

 





