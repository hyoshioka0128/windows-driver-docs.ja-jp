---
title: 記憶域クラス ドライバーの DriverEntry ルーチン
description: 記憶域クラス ドライバーの DriverEntry ルーチン
ms.assetid: 45e929ff-b4e2-4855-8498-15ec4c30f497
keywords:
- DriverEntry WDK storage
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9972210a1c5d05f248736a66add826fc82a688c9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845086"
---
# <a name="storage-class-drivers-driverentry-routine"></a>記憶域クラス ドライバーの DriverEntry ルーチン


## <span id="ddk_storage_class_drivers_driverentry_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_DRIVERENTRY_ROUTINE_KG"></span>


他の Windows NT カーネルモードの上位レベルのドライバーと同様に、ストレージクラスドライバーの[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンは、次の操作を行う必要があります。

1.  [**Ioallocatedriverobjectextension**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatedriverobjectextension)を呼び出して、適切なサイズのドライバーオブジェクト拡張を割り当てます。

2.  必要に応じて、後で使用するために入力レジストリパスをドライバー拡張機能にコピーし、ドライバー拡張機能を初期化します。

3.  入力ドライバーオブジェクトでディスパッチエントリポイントを定義します。

PnP ドライバーの**Driverentry**ルーチンの詳細については、「 [Driverentry ルーチンを記述する](https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-a-driverentry-routine)」を参照してください。

 

 




