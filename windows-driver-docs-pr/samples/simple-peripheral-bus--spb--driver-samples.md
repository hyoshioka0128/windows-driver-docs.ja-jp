---
title: SPB (Simple Peripheral Bus) ドライバーのサンプル
description: このディレクトリのドライバーサンプルは、デバイスのカスタム SPB ドライバーを作成するための出発点となります。
ms.assetid: E9A667EA-3AE5-4A0E-BC3F-CD442141886B
ms.date: 11/21/2019
ms.localizationpriority: medium
ms.openlocfilehash: 08b3a11fec5f6c4ebae4c842f25dc09c462c9292
ms.sourcegitcommit: 30fa63ad13fd5e2e883b76a44f0703e01049ffa1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74735184"
---
# <a name="simple-peripheral-bus-spb-driver-samples"></a>SPB (Simple Peripheral Bus) ドライバーのサンプル

このディレクトリのドライバーサンプルは、デバイスのカスタム SPB ドライバーを作成するための出発点となります。

| サンプル | 説明 |
| --- | --- |
| [スケルトン I2C サンプルドライバー](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/skeleton-i2c-sample-driver) | シンプルな周辺機器バス (SPB) device driver interface (DDI) に準拠した Windows 用 KMDF コントローラードライバーを設計する方法を示します。 SPB は、低速のシリアルバス (I2C や SPI など) を抽象化したものであり、基盤となるバスハードウェアやデバイス接続に関する知識がなくても、クロスプラットフォームで使用するために周辺ドライバーを開発することができます。 |
| [SpbTestTool](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/spbtesttool) | [Spb コントローラー](https://docs.microsoft.com/windows-hardware/drivers/spb/spb-controller-drivers)へのハンドルを開き、kmdf ドライバーから spb インターフェイスを使用して、GPIO[パッシブレベルの割り込み](https://docs.microsoft.com/windows-hardware/drivers/wdf/supporting-passive-level-interrupts)を採用する方法を示します。 |
