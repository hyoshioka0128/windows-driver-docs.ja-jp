---
title: VMQ ドライバーの書き込みはじめに
description: このセクションでは、NDIS virtual machine queue (VMQ) ドライバーの記述について説明します。 このセクションを読む前に、仮想マシンキューアーキテクチャについて理解しておく必要があります。
ms.assetid: 877d3d95-2ec5-4d2e-9bcc-cd2adfc2a667
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1a9194ec15d9559d96bdef69b20d750bdb927a5
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565704"
---
# <a name="getting-started-writing-vmq-drivers"></a>VMQ ドライバーの書き込みはじめに


このセクションでは、NDIS virtual machine queue (VMQ) ドライバーの記述について説明します。 このセクションを読む前に、[仮想マシンキューアーキテクチャ](virtual-machine-queue-architecture.md)について理解しておく必要があります。

注   [NDIS 仮想ミニポートドライバーのサンプル](https://go.microsoft.com/fwlink/p/?LinkId=617918)(特に、vmq と vmq のソースファイル) を確認してください。

VMQ をサポートするミニポートドライバーは、VMQ ハードウェアサポートを提供する Nic を管理します。 このような NIC は、受信ネットワークデータをフィルター処理して VM 受信キューに割り当てるためのハードウェアサービスを提供します。

このセクションでは、前のドライバーが基になるネットワークアダプターに関する情報を取得し、VMQ の構成を設定する方法について説明します。 それまでのドライバーやユーザーアプリケーションは、現在の構成を取得し、VMQ 機能を有効または無効にすることができます。

ここでは、次のトピックについて説明します。

-   [VMQ ドライバーの構成](vmq-driver-configuration.md)
-   [キューの状態と操作](queue-states-and-operations.md)
-   [VMQ の割り込み要件](vmq-interrupt-requirements.md)
-   [VM キューの割り当てと解放](allocating-and-freeing-vm-queues.md)
-   [VMQ フィルターの設定とクリア](setting-and-clearing-vmq-filters.md)
-   [VM キューパラメーターの取得と更新](obtaining-and-updating-vm-queue-parameters.md)
-   [VMQ の送信と受信の操作](vmq-send-and-receive-operations.md)
-   [VMQ 情報の取得](obtaining-vmq-information.md)

 

 





