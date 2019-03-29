---
title: Hyper-V 拡張可能スイッチの保存および復元操作
description: Hyper-V 拡張可能スイッチの保存および復元操作
ms.assetid: 7F3A77E0-F1E9-49E4-8C78-62B8F412353D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7743172210dd2e67569ed6b2a6c0c3495b3a5f61
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571520"
---
# <a name="hyper-v-extensible-switch-save-and-restore-operations"></a>Hyper-V 拡張可能スイッチの保存および復元操作


HYPER-V 子パーティションは、停止、保存されている、またはライブ移行、パーティションの実行時の状態が保存されます。 パーティションは、再起動または別のホスト コンピューターへのライブ マイグレーションが完了した、実行時の状態が復元されます。 保存と復元の状態は、移行中に、子パーティションのネットワーク インターフェイスの設定は変更されず、HYPER-V 拡張可能スイッチにネットワーク接続が破棄されません。

拡張可能スイッチのインターフェイスは、保存の基になる拡張と子パーティションの復元操作を通知します。 保存中に操作を拡張機能はそれぞれ拡張可能スイッチのネットワーク アダプター (NIC) の実行時のデータを返すことができます。 復元操作中に、インターフェイスを返します、実行時データ拡張機能に NIC の状態を復元できるように

ここでは、次のトピックについて説明します。

[保存操作の HYPER-V 拡張可能スイッチ](hyper-v-extensible-switch-save-operations.md)

[復元操作の HYPER-V 拡張可能スイッチ](hyper-v-extensible-switch-restore-operations.md)

[HYPER-V 拡張可能スイッチのライブ マイグレーションのサポート](hyper-v-extensible-switch-live-migration-support.md)

 

 





