---
title: NetAdapterCx データ パスの概要
description: NetAdapterCx データ パスの概要
ms.assetid: D2AC8269-F2D5-4FDC-A59E-6A35DBB18FF0
keywords:
- ネットワークデータを転送する NetAdapterCx、NetCx がネットワークデータを転送する
ms.date: 07/01/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: a1468c06e8f3fb4436f905b7813de9abb024965f
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75208960"
---
# <a name="introduction-to-the-netadaptercx-data-path"></a>NetAdapterCx データ パスの概要

NetAdapterCx でデータパスモデルを紹介するビデオを見るには、「Channel 9 の[ネットワークアダプタークラス拡張: データパス](https://aka.ms/netadapter/video3)ビデオ」を参照してください。

NetAdapterCx モデルでは、ネットワークデータはパケット記述子によって表され、パケットキューを介して転送されます。 OS とクライアントドライバーは、各パケットキューに関連付けられているリングバッファーのセットを使用して、パケット記述子を相互に転送します。

次のトピックでは、NetAdapterCx クライアントドライバーでネットワークデータを転送する方法の詳細について説明します。

- [Packet descriptors and extensions (パケットの記述子と拡張機能)](packet-descriptors-and-extensions.md)
- [キューの送信と受信](transmit-and-receive-queues.md)
- [ネットリングの概要](introduction-to-net-rings.md)
- [Network data buffer management (ネットワーク データ バッファーの管理)](network-data-buffer-management.md)
