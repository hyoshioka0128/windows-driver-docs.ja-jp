---
title: 64 ビット システムでデバイスのインストール
description: 64 ビット システムでデバイスのインストール
ms.assetid: 76d9bff7-6429-4d20-9790-a41ed2cb1bdd
keywords:
- 64 ビットの WDK デバイスのインストール
- デバイスのインストール WDK、64 ビット システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b156df529315318ebe412bf6ae728c8dfe416ff9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535579"
---
# <a name="device-installations-on-64-bit-systems"></a>64 ビット システムでデバイスのインストール





作成するときに、次の手順にする必要があります、デバイスは 32 ビット プラットフォームと 64 ビット プラットフォームの両方でインストールする場合、[ドライバー パッケージ](driver-packages.md):

-   すべてのカーネル モード ドライバーの 32 ビットと 64 ビットの両方のコンパイルを提供*デバイス インストール アプリケーション*、*クラス インストーラー*と*共同インストーラー*します。 詳細については、[Your のドライバーを 64 ビット Windows に移植](https://msdn.microsoft.com/library/windows/hardware/ff559747)を参照してください。

-   使用する 1 つまたは複数のクロス プラットフォーム INF ファイルを提供*INF セクションを装飾*プラットフォームに固有のインストールの動作を制御します。

場合[デバイス インストール アプリケーションを記述して](writing-a-device-installation-application.md)、32 ビット バージョンは、既定のバージョンである必要があります。 32 ビット バージョンはユーザーが、配布のディスクを挿入するときに自動的に開始できるように、(Microsoft Windows SDK のドキュメントで説明) を自動実行、して呼び出す必要があります。

アプリケーションの 32 ビット バージョンがによって返される値を確認する必要があります[ **UpdateDriverForPlugAndPlayDevices**](https://msdn.microsoft.com/library/windows/hardware/ff553534)します。 ERROR_IN_WOW64 を戻り値には、32 ビット アプリケーションは、64 ビット プラットフォームで実行されていると、受信トレイのドライバーを更新することはできません。 代わりに、呼び出す必要があります[ **CreateProcess** ](https://msdn.microsoft.com/library/windows/desktop/ms682425) (Windows SDK のドキュメントで説明)、アプリケーションの 64 ビット バージョンを開始します。 64 ビット バージョンを呼び出して**UpdateDriverForPlugAndPlayDevices**を指定して、 *FullInfPath* 64 ビット バージョンのすべてのファイルの場所を識別するパラメーター。

 

 





