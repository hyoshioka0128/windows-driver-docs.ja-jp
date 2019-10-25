---
title: パラレル ポートとデバイスの IOCTL とコールバックのサポート
description: パラレル ポートとデバイスの IOCTL とコールバックのサポート
ms.assetid: 72a31f50-2f59-4a4d-aac7-571f83a94259
keywords:
- システム提供のパラレルドライバー WDK、Ioctl
- Ioctl WDK パラレルドライバー
- コールバック WDK パラレルドライバー
- システム提供のパラレルドライバー WDK、コールバック
- 並列デバイス WDK、コールバック
- パラレルデバイス WDK、Ioctl
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e7736f4dcec9d6675d6423a57080d539ffc7ffd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845318"
---
# <a name="ioctl-and-callback-support-for-parallel-ports-and-devices"></a>パラレル ポートとデバイスの IOCTL とコールバックのサポート





このセクションでは、システム提供の並列ドライバーがパラレルポートに接続されている操作パラレルポートとデバイスをサポートする方法について説明するトピックへのリンクを示します。

パラレルポートに接続されているパラレルデバイスのベンダー関数ドライバーはオプションです。 システムによって提供されるパラレルドライバーは、並列デバイスを生のデバイスとして直接制御したり、デバイスの親パラレルポートを操作したりするための広範なサポートを提供します。

システム提供の関数ドライバーがパラレルポートを操作するために提供する Ioctl およびコールバックの詳細については、次のトピックを参照してください。

[パラレルポートに関する情報の取得](obtaining-information-about-a-parallel-port.md)

[パラレルポートの使用の同期](synchronizing-the-use-of-a-parallel-port.md)

[パラレルポートに接続されている IEEE 1284 デバイスの選択と選択解除](selecting-and-deselecting-an-ieee-1284-device-attached-to-a-parallel-p.md)

[パラレルポートでの通信モードの設定とクリア](setting-and-clearing-the-communication-mode-on-a-parallel-port.md)

[IEEE 1284.3 データリンクデバイスへの接続](connecting-to-an-ieee-1284-3-data-link-device.md)

システム提供のバスドライバーがパラレルポートに接続されている並列デバイスを操作するために提供する Ioctl およびコールバックの詳細については、以下を参照してください。

[並列デバイスを開いて使用する](opening-and-using-a-parallel-device.md)

[パラレルデバイスへの接続](connecting-to-a-parallel-device.md)

[パラレルデバイスに関する情報の取得](obtaining-information-about-a-parallel-device.md)

[並列デバイスで使用するためのパラレルポートのロックとロック解除](locking-and-unlocking-a-parallel-port-for-use-by-a-parallel-device.md)

[パラレルデバイスの通信モードの設定とクリア](setting-and-clearing-a-communication-mode-for-a-parallel-device.md)

[パラレルデバイスでの属性の設定](setting-attributes-on-a-parallel-device.md)

[並列デバイスの読み取りと書き込み](reading-and-writing-a-parallel-device.md)

パラレルポートおよびパラレルポートに接続されているデバイスを操作する方法の詳細については、以下を参照してください。

[パラレルポートの操作](operating-a-parallel-port.md)

[パラレルポートに接続されているパラレルデバイスの操作](operating-a-parallel-device-attached-to-a-parallel-port.md)

[システム提供のパラレルドライバーへのクライアントインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

 

 




