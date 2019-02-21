---
title: シンプルな周辺機器バス (SPB) ドライバーのサンプル
description: このディレクトリにドライバーのサンプルでは、デバイスのカスタム SPB ドライバーを記述するための開始点を提供します。
ms.assetid: E9A667EA-3AE5-4A0E-BC3F-CD442141886B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 691244e8d41c104439b91219e148116edb0d0707
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531679"
---
# <a name="simple-peripheral-bus-spb-driver-samples"></a>シンプルな周辺機器バス (SPB) ドライバーのサンプル


このディレクトリにドライバーのサンプルでは、デバイスのカスタム SPB ドライバーを記述するための開始点を提供します。

## <a name="simple-peripheral-bus-spb"></a>SPB (Simple Peripheral Bus)


| サンプル名                | ソリューション                                                       | 説明                                                                                                                                                                                                                                                                                                                                                                   |
|----------------------------|----------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| スケルトン I2C サンプル ドライバー | [SkeletonI2C](https://go.microsoft.com/fwlink/p/?LinkId=617969) | シンプルな周辺機器バス (SPB) デバイス ドライバー インターフェイス (DDI) に準拠している Windows の KMDF コント ローラーのドライバーをデザインする方法を示します。 SPB では、基になるバス ハードウェアまたはデバイス接続の知識がなくても、クロスプラット フォームで使用するための周辺機器のドライバーを開発するをできるようにする低速シリアル バス (たとえば、I2C、SPI) の抽象化です。 |
| SpbTestTool                | [SpbTestTool](https://go.microsoft.com/fwlink/p/?LinkId=617970) | 識別するハンドルを開く方法を示して、 [SPB のコント ローラー](https://docs.microsoft.com/windows-hardware/drivers/spb/spb-controller-drivers)、KMDF ドライバーから SPB インターフェイスを使用して、GPIO を採用[パッシブ レベルの割り込み](https://docs.microsoft.com/windows-hardware/drivers/wdf/supporting-passive-level-interrupts)します。                                                 |










