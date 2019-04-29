---
title: GPIO のログ記録と調査
description: このトピックでは、ログ記録と GPIO をテストするための調査について説明します。
ms.assetid: 998BF6BC-D931-4555-A8BC-F860DFA9A18F
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b01e4045b0c8e7f2a2acaf32bbf6ad289968430a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326084"
---
# <a name="gpio-logging-and-investigations"></a>GPIO のログ記録と調査


このトピックでは、ログ記録と GPIO をテストするための調査について説明します。

LogMan:

``` syntax
logman start -ets buttonTrace -p {5a81715a-84c0-4def-ae38-edde40df5b3a} 0xFFFFFFFF 4
<repro>

logman stop -ets buttonTrace
```

**注**   WPP トレースになります。

 

テストが失敗した場合、ログ記録が、適切な挿入が実行されたかどうかの診断に役立つことができます。 などドッキング インジケーターの変更が必要ですが、次のエントリする必要があります記載されて、ログ、通知がトリガーされた時点でします。

``` syntax
--- start of log ---
10: Indicator_EvtDevicePrepareHardware - Received 0 resource descriptors, assuming indicator status will be injected via WriteFile
11: Indicator_EvtIoWrite - Indicator state change : DockMode_Indicator : old state : NotDocked
12: Indicator_UpdateRegistryValue - Indicator state update : DockMode_Indicator : new state : Docked
```

インジケーターの注入を実装する方法の詳細については、次を参照してください。、 [Windows 8.1 の GPIO ボタンとインジケーター実装ガイド](gpio-buttons-and-indicators-implementation-guide-for-windows-8-1.md)します。

 

 




