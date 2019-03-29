---
title: ソフトウェア ファースト インストール
description: ソフトウェア ファースト インストール
ms.assetid: 2199316d-17d5-463a-8c97-f89c87473f20
keywords:
- インストール アプリケーション WDK、ソフトウェアの最初のインストール
- デバイスのインストール アプリケーション WDK、ソフトウェアの最初のインストール
- 配布中規模 WDK デバイスのインストール、ソフトウェアの最初のインストール
- ソフトウェア最初インストール WDK デバイスのインストール
- インストールの自動実行が有効なアプリケーション WDK
- デバイスのインストールの種類、WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e86fabffcf0e12708ee9936c2752a9ebf37356c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579976"
---
# <a name="software-first-installation"></a>ソフトウェア ファースト インストール


ソフトウェアの最初のインストールでは、ステージング環境とのプレインストール、[ドライバー パッケージ](driver-packages.md)ハードウェアの前にシステムにデバイスが接続されています。 デバイスが接続されて、ドライバー パッケージからドライバーがインストールされます。

デバイスを接続する前に、配布メディアを挿入すると、インストールの自動実行が有効なアプリケーションができます。

-   [インストールの進行中はチェック](checking-for-in-progress-installations.md)、およびその他のインストール操作が進行中である場合に実行を停止します。

-   [デバイスが接続されているかどうかを判断](determining-whether-a-device-is-plugged-in.md)します。

-   [プレインストールのドライバー パッケージ](preinstalling-driver-packages.md)

-   Microsoft インストーラーを使用して、[デバイスに固有のアプリケーションをインストールする](installing-device-specific-applications.md)します。

-   デバイスが「ホットプラグ」の場合にプラグインするユーザーに通知します。

    バスがホット プラグ通知を提供していない場合は、呼び出すことによって再列挙を開始[ **CM_Reenumerate_DevNode**](https://msdn.microsoft.com/library/windows/hardware/ff539763)します。

-   デバイスがホット プラグ可能でない場合に、システムの電源をオフに、デバイスを接続、し、システムをオンにユーザーに通知します。

 

 





