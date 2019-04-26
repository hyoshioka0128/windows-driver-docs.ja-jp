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
ms.openlocfilehash: e3d18e55bc38642b48a338fde22fd0e26ae2b416
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359788"
---
# <a name="handling-unsupported-or-unrecognized-power-irps"></a>サポートされていないか認識できない電源 IRP の処理





ドライバーが IRP の特定の電源をサポートしていない場合それでも IRP がデバイス スタックを次の下位ドライバーに渡す、必要があります。 下位のスタックでさらに、ドライバーは IRP を処理できるようにする場合があります、これを行う機会を必要とします。

サポートされていないか認識できない power IRP を渡すには、ドライバーに記載されている順序で、次のルーチンを呼び出す必要があります[Power Irp を渡して](passing-power-irps.md):

-   Windows 7 および Windows Vista では、呼び出す[ **IoSkipCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff550355)と[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)します。

-   Windows Server 2003、Windows XP、および Windows 2000、呼び出して[ **PoStartNextPowerIrp**](https://msdn.microsoft.com/library/windows/hardware/ff559776)、 **IoSkipCurrentIrpStackLocation**、および[ **PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)します。

ドライバーは IRP がデバイス スタックを渡す前に、IRP では何も変更されません。

 

 




