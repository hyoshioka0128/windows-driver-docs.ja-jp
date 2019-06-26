---
title: 記憶域クラス ドライバーの DriverEntry ルーチン
description: 記憶域クラス ドライバーの DriverEntry ルーチン
ms.assetid: 45e929ff-b4e2-4855-8498-15ec4c30f497
keywords:
- DriverEntry WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5cbd50daa298ad6ba550ad518551f281d517ed3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379088"
---
# <a name="storage-class-drivers-driverentry-routine"></a>記憶域クラス ドライバーの DriverEntry ルーチン


## <span id="ddk_storage_class_drivers_driverentry_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_DRIVERENTRY_ROUTINE_KG"></span>


などの他の Windows NT カーネル モードより高度なドライバーを[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ストレージ クラス ドライバーのルーチンは、次を実行する必要があります。

1.  呼び出すことによって適切なサイズのオブジェクトの拡張機能ドライバーを割り当てる[ **IoAllocateDriverObjectExtension**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocatedriverobjectextension)します。

2.  必要に応じて、後で使用できるドライバーの拡張機能に入力のレジストリ パスをコピーし、ドライバーの拡張機能を初期化します。

3.  入力のドライバ オブジェクトでそのディスパッチ エントリ ポイントを定義します。

PnP ドライバーの詳細については**DriverEntry**ルーチンを参照してください[DriverEntry ルーチンを記述](https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-a-driverentry-routine)します。

 

 




