---
title: VMQ ドライバーの作成
description: このセクションでは、NDIS 仮想マシン キュー (VMQ) ドライバーの開発についての情報を提供します。 既に、このセクションを読む前に、仮想マシン キュー アーキテクチャを理解する必要があります。
ms.assetid: 877d3d95-2ec5-4d2e-9bcc-cd2adfc2a667
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e5dae3e783613f339f2f1ac3f97b6bbb2dd2941
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580230"
---
# <a name="writing-vmq-drivers"></a>VMQ ドライバーの作成


このセクションでは、NDIS 仮想マシン キュー (VMQ) ドライバーの開発についての情報を提供します。 既に理解する必要があります、[仮想マシン キュー アーキテクチャ](virtual-machine-queue-architecture.md)このセクションを読む前にします。

**注**  学習してください、 [NDIS 仮想ミニポート ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=617918)、特に vmq.c と vmq.h ソース ファイル。

 




VMQ をサポートしているミニポート ドライバーでは、VMQ ハードウェアのサポートを提供するための Nic を管理します。 このような NIC では、受信ネットワーク データをフィルター処理を VM に割り当てるハードウェア サービスの受信キューで提供します。

このセクションでは、ドライバーが重なって、基になるネットワーク アダプターに関する情報を取得し、設定方法 VMQ 構成について説明します。 ドライバーとアプリケーションのユーザーに関連、現在の構成を取得し、有効または無効に VMQ 機能。

ここでは、次のトピックについて説明します。

-   [VMQ ドライバーの構成](vmq-driver-configuration.md)
-   [キューの状態と操作](queue-states-and-operations.md)
-   [VMQ 割り込みの要件](vmq-interrupt-requirements.md)
-   [割り当てと解放 VM キュー](allocating-and-freeing-vm-queues.md)
-   [設定および VMQ のフィルターをクリア](setting-and-clearing-vmq-filters.md)
-   [取得して、VM キュー パラメーターの更新](obtaining-and-updating-vm-queue-parameters.md)
-   [VMQ 送受信操作](vmq-send-and-receive-operations.md)
-   [VMQ の情報を取得します。](obtaining-vmq-information.md)

 

 





