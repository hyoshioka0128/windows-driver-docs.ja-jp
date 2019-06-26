---
title: OpenPrinter
description: OpenPrinter
ms.assetid: 8bbb46a8-2bba-4d15-a2e2-4770b52d2505
keywords:
- OpenPrinter
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03b116662632e42bc5e068060d5d83a6cdd8348f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385965"
---
# <a name="openprinter"></a>OpenPrinter


印刷キューを開いたときに (を使用して、`OpenPrinter`関数)、印刷ドライバーが読み込まれるとの次のメソッド、 [IPrintTicketProvider インターフェイス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554375(v=vs.85))この順序で呼び出されます。

1.  [**IPrintTicketProvider::GetSupportedVersions**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554371(v=vs.85))

2.  [**IPrintTicketProvider::BindPrinter**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554354(v=vs.85))

3.  [**IPrintTicketProvider::QueryDeviceNamespace**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554378(v=vs.85))

メソッド、 **IPrintTicketProvider** Unidrv または PScript5 印刷ドライバーの呼び出しで、インターフェイス、 **IPrintOemPrintTicketProvider**ドライバーによってホストされている各プラグインのメソッド。 次の図とリストの表示方法これら呼び出しが行われるときに`OpenPrinter`が呼び出されます。

![シーケンスを呼び出すようになりましたを示す図](images/ptpcopen-uml.gif)

1.  各プラグインは、呼び出し[ **IPrintOemPrintTicketProvider::GetSupportedVersions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemprintticketprovider-getsupportedversions)します。

2.  各プラグインは、呼び出し[ **IPrintOemPrintTicketProvider::BindPrinter**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff553151(v=vs.85))します。

3.  各プラグインは、呼び出し[ **IPrintOemPrintTicketProvider::QueryDeviceDefaultNamespace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemprintticketprovider-querydevicedefaultnamespace)します。

 

 




