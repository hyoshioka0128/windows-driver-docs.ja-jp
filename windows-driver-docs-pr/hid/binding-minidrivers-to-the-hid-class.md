---
title: ミニドライバーを HID クラスにバインドする
description: このセクションでは、システムによって提供される HID クラス ドライバーと HIDClass デバイス セットアップ クラスのデバイスをサポートする HID ミニドライバーの操作について説明します。
ms.assetid: 2B51E205-8EBB-413A-A317-0923FAB77F0E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa1e4b01a010529f65ee8ae518291032f4723c54
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375778"
---
# <a name="binding-minidrivers-to-the-hid-class"></a>ミニドライバーを HID クラスにバインドする


このセクションには、システムによって提供される HID クラス ドライバーと、HIDClass でデバイスをサポートする HID ミニドライバーの操作がについて説明します[デバイス セットアップ クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)します。

HID クラス ドライバーはその上位レベルのドライバーのインターフェイスを提供し、入力デバイスでサポートされている HID コレクションにアクセスするユーザー モード アプリケーションを使用します。 HID クラス ドライバーは HID ミニドライバーを使用して、入力デバイスのハードウェアにアクセスします。 HID ミニドライバーは、入力デバイスが接続されているバスのポートの操作を抽象化します。 HID クラス ドライバーは、HID ミニドライバーにリンクされているエクスポート ドライバーです。 HID ミニドライバー HID クラス ドライバーを呼び出すことにより、操作をバインドする[ **HidRegisterMinidriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidport/nf-hidport-hidregisterminidriver) HID クラス ドライバーに自身を登録します。

HID クラス ドライバーと HID ミニドライバーの結合操作は、入力デバイスの WDM 関数ドライバーは、入力デバイスでサポートされる子デバイス (HID コレクション) のバス ドライバーとして機能します。 この設計により HID クラス ドライバーは、USB HID デバイスとポートまたは USB バス以外のバスに接続されている入力デバイスを USB 以外の動作をします。 基になる親デバイスの運用上の詳細は、上位レベルのドライバーやユーザー モード アプリケーションに対して透過的です。

 

 




