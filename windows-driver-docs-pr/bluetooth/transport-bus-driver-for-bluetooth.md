---
title: Bluetooth 用トランスポート バス ドライバー
description: システムのサンプルの次の図は、そのトランスポートとして UART を使用して、多機能のコント ローラーをサポートするために使用されるドライバー スタックを示しています。
ms.assetid: C47FA9B7-9627-452F-8FDC-4B97FFF79E9D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5985f7d0494d23d3d3c4df51a85d3985550342a6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328191"
---
# <a name="transport-bus-driver-for-bluetooth"></a>Bluetooth 用トランスポート バス ドライバー


システムのサンプルの次の図は、そのトランスポートとして UART を使用して、多機能のコント ローラーをサポートするために使用されるドライバー スタックを示しています。

![bluetooth トランスポート バス ドライバーのサンプル](images/bthsampletransportbusdriver.png)

Bluetooth 機能をサポートするために、デバイス スタックは、2 つのレイヤーで構成されます。

1.  **シリアル バス ドライバー層**多機能周辺機器をサポートするために使用される (または Bluetooth や FM をサポートするためにダイアグラムでチップのいわゆる「コンボ」)。
2.  **Bluetooth Core ドライバー層**子 Bluetooth 機能をサポートするためには、シリアル バス ドライバーによって作成された PDO に基づいて読み込まれます。

電源管理のこれら 2 つのレイヤーの役割は、次のトピックについて説明します。

-   [Bluetooth Core ドライバー レイヤーとサポートされている電源遷移](bluetooth-core-driver-layer-and-supported-power-transitions.md)
-   [シリアル バス ドライバーの層](serial-bus-driver-layer.md)

 

 





