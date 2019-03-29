---
title: カーネルモード ドライバーの設計目標
description: カーネルモード ドライバーの設計目標
ms.assetid: 2799556e-0359-4388-acf3-74d90eb86a0f
keywords:
- カーネル モード ドライバー WDK、設計目標
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16e01631509e6ae9bc58d0c88bf15bdc9b2a3e02
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573226"
---
# <a name="design-goals-for-kernel-mode-drivers"></a>カーネルモード ドライバーの設計目標





カーネル モード ドライバーでは、特にシステム I/O マネージャーのオペレーティング システムの設計目標の多くを共有します。 カーネル モード ドライバーはデザインされています。

-   [ポータブル](portable.md)別の 1 つのプラットフォームからです。

-   [構成可能な](configurable.md)さまざまなハードウェアおよびソフトウェア プラットフォームにします。

-   [常に preemptible と常に中断](always-preemptible-and-always-interruptible.md)します。

-   [マルチプロセッサ セーフ](multiprocessor-safe.md)マルチプロセッサ プラットフォーム。

-   [オブジェクトに基づく](object-based.md)します。

-   [I/O を再利用可能な Irp のパケットに基づく](packet-driven-i-o-with-reusable-irps.md)します。

-   対応[非同期 I/O をサポートしている](supporting-asynchronous-i-o.md)します。

 

 




