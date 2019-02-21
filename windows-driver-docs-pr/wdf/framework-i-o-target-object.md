---
title: Framework I/O ターゲット オブジェクト
description: Framework I/O ターゲット オブジェクト
ms.assetid: 355a1818-88c9-4989-9141-8445f511f501
keywords:
- UMDF オブジェクト WDK、I/O、ターゲット オブジェクトします。
- フレームワークは、WDK UMDF、I/O のターゲット オブジェクトをオブジェクトします。
- I/O ターゲット オブジェクト WDK UMDF
- IWDFIoTarget
- WDK UMDF のターゲット
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c2861dea511b6e8c975c12861285a0ca8567c60
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556851"
---
# <a name="framework-io-target-object"></a>Framework I/O ターゲット オブジェクト


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

ドライバーによって I/O のフレームワーク ターゲットのオブジェクトが公開されている、 [IWDFIoTarget](https://msdn.microsoft.com/library/windows/hardware/ff559170)インターフェイス。 通常、スタック内の下位のドライバーを表します I/O ターゲットを取得するには、情報を取得しますが、別の UMDF ドライバーまたはスタックのカーネル モードの部分にも表すことができます。 I/O のターゲット オブジェクトは、UMDF ドライバーを別のデバイス要求を送信する方法を提供します。

UMDF ドライバーを使用することも、 [IWDFIoTargetStateManagement](https://msdn.microsoft.com/library/windows/hardware/ff559198)インターフェイスを管理および I/O のターゲット オブジェクトの状態を監視します。

 

 





