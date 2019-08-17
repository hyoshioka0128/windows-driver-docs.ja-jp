---
title: Hyper-v 拡張可能スイッチの保存と復元の操作の概要
description: Hyper-v 拡張可能スイッチの保存と復元の操作の概要
ms.assetid: 7F3A77E0-F1E9-49E4-8C78-62B8F412353D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dec3f95a638c7173dba3fb550e641729a3713bb7
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565667"
---
# <a name="hyper-v-extensible-switch-save-and-restore-operations-overview"></a>Hyper-v 拡張可能スイッチの保存と復元の操作の概要


Hyper-v の子パーティションが停止、保存、またはライブマイグレーションされると、パーティションの実行時の状態が保存されます。 パーティションが再起動されるか、別のホストコンピューターへのライブマイグレーションが完了すると、実行時の状態が復元されます。 保存状態と復元状態の間の切り替え中、子パーティションのネットワークインターフェイスの設定は変更されず、Hyper-v 拡張可能スイッチへのネットワーク接続は切断されません。

拡張可能スイッチインターフェイスは、子パーティションの保存および復元操作の基になる拡張機能に通知します。 保存操作中、拡張機能は、拡張可能なスイッチネットワークアダプター (NIC) ごとに実行時データを返すことができます。 復元操作中、インターフェイスは実行時データを拡張機能に返し、NIC の状態を復元できるようにします。

ここでは、次のトピックについて説明します。

[Hyper-v 拡張可能スイッチの保存操作](hyper-v-extensible-switch-save-operations.md)

[Hyper-v 拡張可能スイッチの復元操作](hyper-v-extensible-switch-restore-operations.md)

[Hyper-v 拡張可能スイッチライブマイグレーションサポート](hyper-v-extensible-switch-live-migration-support.md)

 

 





