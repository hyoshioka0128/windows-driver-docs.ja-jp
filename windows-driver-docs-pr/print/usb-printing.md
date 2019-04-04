---
title: Microsoft USB プリンター ドライバー (Usbprint.sys)
description: Usbprint.sys では、USB プリンター用の Microsoft 提供のデバイス ドライバーです。 Usbprint.sys は、USB プリンターや高度なプリンター ドライバーの間のエンド ツー エンド接続を提供する Usbmon.dll も連動します。
ms.assetid: 6fc1635d-b819-43ba-a549-2488995fa9b0
keywords:
- プリンター ドライバー WDK、USB
- WDK の USB プリンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e2e31e498f40d842d0d1fe343955babe1bc2485
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570071"
---
# <a name="microsoft-usb-printer-driver-usbprintsys"></a>Microsoft USB プリンター ドライバー (Usbprint.sys)


Usbprint.sys では、USB プリンター用の Microsoft 提供のデバイス ドライバーです。 Usbprint.sys は、USB プリンターや高度なプリンター ドライバーの間のエンド ツー エンド接続を提供する Usbmon.dll も連動します。




一部の USB デバイス クラス ドライバーとは異なり Usbprint.sys はしない「ドライブ」プリンターです。 代わりに、Usbprint.sys プリンターをより高度なドライバーから制御できる通信コンジットを提供します。 パラレル プリンターの場合と USB プリンター、印刷ジョブを表示するために、プリンター ドライバーが必要です、プリンターに高度な通信を管理する、言語モニターも必要になります。

USB プリンターのインストール時に、システムが指定した INF のファイル、Usbprint.inf は、ローカル ファイル Driver.cab から Usbprint.sys を取得します。 Driver.cab は、オペレーティング システムにインストールされている、ためプリンター インストーラー通常必要はありません、元のインストール メディア Usbprint.sys をインストールします。 Usbprint.inf の詳細については、[の USB ポートにプリンターが接続されている](printer-connected-to-a-usb-port.md)を参照してください。 Driver.cab の詳細については、[プリンターのインストールと、プラグ アンド プレイ マネージャ](printer-installation-and-the-plug-and-play-manager.md)を参照してください。

このセクションには、次のトピックが含まれています。

[USBPRINT のプログラミングに関する考慮事項](programming-considerations-for-usbprint.md)

 

 




