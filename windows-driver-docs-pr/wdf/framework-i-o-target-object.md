---
title: フレームワーク I/O ターゲット オブジェクト
description: フレームワーク I/O ターゲット オブジェクト
ms.assetid: 355a1818-88c9-4989-9141-8445f511f501
keywords:
- UMDF オブジェクト WDK、I/O、ターゲット オブジェクトします。
- フレームワークは、WDK UMDF、I/O のターゲット オブジェクトをオブジェクトします。
- I/O ターゲット オブジェクト WDK UMDF
- IWDFIoTarget
- WDK UMDF のターゲット
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 895fc8917dfc288aaff2e9a5451f7e1aac66fc88
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382869"
---
# <a name="framework-io-target-object"></a>フレームワーク I/O ターゲット オブジェクト


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

ドライバーによって I/O のフレームワーク ターゲットのオブジェクトが公開されている、 [IWDFIoTarget](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfiotarget)インターフェイス。 通常、スタック内の下位のドライバーを表します I/O ターゲットを取得するには、情報を取得しますが、別の UMDF ドライバーまたはスタックのカーネル モードの部分にも表すことができます。 I/O のターゲット オブジェクトは、UMDF ドライバーを別のデバイス要求を送信する方法を提供します。

UMDF ドライバーを使用することも、 [IWDFIoTargetStateManagement](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfiotargetstatemanagement)インターフェイスを管理および I/O のターゲット オブジェクトの状態を監視します。

 

 





