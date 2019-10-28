---
title: OpenPrinter
description: OpenPrinter
ms.assetid: 8bbb46a8-2bba-4d15-a2e2-4770b52d2505
keywords:
- OpenPrinter
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0247bdd77782ed2832d510a716c039942218cf84
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843057"
---
# <a name="openprinter"></a>OpenPrinter


印刷キューが開かれると (`OpenPrinter` 関数を使用)、印刷ドライバーが読み込まれ、 [IPrintTicketProvider インターフェイス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554375(v=vs.85))の次のメソッドがこの順序で呼び出されます。

1.  [**IPrintTicketProvider:: GetSupportedVersions**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554371(v=vs.85))

2.  [**IPrintTicketProvider:: BindPrinter**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554354(v=vs.85))

3.  [**IPrintTicketProvider::QueryDeviceNamespace**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554378(v=vs.85))

Unidrv または PScript5 print ドライバーの**IPrintTicketProvider**インターフェイスのメソッドは、ドライバーによってホストされる各プラグインの**IPrintOemPrintTicketProvider**メソッドを呼び出します。 次の図とリストは、`OpenPrinter` が呼び出されたときに、これらの呼び出しがどのように行われるかを示しています。

![openprinter 呼び出しシーケンスを示す図](images/ptpcopen-uml.gif)

1.  各プラグインに対して、 [**IPrintOemPrintTicketProvider:: GetSupportedVersions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemprintticketprovider-getsupportedversions)を呼び出します。

2.  各プラグインに対して、 [**IPrintOemPrintTicketProvider:: BindPrinter**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff553151(v=vs.85))を呼び出します。

3.  各プラグインに対して、 [**IPrintOemPrintTicketProvider:: QueryDeviceDefaultNamespace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemprintticketprovider-querydevicedefaultnamespace)を呼び出します。

 

 




