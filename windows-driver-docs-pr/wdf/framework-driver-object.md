---
title: フレームワーク ドライバー オブジェクト
description: フレームワーク ドライバー オブジェクト
ms.assetid: 6e9e568c-7e4f-48bd-b351-4be0e12cc15b
keywords:
- UMDF オブジェクト WDK、ドライバーオブジェクト
- フレームワークオブジェクト WDK UMDF、driver オブジェクト
- ドライバーオブジェクト WDK UMDF
- IWDFDriver
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9dd791dd23c12aed943278006bcc1b4a743165e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843180"
---
# <a name="framework-driver-object"></a>フレームワーク ドライバー オブジェクト


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

フレームワークドライバーオブジェクトは、 [Iwdfdriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdriver)インターフェイスによってドライバーに公開されます。 これは、ドライバーのホストプロセスに読み込まれるドライバーイメージのフレームワーク表現です。 フレームワークは、ドライバーホストプロセスに読み込まれたドライバーごとに新しいドライバーオブジェクトを作成します。 **Iwdfdriver**インターフェイスは、ユーザーモードドライバーのメインエントリポイントである[**Idriverentry:: oninitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-oninitialize)メソッドによってドライバーに渡されます。

 

 





