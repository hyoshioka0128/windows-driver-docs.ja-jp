---
title: NetAdapterCx データ パスの概要
description: NetAdapterCx データ パスの概要
ms.assetid: D2AC8269-F2D5-4FDC-A59E-6A35DBB18FF0
keywords:
- NetAdapterCx NetCx ネットワーク データを転送する、ネットワーク データを転送します。
ms.date: 07/01/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: b78bafb63c16758a9efdc3f109520363d0eebe32
ms.sourcegitcommit: 6f74454e7ed5e703e4e4b363b6816652950e6a51
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2019
ms.locfileid: "67608474"
---
# <a name="introduction-to-the-netadaptercx-data-path"></a>NetAdapterCx データ パスの概要

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

NetAdapterCx のデータ パスのモデルを紹介するビデオを見るを参照してください、[ネットワーク アダプター クラスの拡張機能。データ パス](https://aka.ms/netadapter/video3)Channel 9 のビデオ。

NetAdapterCx モデルでは、ネットワーク データがパケット記述子によって表され、パケット キューを介して転送します。 OS と、クライアント ドライバーは、パケットの記述子を一連の各パケットのキューに関連付けられているリング バッファーを使用して相互に転送します。

次のトピックは、NetAdapterCx クライアント ドライバーでネットワーク データを転送する方法の詳細について説明します。

- [Packet descriptors and extensions (パケットの記述子と拡張機能)](packet-descriptors-and-extensions.md)
- [送信および受信キュー](transmit-and-receive-queues.md)
- [ネット リングとネット リングの反復子](net-rings-and-net-ring-iterators.md)
- [Network data buffer management (ネットワーク データ バッファーの管理)](network-data-buffer-management.md)
