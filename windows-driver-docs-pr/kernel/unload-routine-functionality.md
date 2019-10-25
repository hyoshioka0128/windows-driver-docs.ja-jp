---
title: アンロードのルーチン機能
description: アンロードのルーチン機能
ms.assetid: a36b4687-df1d-498f-b9f3-d13ae2a9a3cd
keywords:
- アンロードルーチン WDK カーネル、機能
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6c136c052e47e516feaac2dfdb44c696fa6ab85
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838375"
---
# <a name="unload-routine-functionality"></a>アンロードのルーチン機能





ドライバーの[*アンロード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)ルーチンの役割は、ドライバーが PnP をサポートしているかどうかによって異なります。

PnP ドライバーの[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンは通常単純であるため、 [Pnp ドライバーの unload ルーチン](pnp-driver-s-unload-routine.md)で説明されているように、これらの*アンロード*ルーチンがあります。

PnP 以外のドライバーの*アンロード*ルーチンでは、デバイスオブジェクトを解放し、ドライバーによって割り当てられたリソースを解放する必要があります。 つまり、ドライバー、デバイス、およびそのリソースを初期化するときに、対応する**Driverentry**によって実行される作業を元に戻し、[*再初期化*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-driver_reinitialize)する必要があります。 詳細について[は、「PnP 以外のドライバーのアンロードルーチン」を](non-pnp-driver-s-unload-routine.md)参照してください。

 

 




