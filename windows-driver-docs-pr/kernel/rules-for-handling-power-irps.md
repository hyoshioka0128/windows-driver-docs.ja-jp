---
title: 電源 Irp を処理するための規則
description: 電源 Irp を処理するための規則
ms.assetid: ea4a1c57-6184-4160-bf23-b86e3e403388
keywords:
- 電源管理の WDK カーネル、Irp
- Irp WDK の電源管理
- Irp WDK カーネルの電源
- 電源 Irp WDK カーネルでは、規則
- I/O 要求パケット WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b4bfb66815ed1a970e148b5e5839f8ba0e05e67
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551113"
---
# <a name="rules-for-handling-power-irps"></a>電源 Irp を処理するための規則





電源管理をサポートするドライバーに関連する特定の規則に従う必要があります。

* [PoCallDriver を呼び出すと、保留を呼び出す](calling-iocalldriver-versus-calling-pocalldriver.md)power Irp を渡す

* [呼び出す PoStartNextPowerIrp](calling-postartnextpowerirp.md) IRP の [次へ] のパワーを開始するには

* [電源 Irp を渡して](passing-power-irps.md)下ドライバー

* [デバイスがスリープ状態の間の I/O 要求をキュー](queuing-i-o-requests-while-a-device-is-sleeping.md)

* [処理がサポートされていないまたは電源 Irp を認識できません。](handling-unsupported-or-unrecognized-power-irps.md)

* [電源 IRP の処理中に呼び出す ExSetTimerResolution](calling-exsettimerresolution-while-processing-a-power-irp.md)

次のセクションでは、ドライバーがこれらのタスクを実行する方法について説明します。

Irp の電源管理の一覧は、[電源管理のマイナー Irp](power-management-minor-irps.md)を参照してください。

 




