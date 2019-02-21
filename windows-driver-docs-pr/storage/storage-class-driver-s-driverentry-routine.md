---
title: 記憶域クラス ドライバー DriverEntry ルーチン
description: 記憶域クラス ドライバー DriverEntry ルーチン
ms.assetid: 45e929ff-b4e2-4855-8498-15ec4c30f497
keywords:
- DriverEntry WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 015544b3d16b63e146965c6737d31e3496e4485c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530719"
---
# <a name="storage-class-drivers-driverentry-routine"></a>記憶域クラス ドライバー DriverEntry ルーチン


## <span id="ddk_storage_class_drivers_driverentry_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_DRIVERENTRY_ROUTINE_KG"></span>


などの他の Windows NT カーネル モードより高度なドライバーを[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ストレージ クラス ドライバーのルーチンは、次を実行する必要があります。

1.  呼び出すことによって適切なサイズのオブジェクトの拡張機能ドライバーを割り当てる[ **IoAllocateDriverObjectExtension**](https://msdn.microsoft.com/library/windows/hardware/ff548233)します。

2.  必要に応じて、後で使用できるドライバーの拡張機能に入力のレジストリ パスをコピーし、ドライバーの拡張機能を初期化します。

3.  入力のドライバ オブジェクトでそのディスパッチ エントリ ポイントを定義します。

PnP ドライバーの詳細については**DriverEntry**ルーチンを参照してください[DriverEntry ルーチンを記述](https://msdn.microsoft.com/library/windows/hardware/ff566402)します。

 

 




