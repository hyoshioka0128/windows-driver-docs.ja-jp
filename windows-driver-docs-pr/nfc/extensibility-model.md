---
title: NFC クラス拡張機能の拡張モデル
description: NFC クラス拡張ドライバーを使用すると、開発者は、NCI 仕様に含まれていないチップセット固有の NCI 専用拡張機能を追加できます。
ms.assetid: 8CCCE7BF-595A-4F30-9924-B5BD45D6137F
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c406505aa705ac342e59dafea05acfa5b27442c9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843417"
---
# <a name="nfc-class-extension-extensibility-model"></a>NFC クラス拡張機能の拡張モデル


NFC クラス拡張ドライバーの主な目的は、NCI 仕様でカバーされていないチップセット固有の NCI 専用拡張機能を追加できる柔軟性をクライアントドライバーに提供することです。

これに対応するために、NFC クラス拡張ドライバーは、クライアントドライバーがサポートする複数の拡張ポイントを提供します。これらの NCI ベンダ拡張機能は、NCI で定義された RF プロトコル以外の実装に限定されませんが、チップセット固有の NCI コマンド。低電力モードおよびその他のチップセット固有のファームウェアパラメーターの構成用に NFC コントローラーを構成します。

NFC クラス拡張ドライバーは、NFC クライアントドライバー用に3つの拡張ポイントを提供します。

-   [シーケンス処理](sequence-handling.md)
-   RF プロトコルとインターフェイスの拡張
-   NCI のパケットの処理

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[NFC クラス拡張 (CX) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
