---
title: デバイスとコントローラーオブジェクトの解放
description: デバイスとコントローラーオブジェクトの解放
ms.assetid: 35404401-d3a8-4257-b1a3-b16ebe42b181
keywords:
- アンロードルーチン WDK カーネル、非 PnP ドライバー
- PnP 以外のアンロードルーチン WDK カーネル
- デバイスの解放
- コントローラーオブジェクトの解放
- デバイスが WDK カーネルをリリースする
- コントローラーオブジェクト WDK カーネル、リリース
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a66feeaffc0f75c3f2f7f1bacee8670dfdd6d2dc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838458"
---
# <a name="releasing-device-and-controller-objects"></a>デバイスとコントローラーオブジェクトの解放





ドライバーは、デバイスまたはコントローラーのオブジェクトを削除する前に、他のドライバーのオブジェクトへのポインター、オブジェクトを中断するなど、外部リソースへの参照を解放する必要があります。これは、対応するデバイスまたはコントローラーの拡張機能に格納されています。 その後、ドライバーによって作成されたデバイスオブジェクトごとに[**Iodeletedevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice)を呼び出すことができます。 以前に[**IoCreateController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatecontroller)を呼び出した非 WDM ドライバーも[**IoDeleteController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iodeletecontroller)を呼び出す必要があります。

ドライバーがデバイス拡張機能のストレージを提供するカーネル定義オブジェクトは、[*アンロード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)ルーチンが対応するデバイスオブジェクトを使用して**iodeletedevice**を呼び出すと、自動的に解放されます。 一般に、 **Keinitialize * Xxx*** を呼び出すことによって[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)または[*再初期化*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-driver_reinitialize)ルーチンによって設定されたすべてのオブジェクトは、ドライバーがデバイス拡張機能でそのオブジェクトのストレージを提供した場合に**iodeletedevice**を呼び出すことによって解放できます。 たとえば、ドライバーに[*Customtimerdpc*](https://msdn.microsoft.com/library/windows/hardware/ff542983)ルーチンがあり、必要な dpc およびタイマーオブジェクトのストレージがデバイス拡張機能に提供されている場合、 **iodeletedevice**を呼び出すと、これらのシステムリソースが解放されます。

同様に、ドライバーがコントローラー拡張機能にストレージを提供するカーネル定義オブジェクトは、*アンロード*ルーチンが対応するコントローラーオブジェクトを使用して**IoDeleteController**を呼び出すと、自動的に解放されます。

**Driverentry**または*再初期化*ルーチンが特定の種類のデバイスのカウントをインクリメントするために[**IoGetConfigurationInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iogetconfigurationinformation)を呼び出した場合、 *Unload*ルーチンは**IoGetConfigurationInformation**を呼び出す必要もあります。i/o マネージャのグローバル構成情報構造で、対応するデバイスオブジェクトを削除するときに、そのデバイスの数を減らします。

*アンロード*ルーチンは、制御を返す前に、他のドライバールーチンによって解放されていない他のドライバー割り当てリソースも解放します。

 

 




