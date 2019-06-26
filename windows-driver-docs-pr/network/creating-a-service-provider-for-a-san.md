---
title: SAN のサービス プロバイダーの作成
description: SAN のサービス プロバイダーの作成
ms.assetid: 848b6fd5-64f8-4e62-9c54-c23bbc3d9ede
keywords:
- Windows ソケットは、WDK、サービス プロバイダーを直接します。
- SAN サービス プロバイダー、WDK を作成します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05a53136415eb5ce43effe5124789ecfae26e59c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374928"
---
# <a name="creating-a-service-provider-for-a-san"></a>SAN のサービス プロバイダーの作成





このセクションでは、SAN サービス プロバイダーの DLL と、Windows Sockets スイッチ間のインターフェイスを構成する関数の簡単な説明を提供します。 SAN サービス プロバイダーの DLL の初期化関数の 1 つのエントリ ポイントをエクスポートします[ **WSPStartupEx**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566321(v=vs.85))します。 SAN サービス プロバイダーの**WSPStartupEx**関数見なさず、他のインターフェイスの機能の大部分ディスパッチ テーブルを介して Windows Sockets スイッチにアクセスできます。 インターフェイスの関数は SAN サービス プロバイダーの呼び出しを通じて、スイッチに渡される[ **WSPIoctl** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566296(v=vs.85))関数。 インターフェイスの機能には、 [Windows Sockets SPI 関数](windows-sockets-spi-functions-required-for-sans.md)と[Windows Sockets SPI インターフェイスを SAN に固有の拡張機能](windows-sockets-spi-extensions-for-sans.md)します。

[Windows Sockets ダイレクト参照](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565857(v=vs.85))SAN サービス プロバイダーに実装されると、これらの関数の詳細についてを説明します。 Windows Sockets SPI 関数の説明については Microsoft Windows SDK を使用しないでください。 Windows SDK の説明には、SAN に固有の要件はありません。

このセクションの一覧も、[を指定するために必要な SAN サービス プロバイダーでは Windows Sockets SPI 関数](windows-sockets-spi-functions-not-required-for-sans.md)します。

 

 





