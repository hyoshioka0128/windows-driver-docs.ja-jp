---
title: DriverEntry から記憶装置ドライバーの戻り値
description: DriverEntry から記憶装置ドライバーの戻り値
ms.assetid: a5772e9c-ec7b-4570-aaae-d2879f7e0bc7
keywords:
- WDK SCSI の値を返す
- ScsiPortInitialize
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e9d41262f3b4981bf18f5e808db818dbda53054
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551336"
---
# <a name="storage-drivers-return-from-driverentry"></a>DriverEntry から記憶装置ドライバーの戻り値


## <span id="ddk_storage_driver_s_return_from_driverentry_kg"></span><span id="DDK_STORAGE_DRIVER_S_RETURN_FROM_DRIVERENTRY_KG"></span>


ときに[ **ScsiPortInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff564645)コントロールを返します、 [ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff552654)ルーチンの戻り値の反映**ScsiPortInitialize**とき**DriverEntry**自体がコントロールを返します。

ミニポート ドライバーを呼び出す場合**ScsiPortInitialize** 2 回以上その**DriverEntry**ルーチン*一番低い値を反映する必要があります*によって返される**ScsiPortInitialize**します。 ミニポート ドライバーのライターによって返される値についてどのような想定を行えません。 **ScsiPortInitialize**します。

 

 




