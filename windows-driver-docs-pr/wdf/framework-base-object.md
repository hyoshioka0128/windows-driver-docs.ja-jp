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
ms.openlocfilehash: 3d7a4982ed00f90b2c18b6ff19eaceab1ad426d4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843185"
---
# <a name="framework-base-object"></a>フレームワーク ベース オブジェクト


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

フレームワークベースオブジェクトは、 [Iwdfobject](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfobject)インターフェイスによってドライバーに公開されます。 すべてのフレームワークオブジェクトの種類で共通の基本的な機能が用意されています。 すべてのフレームワークオブジェクトは、このルートオブジェクトから派生します。

ドライバーが[**Iwdfdriver:: CreateWdfObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createwdfobject)メソッドの呼び出しを使用してフレームワークのベースオブジェクトを作成する場合、最初に[IObjectCleanup](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iobjectcleanup)インターフェイスを登録して、オブジェクトが次のようになったときにフレームワークからドライバーに通知されるようにすることができます。れる. 後で、ドライバーは[**Iwdfobject:: 割り当てコンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-assigncontext)メソッドを使用して、フレームワークのベースオブジェクトインスタンスで通知を受信する方法を変更できます。

 

 





