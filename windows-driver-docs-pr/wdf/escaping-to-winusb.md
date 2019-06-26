---
title: UMDF からの WinUSB の呼び出し
description: UMDF からの WinUSB の呼び出し
ms.assetid: 33455d61-0eb3-47ef-998a-6e1b5d7db24e
keywords:
- WinUSB WDK UMDF
- WinUSB WDK UMDF、WinUSB のエスケープ
- ユーザー モード ドライバー WDK UMDF、WinUSB のエスケープ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 179c98ad02aea344d215dc17aff336831f1e4d41
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368715"
---
# <a name="calling-winusb-from-umdf"></a>UMDF からの WinUSB の呼び出し


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

UMDF ドライバーを呼び出すことができます[WinUSB Functions](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)直接場合、ドライバーは、USB 固有 UMDF インターフェイスを使用して、特定の操作を実行することはできません。 WinUSB 関数を呼び出すには、ドライバーする必要があります最初 WinUSB インターフェイスのハンドルを呼び出すことによって取得[ **IWDFUsbTargetDevice::GetWinUsbHandle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-getwinusbhandle)または[ **IWDFUsbInterface:。GetWinUsbHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-getwinusbhandle)します。 WinUSB インターフェイスのハンドルを使用して、選択した構成では、最初のインターフェイスを定義します。

詳細については、次を参照してください。 [WinUSB 関数を使用して、USB デバイスへのアクセス方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

 

 





