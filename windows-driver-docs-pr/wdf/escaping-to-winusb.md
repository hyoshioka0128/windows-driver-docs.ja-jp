---
title: UMDF から WinUSB の呼び出し
description: UMDF から WinUSB の呼び出し
ms.assetid: 33455d61-0eb3-47ef-998a-6e1b5d7db24e
keywords:
- WinUSB WDK UMDF
- WinUSB WDK UMDF、WinUSB のエスケープ
- ユーザー モード ドライバー WDK UMDF、WinUSB のエスケープ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3d541be43dd9d00e12f688823962347f71baf7a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532529"
---
# <a name="calling-winusb-from-umdf"></a>UMDF から WinUSB の呼び出し


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

UMDF ドライバーを呼び出すことができます[WinUSB Functions](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb)直接場合、ドライバーは、USB 固有 UMDF インターフェイスを使用して、特定の操作を実行することはできません。 WinUSB 関数を呼び出すには、ドライバーする必要があります最初 WinUSB インターフェイスのハンドルを呼び出すことによって取得[ **IWDFUsbTargetDevice::GetWinUsbHandle** ](https://msdn.microsoft.com/library/windows/hardware/ff560369)または[ **IWDFUsbInterface:。GetWinUsbHandle**](https://msdn.microsoft.com/library/windows/hardware/ff560337)します。 WinUSB インターフェイスのハンドルを使用して、選択した構成では、最初のインターフェイスを定義します。

詳細については、次を参照してください。 [WinUSB 関数を使用して、USB デバイスへのアクセス方法](https://msdn.microsoft.com/library/windows/hardware/ff540174)します。

 

 





