---
title: ヒューマン インターフェイス デバイス (HID) ドライバーのサンプル
description: このディレクトリのドライバーサンプルは、デバイスのカスタム HID ドライバーを作成するための開始点となります。
ms.assetid: 38C52EAD-9DC6-4575-A9FF-1472FDDC2702
ms.date: 11/19/2019
ms.localizationpriority: medium
ms.openlocfilehash: a2f4a0f7d636ae025281da12b703d136439fa02f
ms.sourcegitcommit: 30fa63ad13fd5e2e883b76a44f0703e01049ffa1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74735260"
---
# <a name="human-interface-devices-hid-driver-samples"></a>ヒューマン インターフェイス デバイス (HID) ドライバーのサンプル

このディレクトリのドライバーサンプルは、デバイスのカスタム HID ドライバーを作成するための開始点となります。

| サンプル | 説明 |
| --- | --- |
| [KMDF HID フィルター](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/kmdf-filter-driver-for-a-hid-device) | HID デバイス用のフィルタードライバー。 このサンプルでは、フィルタードライバーの記述方法を説明すると共に、リモート i/o ターゲットインターフェイスを使用して、HID コレクションをカーネルモードで開き、IOCTL 要求を送信して機能レポートを設定および取得する方法に加えて、アプリケーションが WMI インターフェイスを使用してフィルタードライバーにコマンドを送信する方法を示します。 |
| [HClient アプリケーション](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/hclient-sample-application) | Hid デバイスクラス仕様に準拠した HID デバイスと通信するユーザーモードクライアントアプリケーションを作成する方法を示します。 |
| [HIDUSBFX2](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/hidusbfx2-sample-driver) | 非 HID USB デバイスから HID デバイスへのマッピングを示します。 |
| [UMDF HID ミニドライバー](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/hid-minidriver-sample-umdf-version-2) | ユーザーモードドライバーフレームワーク (UMDF) を使用して HID ミニドライバーを記述する方法を示すサンプルです。
