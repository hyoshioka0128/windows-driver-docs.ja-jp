---
title: 64 ビット システムへのデバイスのインストール
description: 64 ビット システムへのデバイスのインストール
ms.assetid: 76d9bff7-6429-4d20-9790-a41ed2cb1bdd
keywords:
- 64 ビットの WDK デバイスのインストール
- デバイスのインストール WDK、64 ビット システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6b3ee167eb7c8f690175b440f4a45e48c0112d4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387127"
---
# <a name="device-installations-on-64-bit-systems"></a>64 ビット システムへのデバイスのインストール





作成するときに、次の手順にする必要があります、デバイスは 32 ビット プラットフォームと 64 ビット プラットフォームの両方でインストールする場合、[ドライバー パッケージ](driver-packages.md):

-   すべてのカーネル モード ドライバーの 32 ビットと 64 ビットの両方のコンパイルを提供*デバイス インストール アプリケーション*、*クラス インストーラー*と*共同インストーラー*します。 詳細については、次を参照してください。 [Your のドライバーを 64 ビット Windows に移植](https://docs.microsoft.com/windows-hardware/drivers/kernel/porting-your-driver-to-64-bit-windows)します。

-   使用する 1 つまたは複数のクロス プラットフォーム INF ファイルを提供*INF セクションを装飾*プラットフォームに固有のインストールの動作を制御します。

場合[デバイス インストール アプリケーションを記述して](writing-a-device-installation-application.md)、32 ビット バージョンは、既定のバージョンである必要があります。 32 ビット バージョンはユーザーが、配布のディスクを挿入するときに自動的に開始できるように、(Microsoft Windows SDK のドキュメントで説明) を自動実行、して呼び出す必要があります。

アプリケーションの 32 ビット バージョンがによって返される値を確認する必要があります[ **UpdateDriverForPlugAndPlayDevices**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa)します。 ERROR_IN_WOW64 を戻り値には、32 ビット アプリケーションは、64 ビット プラットフォームで実行されていると、受信トレイのドライバーを更新することはできません。 代わりに、呼び出す必要があります[ **CreateProcess** ](https://docs.microsoft.com/windows/desktop/api/processthreadsapi/nf-processthreadsapi-createprocessa) (Windows SDK のドキュメントで説明)、アプリケーションの 64 ビット バージョンを開始します。 64 ビット バージョンを呼び出して**UpdateDriverForPlugAndPlayDevices**を指定して、 *FullInfPath* 64 ビット バージョンのすべてのファイルの場所を識別するパラメーター。

 

 





