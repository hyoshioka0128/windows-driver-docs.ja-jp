---
title: モバイル ブロードバンド (MBB) WDF クラス拡張機能 (MBBCx)
description: モバイル ブロード バンド (MBB) WDF クラス拡張 (MBBCx) の概要。
ms.assetid: FA4D1C2D-270B-40C4-A922-8ABDDE4D8444
keywords:
- (MBB モバイル ブロード バンド) WDF クラスの拡張機能、MBBCx、モバイル ブロード バンド NetAdapterCx
ms.date: 03/19/2018
ms.localizationpriority: medium
ms.openlocfilehash: 851489e28a5a2928260c6d73958583c71be2cfde
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384543"
---
# <a name="mobile-broadband-mbb-wdf-class-extension-mbbcx"></a>モバイル ブロードバンド (MBB) WDF クラス拡張機能 (MBBCx)

[!include[MBBCx Beta Prerelease](../mbbcx-beta-prerelease.md)]

Windows 10 の次のリリース以降、Windows Driver Kit (WDK) には、NetAdapterCx で動作するモバイル ブロード バンド (MBB) WDF クラスの拡張機能が含まれています。 MBB NetAdapter クライアント ドライバーは、完全限定の WDF クライアント ドライバーでは何よりもまず、いる NetAdapterCx クライアント ドライバーと同様に他の NIC ドライバーと最後に、MBB クラスの拡張機能 (MBBCx) MBB メディア固有のクライアント ドライバーになります。機能。 次のブロック図は、MBBCx アーキテクチャを示しています。

![MbbCx アーキテクチャ](images/MbbCx.png)

MBB NetAdapter のクライアント ドライバーは、3 つのカテゴリのフレームワークとのリレーションシップに基づいてタスクを実行します。

- 呼び出す[WDF の標準 Api](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_wdf/) Pnp や電源管理などの一般的なデバイス タスク。
- 呼び出す[NetAdapterCx Api](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/#netadaptercx)の送信または受信ネットワーク パケットのような一般的なネットワーク デバイスの操作。
- 呼び出す[MbbCx Api](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/#mbbcx) MBB 固有 MBIM メッセージの処理のようなパスの操作を制御します。

開始する前にする必要がありますについて理解を深めるこれらの概念。

- [Windows Driver Foundation (WDF)](../wdf/using-the-framework-to-develop-a-driver.md)
- [NetAdapter クラスの拡張機能 (NetAdapterCx)](index.md)

このセクションのトピックでは、集中 MBBCx 固有のコードでのみ、基本の NIC の NetAdapterCx クライアント ドライバーを記述する方法を既にご存知と仮定します。

このセクションでは、次のトピックについて説明します。

- [Writing an MBBCx client driver (MBBCx クライアント ドライバーの作成)](writing-an-mbbcx-client-driver.md)
