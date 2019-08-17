---
title: USB 経由の HID の概要
description: USB は、Windows オペレーティングシステムで最初にサポートされている HID トランスポートです。
ms.assetid: F892C910-BA33-4795-A803-9D3FD55782BC
keywords:
- HID ミニポートドライバー
- USB
- USB 1.1
- USB 2.0
- USB 3.0
- USB、HID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff088091329327f6063bba24c7f9c92d4827661b
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565575"
---
# <a name="hid-over-usb-overview"></a>USB 経由の HID の概要


USB は、Windows オペレーティングシステムで最初にサポートされている HID トランスポートです。 対応する受信トレイドライバーは Windows 2000 で導入され、以降のすべてのオペレーティングシステムで使用可能になりました。

Windows 8 は、USB 経由の HID を引き続きサポートしています。また、タッチパッド向けからの HID デバイスの新しいクラスと、センサーおよびベンダー固有のデバイスの種類を含むように強化されています。

HID は、選択的中断を活用するように最適化されています。 (この機能を使用するには、ベンダーから提供されている INF または Microsoft オペレーティングシステム記述子によるサポートが必要です)。

USB を使用した HID の最近の更新には、次のものも含まれます。

-   USB 1.1、USB 2.0、および USB 3.0 のサポート。
-   HID over USB ドライバーは、Windows のすべてのクライアント Sku で使用でき、WinPE に含まれています。

 

 




