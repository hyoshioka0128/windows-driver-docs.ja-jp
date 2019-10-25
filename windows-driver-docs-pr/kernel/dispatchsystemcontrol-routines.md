---
title: DispatchSystemControl ルーチン
description: DispatchSystemControl ルーチン
ms.assetid: b885a4a3-a9b6-423c-83bb-ee502724b0d0
keywords:
- ディスパッチルーチン WDK カーネル、DispatchSystemControl ルーチン
- システム制御ディスパッチルーチン WDK カーネル
- IRP_MJ_SYSTEM_CONTROL i/o 関数のコード
- DispatchSystemControl ルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14d4b1f204b9f6e30d0149993717b17388f12098
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836811"
---
# <a name="dispatchsystemcontrol-routines"></a>DispatchSystemControl ルーチン





ドライバーの[*DispatchSystemControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンは、 [**irp\_MJ\_システム\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control) I/o 関数コードの irp を処理します。

すべてのドライバーは、 *DispatchSystemControl*ルーチンを提供する必要があります。 このルーチンの目的は、Windows Management Instrumentation (WMI) のサポートを提供することです。 ドライバーで WMI がサポートされているかどうかにかかわらず、このルーチンは IRP を次の下位のドライバーに渡す必要があります。

*DispatchSystemControl*ルーチンを実装する方法と、一般的な WMI をサポートする方法については、「 [Windows Management Instrumentation](implementing-wmi.md)」を参照してください。

 

 




