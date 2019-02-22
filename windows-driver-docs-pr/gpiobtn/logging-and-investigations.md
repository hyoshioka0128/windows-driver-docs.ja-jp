---
title: ログ記録と調査
description: このトピックでは、ログ記録と調査の GPIO 実装について説明します。
ms.assetid: 27D6349D-5F92-450B-B9AA-90BA9C5D7E65
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 60b92bcd702c6d59c12a8473c23372540e1c8dce
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538807"
---
# <a name="logging-and-investigations"></a>ログ記録と調査


このトピックでは、ログ記録と調査の GPIO 実装について説明します。

## <a name="span-idlivedebugprintsfromthekerneldebuggerspanspan-idlivedebugprintsfromthekerneldebuggerspanspan-idlivedebugprintsfromthekerneldebuggerspanlive-debug-prints-from-the-kernel-debugger"></a><span id="Live_debug_prints_from_the_kernel_debugger"></span><span id="live_debug_prints_from_the_kernel_debugger"></span><span id="LIVE_DEBUG_PRINTS_FROM_THE_KERNEL_DEBUGGER"></span>カーネル デバッガーからライブ デバッグを出力します


``` syntax
!wmitrace.start buttonTrace -kd ; !wmitrace.enable buttonTrace {5a81715a-84c0-4def-ae38-edde40df5b3a} -level 4 -flag 0xFFFFFFFF
<repro>
!wmitrace.stop buttonTrace
```

## <a name="span-idlogsandinvestigationsspanspan-idlogsandinvestigationsspanspan-idlogsandinvestigationsspanlogs-and-investigations"></a><span id="Logs_and_investigations"></span><span id="logs_and_investigations"></span><span id="LOGS_AND_INVESTIGATIONS"></span>ログと調査


KD から IFR ログ:

``` syntax
!rcdrkd msgpiowin32 
```

LogMan:

``` syntax
 
logman start -ets buttonTrace -p {5a81715a-84c0-4def-ae38-edde40df5b3a} 0xFFFFFFFF 4
<repro>
logman stop -ets buttonTrace
```

### <a name="span-idvalidationsspanspan-idvalidationsspanspan-idvalidationsspanvalidations"></a><span id="Validations"></span><span id="validations"></span><span id="VALIDATIONS"></span>検証

IFR ログまたは Logman を使用して、状態が正常に切り替えられたことを検証することができます。

などドッキング インジケーターの変更が必要ですが、次のエントリする必要があります記載されて、ログ、通知がトリガーされた時点でします。

``` syntax
--- start of log ---
10: Indicator_EvtDevicePrepareHardware - Received 0 resource descriptors, assuming indicator status will be injected via WriteFile
11: Indicator_EvtIoWrite - Indicator state change : DockMode_Indicator : old state : NotDocked
12: Indicator_UpdateRegistryValue - Indicator state update : DockMode_Indicator : new state : Docked
```

 

 




