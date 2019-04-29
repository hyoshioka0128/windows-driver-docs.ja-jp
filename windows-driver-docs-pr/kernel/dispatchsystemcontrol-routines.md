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
ms.openlocfilehash: 314ea313ef84033e1ca7feb29ca2efa3dd75ee28
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387186"
---
# <a name="dispatchsystemcontrol-routines"></a>DispatchSystemControl ルーチン





ドライバーの[ *DispatchSystemControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンの Irp の処理、 [ **IRP\_MJ\_システム\_コントロール** ](https://msdn.microsoft.com/library/windows/hardware/ff550813) I/O 関数のコード。

すべてのドライバーを提供する必要があります、 *DispatchSystemControl*ルーチン。 このルーチンでは、Windows Management Instrumentation (WMI) のサポートを提供します。 ドライバーが、WMI をサポートするかどうかに関係なく、このルーチンは次の下位のドライバーに IRP を渡す必要があります。

実装する方法については、 *DispatchSystemControl*ルーチンと一般に WMI をサポートする方法[Windows Management Instrumentation](implementing-wmi.md)します。

 

 




