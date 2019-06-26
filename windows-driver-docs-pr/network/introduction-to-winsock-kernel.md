---
title: Winsock カーネルの概要
description: Winsock カーネルの概要
ms.assetid: 52c65b9f-e3b3-4b0d-8334-7db1abb2c971
keywords:
- ネットワークには、Winsock カーネルに関する Winsock カーネル WDK
- ネットワークには、Winsock カーネルに関する WSK WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d516cde9492582778576a1ce51dee676ee814e31
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386337"
---
# <a name="introduction-to-winsock-kernel"></a>Winsock カーネルの概要


Winsock カーネル (WSK) は、カーネル モード[ネットワーク プログラミング インターフェイス (NPI)](network-programming-interface.md)します。 WSK、カーネル モード ソフトウェア モジュールはプログラミングの概念 Winsock2 のユーザー モードでサポートされている同じソケットを使用して、ネットワーク I/O 操作を実行できます。 WSK NPI ソケットの作成、バインド、接続の確立、およびデータ転送などの使い慣れたソケット操作をサポートしています (送信し、受信)。 ただし、WSK NPI には、ほとんどのプログラミングの概念をユーザー モード Winsock2 として同じソケットがサポートされますは、非同期の I/O パフォーマンスを強化するために Irp とイベントのコールバックを使用するなどの一意の特性を持つ、まったく新しいさまざまなインターフェイスです。

カーネル モードのネットワーク モジュールの代わりに WSK を使用する必要があり、Windows Vista 以降のバージョンの Microsoft Windows の対象となる[TDI](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565094(v=vs.85)) WSK、パフォーマンスの向上とプログラミングを簡単にするためです。 フィルター ドライバーを実装する必要があります、 [Windows フィルタ リング プラットフォーム](introduction-to-windows-filtering-platform-callout-drivers.md)クライアントで Windows Vista、および TDI WSK を実装する必要があります。

**注**  Windows Vista の後に、TDI が Microsoft Windows のバージョンでサポートされません。 使用[Windows フィルタ リング プラットフォーム](windows-filtering-platform-callout-drivers2.md)または[Winsock Kernel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)代わりにします。

 

 

 





