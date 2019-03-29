---
title: ネットワーク データの転送
description: ネットワーク データの転送
ms.assetid: D2AC8269-F2D5-4FDC-A59E-6A35DBB18FF0
keywords:
- NetAdapterCx NetCx ネットワーク データを転送する、ネットワーク データを転送します。
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: 544b00d8e0e12184748bc3cb60617aad0a08a798
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582498"
---
# <a name="transferring-network-data"></a>ネットワーク データの転送

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

NetAdapterCx のデータ パスのモデルを紹介するビデオを見るを参照してください、[ネットワーク アダプター クラスの拡張機能。データ パス](https://aka.ms/netadapter/video3)Channel 9 のビデオ。

NetAdapterCx モデルでは、ネットワーク データがパケット記述子によって表され、パケット キューを介して転送します。 OS と、クライアント ドライバーは、パケットの記述子を一連の各パケットのキューに関連付けられているリング バッファーを使用して相互に転送します。

次のトピックは、NetAdapterCx クライアント ドライバーでネットワーク データを転送する方法の詳細について説明します。

- [Packet descriptors and extensions (パケットの記述子と拡張機能)](packet-descriptors-and-extensions.md)
- [送信および受信キュー](transmit-and-receive-queues.md)
- [リング バッファーを使用してください。](using-the-ring-buffer.md)
- [Network data buffer management (ネットワーク データ バッファーの管理)](network-data-buffer-management.md)
