---
title: サポートされていないか認識できない電源 IRP の処理
description: サポートされていないか認識できない電源 IRP の処理
ms.assetid: 0664389c-f746-4025-969f-8c3b07139026
keywords:
- サポートされていない電源 Irp WDK カーネル
- サポートされていない電源 Irp WDK カーネル
- 認識できない power Irp WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6e8fb7f12329e0551df306a638a7a73d9db0f87
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371902"
---
# <a name="handling-unsupported-or-unrecognized-power-irps"></a>サポートされていないか認識できない電源 IRP の処理





ドライバーが IRP の特定の電源をサポートしていない場合それでも IRP がデバイス スタックを次の下位ドライバーに渡す、必要があります。 下位のスタックでさらに、ドライバーは IRP を処理できるようにする場合があります、これを行う機会を必要とします。

サポートされていないか認識できない power IRP を渡すには、ドライバーに記載されている順序で、次のルーチンを呼び出す必要があります[Power Irp を渡して](passing-power-irps.md):

-   Windows 7 および Windows Vista では、呼び出す[ **IoSkipCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)と[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)します。

-   Windows Server 2003、Windows XP、および Windows 2000、呼び出して[ **PoStartNextPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-postartnextpowerirp)、 **IoSkipCurrentIrpStackLocation**、および[ **PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver)します。

ドライバーは IRP がデバイス スタックを渡す前に、IRP では何も変更されません。

 

 




