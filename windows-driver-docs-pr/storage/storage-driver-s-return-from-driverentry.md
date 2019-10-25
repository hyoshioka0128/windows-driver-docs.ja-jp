---
title: DriverEntry からのストレージ ドライバーの戻り値
description: DriverEntry からのストレージ ドライバーの戻り値
ms.assetid: a5772e9c-ec7b-4570-aaae-d2879f7e0bc7
keywords:
- 戻り値 WDK SCSI
- ScsiPortInitialize
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: b44af3c75239bde4019cee58c591b803f62aa270
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844353"
---
# <a name="storage-drivers-return-from-driverentry"></a>DriverEntry からのストレージ ドライバーの戻り値

[**ScsiPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportinitialize)が制御を返すとき **、driverentry 自体が**制御を返すときに、 [**driverentry**](driverentry-of-scsi-miniport-driver.md)ルーチンは**ScsiPortInitialize**の戻り値を反映します。

ミニポートドライバーが**ScsiPortInitialize**を複数回呼び出す場合、その**Driverentry**ルーチンは**ScsiPortInitialize**によって返される*最も小さい値を伝達する必要があり*ます。 ミニポートドライバーのライターは、 **ScsiPortInitialize**によって返される値についての想定を行うことはできません。
