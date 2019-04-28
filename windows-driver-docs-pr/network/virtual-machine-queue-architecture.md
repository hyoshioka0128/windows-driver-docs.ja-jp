---
title: 仮想マシン キュー アーキテクチャ
description: 仮想マシン キュー アーキテクチャ
ms.assetid: 7aa8c9a4-1bb2-48a5-be28-9806e16d4e94
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2cf2813ad11f895e1c5d8a7bdcbf08ab6bd7bbba
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378226"
---
# <a name="virtual-machine-queue-architecture"></a>仮想マシン キュー アーキテクチャ





NDIS 仮想マシン キュー (VMQ) のアーキテクチャは、次の仮想化に関する利点を提供します。

-   仮想化のパフォーマンスに影響し、VMQ がそれらの効果を克服を支援します。

-   VMQ は、ライブ マイグレーションをサポートします。

-   VMQ は、NDIS タスク オフロード、およびその他の最適化と共存します。

このセクションは、NDIS VMQ インターフェイスに関する詳細な情報を提供します。 このセクションは、VMQ をサポートする NDIS ドライバーを記述する前に読む必要があります。 VMQ ドライバーの記述については、次を参照してください。 [VMQ ドライバーの記述](writing-vmq-drivers.md)します。

ここでは、次のトピックについて説明します。

[NDIS 仮想マシン キュー (VMQ) の概要](introduction-to-ndis-virtual-machine-queue--vmq-.md)

[共有メモリの NDIS 仮想マシン (VM) セキュリティ上の問題](security-issues-with-ndis-virtual-machine--vm--shared-memory.md)

[NDIS VMQ のライブ マイグレーションのサポート](ndis-vmq-live-migration-support.md)

[NDIS VM キューの状態](ndis-virtual-machine-queue-states.md)

 

 





