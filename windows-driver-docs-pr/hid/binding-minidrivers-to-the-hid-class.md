---
title: ミニドライバーを HID クラスにバインドする
description: このセクションでは、システムによって提供される HID クラスドライバーと HID ミニドライバーの動作について説明します。このクラスは、HIDClass device setup クラスのデバイスをサポートしています。
ms.assetid: 2B51E205-8EBB-413A-A317-0923FAB77F0E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fba5ec985bd82b3cac465db9033c3fdf19c29322
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824852"
---
# <a name="binding-minidrivers-to-the-hid-class"></a>ミニドライバーを HID クラスにバインドする


このセクションでは、システムによって提供される HID クラスドライバーと HID ミニドライバーの動作について説明します。このクラスは、HIDClass [device setup クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)のデバイスをサポートしています。

HID クラスドライバーは、入力デバイスでサポートされている HID コレクションにアクセスするために、上位レベルのドライバーとユーザーモードアプリケーションが使用するインターフェイスを提供します。 HID クラスドライバーは、HID ミニドライバーを使用して入力デバイスのハードウェアにアクセスします。 HID ミニドライバー入力デバイスが接続されているバスのポートの操作を要約します。 HID クラスドライバーは、HID ミニドライバーにリンクされているエクスポートドライバーです。 Hid ミニドライバーは、 [**HidRegisterMinidriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidport/nf-hidport-hidregisterminidriver)を呼び出して hid クラスドライバーに自身を登録することで、その操作を hid クラスドライバーにバインドします。

HID クラスドライバーと HID ミニドライバーの組み合わせ操作は、入力デバイス用の WDM 関数ドライバーとして機能し、入力デバイスがサポートする子デバイス (HID コレクション) 用のバスドライバーとして機能します。 この設計により、HID クラスドライバーは、usb バス以外のポートまたはバスに接続されている USB HID デバイスと非 USB 入力デバイスを操作できるようになります。 基になる親デバイスの操作上の詳細は、上位レベルのドライバーまたはユーザーモードアプリケーションに対して透過的です。

 

 




