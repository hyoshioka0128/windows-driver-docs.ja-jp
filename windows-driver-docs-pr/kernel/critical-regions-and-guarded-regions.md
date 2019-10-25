---
title: クリティカル領域と保護された領域
description: クリティカル領域と保護された領域
ms.assetid: 3781498a-45e9-4f24-8fd2-830eed61298c
keywords:
- 非同期プロシージャ呼び出し WDK カーネル
- Apc WDK カーネル
- 重要なリージョン WDK カーネル
- 保護されたリージョンの WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf81928dd90ff25c9b8279505929c80032447d24
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836971"
---
# <a name="critical-regions-and-guarded-regions"></a>クリティカル領域と保護された領域


*クリティカル領域*内のスレッドは、ユーザー apc と通常のカーネル apc を無効にして実行されます。 保護された*リージョン*内のスレッドは、すべての apc を無効にして実行されます。

### <a name="critical-regions"></a>重要なリージョン

ドライバーは、次のように、重要なリージョンに入力して終了することができます。

-   [**KeEnterCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)を呼び出して、重要なリージョンを入力します。

-   [**KeLeaveCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion)を呼び出して、重要なリージョンを終了します。

**KeEnterCriticalRegion**を呼び出すたびに、 **KeLeaveCriticalRegion**への呼び出しが一致している必要があります。

### <a name="guarded-regions"></a>保護されたリージョン

ドライバーは、次のように保護されたリージョンに入力して終了することができます。

-   [**KeEnterGuardedRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keenterguardedregion)を呼び出して、保護されたリージョンを入力します。

-   [**KeLeaveGuardedRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleaveguardedregion)を呼び出して、保護されたリージョンを脱退します。

**KeEnterGuardedRegion**を呼び出すたびに、 **KeLeaveGuardedRegion**への呼び出しが一致している必要があります。

Windows Server 2003 以降のバージョンの Windows 用に開発されたドライバーでは、保護された領域を使用して特殊なカーネル Apc を無効にすることができます。 以前のオペレーティングシステム用に開発されたドライバーは、 [**Keraiseirql**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirql)を呼び出すことにより、現在の IRQL を APC\_レベルに上げることによって、特殊なカーネル apc を無効にすることができます。 [**Kelower irql**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kelowerirql)を使用して、現在の irql を前の値に下げます。

 

 




