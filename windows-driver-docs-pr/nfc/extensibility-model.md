---
title: NFC クラスの拡張機能の拡張モデル
description: NFC クラスの拡張機能ドライバーでは、NCI 仕様が対応していないチップセット固有 NCI の専用拡張を追加することができます。
ms.assetid: 8CCCE7BF-595A-4F30-9924-B5BD45D6137F
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f3b2a5c47ed8be8f9066446ec7ff5acf231bbf2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370513"
---
# <a name="nfc-class-extension-extensibility-model"></a>NFC クラスの拡張機能の拡張モデル


NFC クラスの拡張機能ドライバーの主な目的は、NCI 仕様が対応していないチップセット固有 NCI の専用拡張を追加する柔軟性を備えたクライアント ドライバーを提供します。

これに合わせて、NFC クラスの拡張機能ドライバーがこれら NCI のベンダー拡張機能のサポートを提供するクライアント ドライバーを含む、NCI で定義されている RF プロトコルの独自の実装に限らずの複数の機能拡張ポイントを提供します省電力モードおよびファームウェアのパラメーターの他のチップセット固有の構成の NFC コント ローラーを構成するチップセット固有 NCI コマンド。

NFC クラスの拡張機能ドライバーでは、NFC のクライアント ドライバーの 3 つの機能拡張ポイントを提供します。

-   [シーケンス処理](sequence-handling.md)
-   RF プロトコルとインターフェイスの機能拡張
-   NCI のパケットの処理

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[NFC クラスの拡張機能 (CX) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
