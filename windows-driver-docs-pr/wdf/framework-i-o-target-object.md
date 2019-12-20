---
title: フレームワーク I/O ターゲット オブジェクト
description: フレームワーク I/O ターゲット オブジェクト
ms.assetid: 355a1818-88c9-4989-9141-8445f511f501
keywords:
- UMDF オブジェクト WDK、i/o ターゲットオブジェクト
- フレームワークオブジェクト WDK UMDF、i/o ターゲットオブジェクト
- I/o ターゲットオブジェクト WDK UMDF
- IWDFIoTarget
- WDK UMDF のターゲット
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50da71595f7edc35dedd826575c9e78e46ba4e6a
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210360"
---
# <a name="framework-io-target-object"></a>フレームワーク I/O ターゲット オブジェクト


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

フレームワークの i/o ターゲットオブジェクトは、 [Iwdfiotarget](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiotarget)インターフェイスによってドライバーに公開されます。 I/o ターゲットに関する情報を取得します。これは通常、スタック内の下位のドライバーを表しますが、別の UMDF ドライバーまたはスタックのカーネルモード部分を表すこともできます。 I/o ターゲットオブジェクトは、他のデバイスに要求を送信するための方法を、UMDF ドライバーに提供します。

また、UMDF ドライバーでは、 [IWDFIoTargetStateManagement](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiotargetstatemanagement)インターフェイスを使用して、i/o ターゲットオブジェクトの状態を管理および監視することもできます。

 

 





