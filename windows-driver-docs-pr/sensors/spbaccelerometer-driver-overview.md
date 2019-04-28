---
title: SpbAccelerometer ドライバーの概要
description: このサンプルの UMDF ドライバーでは、シンプルな周辺機器バス (SPB) に接続されている ADXL345 加速度計を制御します。
ms.assetid: 355C753D-E5E3-4F8B-B16F-45EFA1E741F3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0bfc90e8722d974ac3cd9094771fb1638b46947c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380008"
---
# <a name="spbaccelerometer-driver-overview"></a>SpbAccelerometer ドライバーの概要


このサンプルの UMDF ドライバーでは、シンプルな周辺機器バス (SPB) に接続されている ADXL345 加速度計を制御します。ADXL345 は、省電力、3 軸加速度計を各軸に沿った 16 g +/-測定できます。 このセンサーは、SPI と I2C のトランスポートをサポートしています。ドライバーのサンプルでは、I2C トランスポートをサポートします。 (ADXL345 とブレイク アウトから掲示板を注文する[SparkFun](https://go.microsoft.com/fwlink/p/?linkid=401463))。

システムがこのセンサーをサポートしていない場合でも I2C 経由で他のデバイスを統合するための参照としてサンプル ドライバーを使用できます。

 

 




