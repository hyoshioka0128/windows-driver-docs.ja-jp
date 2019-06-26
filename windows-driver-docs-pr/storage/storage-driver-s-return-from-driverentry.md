---
title: DriverEntry からのストレージ ドライバーの戻り値
description: DriverEntry からのストレージ ドライバーの戻り値
ms.assetid: a5772e9c-ec7b-4570-aaae-d2879f7e0bc7
keywords:
- WDK SCSI の値を返す
- ScsiPortInitialize
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aaf808b5a83f89af3eb050b63d09bacbd635dc96
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368856"
---
# <a name="storage-drivers-return-from-driverentry"></a>DriverEntry からのストレージ ドライバーの戻り値


## <span id="ddk_storage_driver_s_return_from_driverentry_kg"></span><span id="DDK_STORAGE_DRIVER_S_RETURN_FROM_DRIVERENTRY_KG"></span>


ときに[ **ScsiPortInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportinitialize)コントロールを返します、 [ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)ルーチンの戻り値の反映**ScsiPortInitialize**とき**DriverEntry**自体がコントロールを返します。

ミニポート ドライバーを呼び出す場合**ScsiPortInitialize** 2 回以上その**DriverEntry**ルーチン*一番低い値を反映する必要があります*によって返される**ScsiPortInitialize**します。 ミニポート ドライバーのライターによって返される値についてどのような想定を行えません。 **ScsiPortInitialize**します。

 

 




