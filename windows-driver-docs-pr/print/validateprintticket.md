---
title: ValidatePrintTicket の概要
description: 各プラグインは、検証、PrintTicket IPrintOemPrintTicketProvider::ValidatePrintTicket メソッドを呼び出します。
ms.assetid: 3a4cf946-c931-4f71-9f1a-4efec4dfe866
keywords:
- ValidatePrintTicket
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5359a1c015f0b25397bff0d2a0911e7989163d54
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556914"
---
# <a name="validateprintticket-overview"></a>ValidatePrintTicket の概要


Unidrv と PScript5 の印刷ドライバーでは、次の図と一覧を表示するシーケンスを使用して印刷チケットを検証します。

![unidrv と pscript5 のドライバーを印刷する方法を示すダイアグラムが印刷チケットを検証します。](images/ptpcvalpt-uml.gif)

1.  各プラグインを呼び出し、 [ **IPrintOemPrintTicketProvider::ExpandIntentOptions** ](https://msdn.microsoft.com/library/windows/hardware/ff553168)メソッド。

2.  呼び出す、 [ **IPrintOemPrintTicketProvider::ConvertPrintTicketToDevMode** ](https://msdn.microsoft.com/library/windows/hardware/ff553167)メソッド。

3.  各プラグインは、呼び出し**IPrintOemPrintTicketProvider::ConvertPrintTicketToDevMode**のプライベート部分に変換する、 [ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)構造体。

4.  パブリックおよびプライベートな部分を Unidrv または PScript5 印刷ドライバーがサポートする DEVMODEW 構造を検証します。

5.  各プラグイン、DEVMODEW 構造にプライベートな部分を検証します。

6.  呼び出す、 [ **IPrintTicketProvider::ConvertPrintTicketToDevMode** ](https://msdn.microsoft.com/library/windows/hardware/ff554363)メソッド。

7.  各プラグインを呼び出し、 [ **IPrintOemPrintTicketProvider::ConvertDevModeToPrintTicket** ](https://msdn.microsoft.com/library/windows/hardware/ff553161) DEVMODEW 構造体のプライベート部分に変換します。

8.  各プラグインを呼び出し、 [ **IPrintOemPrintTicketProvider::ValidatePrintTicket** ](https://msdn.microsoft.com/library/windows/hardware/ff553184) PrintTicket を検証するメソッド。

 

 




