---
title: SpbAccelerometer ドライバーのサンプル
description: このサンプルの UMDF ドライバーでは、シンプルな周辺機器バス (SPB) に接続されている ADXL345 加速度計を制御します。
ms.assetid: 5951CED5-13D5-44A4-862A-1C34E2122D99
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de11b75466a7a170084dae63d517d1bee3664cf1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382565"
---
# <a name="spbaccelerometer-driver-sample"></a>SpbAccelerometer ドライバーのサンプル


このサンプルの UMDF ドライバーでは、シンプルな周辺機器バス (SPB) に接続されている ADXL345 加速度計を制御します。ADXL345 は、各軸に沿った 16 g +/-最大を測定するのに対応している低電力、3 軸加速です。

**注**  このセクションの情報は、Windows 8.1 および以前のオペレーティング システムに適用されます。 Windows 10 および以降のオペレーティング システム用センサー ドライバーのサンプルを評価するため、次を参照してください。[センサー サンプル ドライバー](https://github.com/Microsoft/Windows-driver-samples/tree/master/sensors)します。 開発および Windows 10 および以降のオペレーティング システム用センサー ドライバーをビルドする方法については、次を参照してください。[作成および配置には、ユニバーサル センサー ドライバー](write-and-deploy-your-universal-sensor-driver.md)します。

 

サンプルは、センサーが完全に I2C バスに接続されていることを前提に書き込まれます。 ドライバーは、プラグ アンド プレイをサポートしていません。 代わりに、ハードウェア プラットフォームの ACPI システム ファームウェアには、センサー デバイスの接続について説明します。 プラグ アンド プレイ マネージャーは、ACPI ドライバーから bus の接続情報を取得、bus の接続を表します接続 ID を作成し、ハードウェア リソースとしてサンプル ドライバーに接続 ID を渡します。 サンプル ドライバーでは、接続 ID を使用して、センサー デバイスへの論理接続を開くし、接続ハンドルを取得します。 ドライバーは、I/O の対象の要求がデバイスに送信されますこのハンドルを指定します。

システムが完全に接続されている ADXL345 センサーをサポートしていない場合でも SPB 経由で他のデバイスを統合するための参照としてこのサンプルを使用することができます。

## <a name="related-topics"></a>関連トピック
[センサー ドライバー開発の基本概念](sensor-driver-development-basics.md)  



