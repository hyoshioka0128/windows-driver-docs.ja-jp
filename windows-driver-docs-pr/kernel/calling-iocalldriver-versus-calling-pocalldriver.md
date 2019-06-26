---
title: PoCallDriver を呼び出すと、保留を呼び出す
description: PoCallDriver を呼び出すと、保留を呼び出す
ms.assetid: a47e2310-e89b-4552-bbe3-d4984ae8b564
keywords:
- PoCallDriver
- アクティブな電源 Irp WDK カーネル
- 電源 Irp WDK カーネル、PoCallDriver と保留
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41e52ccc5b429369008cdf863762b892a4d8fd03
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385268"
---
# <a name="calling-iocalldriver-versus-calling-pocalldriver"></a>PoCallDriver を呼び出すと、保留を呼び出す





ドライバーを呼び出す必要があります Windows Vista 以降、 [**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)の代わりに[ **PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver)、電源 Irp に渡す、次の下位のドライバーです。 Windows Server 2003、Windows XP、および Windows 2000 でドライバーを呼び出す必要があります**PoCallDriver**ではなく、**保留**次の下位ドライバーに電源 Irp を渡す。 ただし、Windows Vista と Windows の以前のバージョンで実行する同じコードを使用するドライバーを呼び出す必要があります**PoCallDriver**ではなく、**保留**します。

以降、Windows Vista で[ **PoRequestPowerIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-porequestpowerirp)と**保留**電源マネージャーが、システム全体で power Irp を正しく同期するようにします。 Windows Server 2003、Windows XP、および Windows 2000 で**PoRequestPowerIrp**、 **PoCallDriver**、および[ **PoStartNextPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-postartnextpowerirp)、電源マネージャーが、システム全体で power Irp を正しく同期するようにします。

システムでは、次のようにアクティブな電源 Irp の数を制限します。

-   複数のシステム電源 IRP (**IRP\_MN\_設定\_POWER**) 常に特定します。

-   複数のデバイス セット power IRP (**IRP\_MN\_設定\_電源)** 任意の時点に各 PDO をアクティブにできます。

-   任意の時点で、システムの任意の場所でアクティブにできる複数のデバイスの電源の電源を突入を必要とする IRP です。

確実に突入の 2 つのデバイスを同時に電源をオンにしないでを電源マネージャーのシステム全体にまたがる active 突入 power Irp を追跡でき、1 つだけが、一度にアクティブにできます。 追加の突入電流がアクティブな IRP の完了まで IRP を開始できません。

突入 Irp でこれらの制限により、突入中にブロックされる可能性 IRP デバイスの電源別のデバイス用の IRP を完了します。 ドライバー開発者は、デバッグ中にこの動作認識する必要があります。

 

 




