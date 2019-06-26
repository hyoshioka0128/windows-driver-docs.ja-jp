---
title: クリティカル領域と保護された領域
description: クリティカル領域と保護された領域
ms.assetid: 3781498a-45e9-4f24-8fd2-830eed61298c
keywords:
- 非同期プロシージャ呼び出しの WDK カーネル
- Apc WDK カーネル
- クリティカル領域 WDK カーネル
- 保護された領域の WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0cb0c1166abc2a23c67e9077725db4507ac256cf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377148"
---
# <a name="critical-regions-and-guarded-regions"></a>クリティカル領域と保護された領域


内にあるスレッドを*クリティカル領域*Apc のユーザーと無効になっている通常のカーネル Apc を実行します。 内でスレッドを*保護された領域*無効になっているすべての Apc を使用して実行します。

### <a name="critical-regions"></a>クリティカル領域

ドライバーは、入力し、次のように重要な領域を終了します。

-   呼び出す[ **KeEnterCriticalRegion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keentercriticalregion)クリティカル領域を入力します。

-   呼び出す[ **KeLeaveCriticalRegion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keleavecriticalregion)クリティカル領域を終了します。

呼び出しごとに**KeEnterCriticalRegion**に一致する呼び出しがあります。 **KeLeaveCriticalRegion**します。

### <a name="guarded-regions"></a>保護された領域

ドライバーは、入力し、次のように保護された領域を終了します。

-   呼び出す[ **KeEnterGuardedRegion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keenterguardedregion)保護された領域を入力します。

-   呼び出す[ **KeLeaveGuardedRegion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keleaveguardedregion)保護された領域のままにします。

呼び出しごとに**KeEnterGuardedRegion**に一致する呼び出しがあります。 **KeLeaveGuardedRegion**します。

Windows Server 2003 および Windows の以降のバージョン用に開発されたドライバーは、特別なカーネル Apc を無効にするのに保護された領域を使用できます。 ドライバーの以前のオペレーティング システムは、特別なカーネル Apc を無効に APC を現在の IRQL を発生させることによって開発された\_呼び出してレベル[ **KeRaiseIrql**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keraiseirql)します。 使用[ **KeLowerIrql** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kelowerirql)前の値を現在の IRQL を削減します。

 

 




