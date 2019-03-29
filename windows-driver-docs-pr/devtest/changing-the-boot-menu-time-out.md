---
title: ブート メニューのタイムアウトの変更
description: ブート メニューのタイムアウトの変更
ms.assetid: 447fe656-4bb5-454e-bc89-bab58c8ffaea
keywords:
- Boot.ini ファイル WDK、メニューのタイムアウト
- ブート メニュー タイムアウト、WDK のオプション
- メニュー タイムアウト WDK ブート オプション
- WDK ブート オプションのタイムアウト
- ブート メニュー タイムアウト WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba8c0ff7af8be4ae0f5161d9e026f8f030391ba0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582672"
---
# <a name="changing-the-boot-menu-time-out"></a>ブート メニューのタイムアウトの変更


## <span id="ddk_changing_the_boot_menu_time_out_tools"></span><span id="DDK_CHANGING_THE_BOOT_MENU_TIME_OUT_TOOLS"></span>


ブート メニュー タイムアウトは、ブート メニューが表示される既定のブート エントリが読み込まれる前にどのくらいの期間を決定します。 秒単位で調整することには。

余分な時間が、コンピューターに読み込まれるオペレーティング システムを選択する場合は、タイムアウト値を拡張できます。 または、タイムアウト値を短くには、既定のオペレーティング システムが高速化が開始されるようにします。

Windows、既定のブート メニュー タイムアウト値を変更するのに BCDEdit を使用することができます。

### <a name="span-idusingbcdeditspanspan-idusingbcdeditspanusing-bcdedit"></a><span id="using_bcdedit"></span><span id="USING_BCDEDIT"></span>BCDEdit を使用してください。

ブート メニュー タイムアウトの値を指定するには、使用、 **/timeout**オプション。

```
bcdedit /timeout <timeout>
```

使用して、 **/timeout**オプションし、タイムアウト値を秒単位で指定します。 たとえば、15 秒のタイムアウト値を指定します。

```
bcdedit /timeout 15
```

 

 





