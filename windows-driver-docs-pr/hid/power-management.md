---
title: HID USB 経由での電源管理
description: USB 経由で非表示に USB は、電源中断の採用はデバイスを管理します。
ms.assetid: 7B5E10B0-2EEA-450A-9E21-B60215F60027
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8abfbee9b5a0d8c17b89137c99e212a2781cbfff
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581040"
---
# <a name="power-management"></a>電源管理


USB 経由で非表示に USB は、電源中断の採用はデバイスを管理します。

次の 2 つの構成では主に電源を管理できます。

1.  ケース\#1。システムが電源管理の状態 (S3 など) が、デバイスは、システムをウェイク アップを入手できます。 例: HID USB キーボードを S3 からキーの押下でのデスクトップをスリープ解除されているのです。
2.  ケース\#2。システムが実行中の状態 (例: S0) が、デバイスがアイドル状態 (ユーザーの操作なし)。 例: 選択的だれが使用または接してときに、HID USB マウスを中断します。

*ケース\#1 のプロビジョニング*

HID デバイスはない低電力状態からシステムを自動的にスリープ解除します。 のみ特定 HID デバイス (キーボードとマウスのレベル コレクションを上位など) は、これを行います。

エンドユーザーをウェイク アップするシステムからのデバイスを解除する場合、ユーザーを指定できますこのデバイス マネージャーのプロパティ/電源管理 タブで。

 

 




