---
title: UMDF からの WinUSB の呼び出し
description: UMDF からの WinUSB の呼び出し
ms.assetid: 33455d61-0eb3-47ef-998a-6e1b5d7db24e
keywords:
- WinUSB WDK UMDF
- WinUSB WDK UMDF、WinUSB へのエスケープ
- ユーザーモードドライバー WDK UMDF、WinUSB へのエスケープ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a23ec391b2be9a0e3bc5dcb307c2db342b14f5c4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843194"
---
# <a name="calling-winusb-from-umdf"></a>UMDF からの WinUSB の呼び出し


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

ドライバーが USB 固有の UMDF インターフェイスを使用して特定の操作を実行できない場合、UMDF ドライバーは[Winusb 関数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)を直接呼び出すことができます。 WinUSB 関数を呼び出すには、まず[**IWDFUsbTargetDevice:: getwinusbhandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-getwinusbhandle)または[**IWDFUsbInterface:: getwinusbhandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-getwinusbhandle)を呼び出して、ドライバーが winusb インターフェイスハンドルを取得する必要があります。 WinUSB インターフェイスハンドルは、選択した構成の最初のインターフェイスを定義するために使用されます。

詳細については、「 [Winusb 機能を使用して Usb デバイスにアクセスする方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

 

 





