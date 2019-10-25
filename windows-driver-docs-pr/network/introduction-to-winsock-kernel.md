---
title: Winsock カーネルの概要
description: Winsock カーネルの概要
ms.assetid: 52c65b9f-e3b3-4b0d-8334-7db1abb2c971
keywords:
- Winsock カーネル WDK ネットワーク, Winsock カーネルについて
- WSK WDK ネットワーク、Winsock カーネルについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66885083bb4b17f954984f8f87870ba6221400af
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844160"
---
# <a name="introduction-to-winsock-kernel"></a>Winsock カーネルの概要


Winsock カーネル (WSK) は、カーネルモードの[ネットワークプログラミングインターフェイス (NPI)](network-programming-interface.md)です。 WSK では、カーネルモードのソフトウェアモジュールは、ユーザーモード Winsock2 でサポートされているのと同じソケットプログラミング概念を使用して、ネットワーク i/o 操作を実行できます。 WSK NPI は、ソケットの作成、バインド、接続の確立、データ転送 (送受信) などの使い慣れたソケット操作をサポートしています。 ただし、WSK NPI は、ユーザーモード Winsock2 と同じソケットプログラミング概念のほとんどをサポートしていますが、Irp やイベントコールバックを使用してパフォーマンスを向上させる非同期 i/o などの一意の特性を備えた、まったく新しい、異なるインターフェイスです。

Windows Vista 以降のバージョンの Microsoft Windows を対象とするカーネルモードのネットワークモジュールでは、 [TDI](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565094(v=vs.85))ではなく wsk を使用する必要があります。 wsk では、パフォーマンスが向上し、プログラミングが簡単になるためです。 フィルタードライバーは Windows Vista で[Windows フィルタリングプラットフォーム](introduction-to-windows-filtering-platform-callout-drivers.md)を実装する必要があり、TDI クライアントは wsk を実装する必要があります。

Windows Vista 以降では、Microsoft Windows のバージョンでは TDI はサポートされませ**ん  。** 代わりに、 [Windows フィルタリングプラットフォーム](windows-filtering-platform-callout-drivers2.md)または[Winsock カーネル](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)を使用してください。

 

 

 





