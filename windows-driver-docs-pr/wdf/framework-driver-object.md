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
ms.openlocfilehash: 608e6cb6744d296207520c8409248d49998a378a
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209944"
---
# <a name="framework-driver-object"></a>フレームワーク ドライバー オブジェクト


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

フレームワークドライバーオブジェクトは、 [Iwdfdriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdriver)インターフェイスによってドライバーに公開されます。 これは、ドライバーのホストプロセスに読み込まれるドライバーイメージのフレームワーク表現です。 フレームワークは、ドライバーホストプロセスに読み込まれたドライバーごとに新しいドライバーオブジェクトを作成します。 **Iwdfdriver**インターフェイスは、ユーザーモードドライバーのメインエントリポイントである[**Idriverentry:: oninitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-oninitialize)メソッドによってドライバーに渡されます。

 

 





