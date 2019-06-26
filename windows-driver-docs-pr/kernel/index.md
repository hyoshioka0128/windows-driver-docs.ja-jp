---
title: カーネルモード ドライバー アーキテクチャ設計ガイド
description: カーネルモード ドライバー アーキテクチャ設計ガイド
ms.assetid: 21c199f3-abc3-4607-a674-eb84b6c3c25a
keywords:
- カーネルモード ドライバー WDK, アーキテクチャ
- カーネルモード ドライバー WDK
ms.date: 06/16/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: b8964add8d2685ba516590f1a87e84b3d10457a0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369804"
---
# <a name="kernel-mode-driver-architecture-design-guide"></a>カーネルモード ドライバー アーキテクチャ設計ガイド





このセクションでは、カーネルモードのプログラミングを理解するための一般的な概念を示し、カーネル プログラミングの特定の手法について説明します。 このセクションは、4 部構成となっています。

-   「[Introduction to Windows Drivers (Windows ドライバーの概要)](introduction-to-windows-drivers.md)」では、Windows コンポーネントの概要、Windows で使用されるデバイス ドライバーの種類、Windows デバイス ドライバーの目的、およびキットに付属する汎用的なデバイス ドライバーのサンプルを示します。

-   「[Kernel-Mode Managers and Libraries (カーネルモードのマネージャーとライブラリ)](kernel-mode-managers-and-libraries.md)」では、Windows オペレーティング システムの主要なカーネルモード コンポーネントを示します。

-   「[Writing WDM Drivers (WDM ドライバーを作成する)](writing-wdm-drivers.md)」では、Windows Driver Model (WDM) を使用してドライバーを作成するために必要な情報を示します。

-   「[Driver Programming Techniques (ドライバーのプログラミング手法)](driver-programming-techniques.md)」では、Windows カーネルモード デバイス ドライバーのプログラミングに使用できる手法について説明します。

    **注**  ドライバーで実装または呼び出すことのできるプログラミング インターフェイスについては、[カーネルモード ドライバー リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)をご覧ください。

     

 

 




