---
title: HID over USB の概要
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
ms.openlocfilehash: 693dc815278f8b692a9529aa37a460163b029db1
ms.sourcegitcommit: f1f641bd759b7bf6e45626ffcc090ffd28337c30
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/28/2020
ms.locfileid: "78166664"
---
# <a name="hid-over-usb-overview"></a>HID over USB の概要

USB は、Windows で最初にサポートされている HID トランスポートです。 対応するインボックスドライバーは Windows 2000 で導入され、以降のすべてのオペレーティングシステムで使用できるようになりました。 このドライバーは、タッチパッド向けからの HID デバイスの新しいクラスとセンサーおよびベンダー固有のデバイスの種類を含むように強化されています。 HID は、選択的中断を活用するように最適化されています。 (この機能を使用するには、ベンダーから提供されている INF または Microsoft オペレーティングシステム記述子によるサポートが必要です)。

USB を使用した HID の最近の更新には、次のものも含まれます。

- USB 1.1、USB 2.0、および USB 3.0 のサポート。
- HID over USB ドライバーは、Windows のすべてのクライアント Sku で使用でき、WinPE に含まれています。

## <a name="see-also"></a>参照

- [HID USB ホームページ](https://www.usb.org/hid)
- [HID USB 仕様](https://www.usb.org/sites/default/files/documents/hid1_11.pdf)
- [HID 使用状況テーブル](https://www.usb.org/sites/default/files/documents/hut1_12v2.pdf)
