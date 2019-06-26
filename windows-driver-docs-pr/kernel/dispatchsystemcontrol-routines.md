---
title: DispatchSystemControl ルーチン
description: DispatchSystemControl ルーチン
ms.assetid: b885a4a3-a9b6-423c-83bb-ee502724b0d0
keywords:
- ディスパッチ ルーチンの WDK カーネル、DispatchSystemControl ルーチン
- システム コントロール ディスパッチ ルーチン WDK カーネル
- IRP_MJ_SYSTEM_CONTROL I/O 関数のコード
- DispatchSystemControl ルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4e59815ff2b921e6eb350415632549757b73561
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384971"
---
# <a name="dispatchsystemcontrol-routines"></a>DispatchSystemControl ルーチン





ドライバーの[ *DispatchSystemControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンの Irp の処理、 [ **IRP\_MJ\_システム\_コントロール** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control) I/O 関数のコード。

すべてのドライバーを提供する必要があります、 *DispatchSystemControl*ルーチン。 このルーチンでは、Windows Management Instrumentation (WMI) のサポートを提供します。 ドライバーが、WMI をサポートするかどうかに関係なく、このルーチンは次の下位のドライバーに IRP を渡す必要があります。

実装する方法については、 *DispatchSystemControl*ルーチンと一般に WMI をサポートする方法[Windows Management Instrumentation](implementing-wmi.md)します。

 

 




