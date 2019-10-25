---
title: GPIO ベースの割り込みリソース
description: 汎用 i/o (GPIO) ピンに割り込みを送信する周辺機器のドライバーは、抽象的な Windows 割り込みリソースとして GPIO 割り込みを取得します。
ms.assetid: 65031C43-917D-4665-BD7F-97D3DDA0A918
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8233ecd148b5daf8539dc8ac95f650de3dd4641
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825035"
---
# <a name="gpio-based-interrupt-resources"></a>GPIO ベースの割り込みリソース


汎用 i/o (GPIO) ピンに割り込みを送信する周辺機器のドライバーは、抽象的な Windows 割り込みリソースとして GPIO 割り込みを取得します。 [カーネルモードドライバーフレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers)(kmdf) ドライバーと[ユーザーモードドライバーフレームワーク](../wdf/overview-of-the-umdf.md)(UMDF) ドライバーは、これらのリソースを[*evtdevicepreparehardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)イベントコールバック関数を介して受け取ります。

GPIO ベースの割り込みリソースを使用する周辺機器ドライバーでは、割り込みが割り込みコントローラーではなく GPIO pin によって生成されるか、プロセッサチップの割り込みピンによって生成されるかなど、低レベルの実装の詳細を無視できます。

GPIO ベースの割り込みは、 **Cmresourcetypeinterrupt**型のリソースです。 この割り込みの構成パラメーターは、割り込みリソースを記述している[**CM\_部分\_リソース\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_partial_resource_descriptor)構造の**u. interrupt**メンバーに含まれています。 割り込みサービスルーチン (ISR) を割り込みに接続するために、UMDF または KMDF ドライバーは、割り込みの作成方法に、割り込みリソースの生の説明[と変換](https://docs.microsoft.com/windows-hardware/drivers/wdf/raw-and-translated-resources)された説明の両方を提供します。

周辺機器の KMDF または UMDF ドライバーは、 [**WdfInterruptCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate)メソッドを呼び出して、デバイスからの割り込みに ISR を接続します。 このメソッドの入力パラメーターの1つは、割り込みの構成情報を格納する[**WDF\_interrupt\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config)構造体へのポインターです。 詳細については、「[ハードウェア割り込みの処理](../wdf/handling-hardware-interrupts.md)」を参照してください。

周辺機器ドライバーで複数の GPIO interrupt リソースが使用されている場合、このドライバーで*は、入力*パラメーターとして提供されている未加工のリソースリストと変換されたリソースの一覧で、これらのリソースが表示される順序に注意する必要があります。関数または**Onのハードウェア**メソッド。 これらの一覧にあるリソースは、プラットフォームファームウェアで記述されている順序で表示されます。この順序は、ドライバーによって予想される順序と一致している必要があります。

 

 




