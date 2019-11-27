---
title: サポートされていないか認識できない電源 IRP の処理
description: サポートされていないか認識できない電源 IRP の処理
ms.assetid: 0664389c-f746-4025-969f-8c3b07139026
keywords:
- パワー Irp WDK カーネル、サポートされていません
- サポートされていない電源 Irp WDK カーネル
- 認識されない電源 Irp WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a38190e369f7df027723adc8d3424d7a653299b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836480"
---
# <a name="handling-unsupported-or-unrecognized-power-irps"></a>サポートされていないか認識できない電源 IRP の処理





ドライバーが特定の電源 IRP をサポートしていない場合は、それでも IRP をデバイススタックから次の下位のドライバーに渡す必要があります。 スタックの下位にあるドライバーは、IRP を処理できるように準備されている可能性があり、それを行う機会が必要です。

サポートされていないまたは認識されていない電源 IRP を渡すには、「[電源 irp を渡す](passing-power-irps.md)」で説明されているシーケンスで、次のルーチンを呼び出します。

-   Windows 7 と Windows Vista の場合は、 [**IoskipIoCallDriver Entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)と[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出します。

-   Windows Server 2003、Windows XP、および Windows 2000 では、 [**Postartnextpowerirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)、 **ioskipの場所**、および[**pocalldriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)を呼び出します。

ドライバーは、irp をデバイススタックに渡す前に、IRP 内の何も変更しないようにする必要があります。

 

 




