---
title: OpenPrinter
description: OpenPrinter
ms.assetid: 8bbb46a8-2bba-4d15-a2e2-4770b52d2505
keywords:
- OpenPrinter
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1fca25391ddbc2f2906e787ae2f2b8617ab8fa5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339912"
---
# <a name="openprinter"></a>OpenPrinter


印刷キューを開いたときに (を使用して、`OpenPrinter`関数)、印刷ドライバーが読み込まれるとの次のメソッド、 [IPrintTicketProvider インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff554375)この順序で呼び出されます。

1.  [**IPrintTicketProvider::GetSupportedVersions**](https://msdn.microsoft.com/library/windows/hardware/ff554371)

2.  [**IPrintTicketProvider::BindPrinter**](https://msdn.microsoft.com/library/windows/hardware/ff554354)

3.  [**IPrintTicketProvider::QueryDeviceNamespace**](https://msdn.microsoft.com/library/windows/hardware/ff554378)

メソッド、 **IPrintTicketProvider** Unidrv または PScript5 印刷ドライバーの呼び出しで、インターフェイス、 **IPrintOemPrintTicketProvider**ドライバーによってホストされている各プラグインのメソッド。 次の図とリストの表示方法これら呼び出しが行われるときに`OpenPrinter`が呼び出されます。

![シーケンスを呼び出すようになりましたを示す図](images/ptpcopen-uml.gif)

1.  各プラグインは、呼び出し[ **IPrintOemPrintTicketProvider::GetSupportedVersions**](https://msdn.microsoft.com/library/windows/hardware/ff553170)します。

2.  各プラグインは、呼び出し[ **IPrintOemPrintTicketProvider::BindPrinter**](https://msdn.microsoft.com/library/windows/hardware/ff553151)します。

3.  各プラグインは、呼び出し[ **IPrintOemPrintTicketProvider::QueryDeviceDefaultNamespace**](https://msdn.microsoft.com/library/windows/hardware/ff553180)します。

 

 




