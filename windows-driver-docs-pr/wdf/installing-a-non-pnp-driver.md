---
title: 非 PnP ドライバーのインストール
description: 非 PnP ドライバーのインストール
ms.assetid: 99676d85-feb2-482c-a91b-cfc48be5904c
keywords:
- カーネルモードドライバーフレームワーク WDK、ドライバーのインストール
- フレームワークベースのドライバー WDK KMDF, インストール
- INF ファイル WDK KMDF、PnP 以外のドライバー
- 非 PnP ドライバー WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2492440c873c6153ec527a635df8270d3b818442
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844776"
---
# <a name="installing-a-non-pnp-driver"></a>非 PnP ドライバーのインストール


ドライバーがプラグアンドプレイ (PnP) デバイスをサポートしていない場合は、ドライバーパッケージに INF <em>Ddinstall</em>を含む inf ファイルが含まれている必要があり**ます。CoInstallers** section および INF <em>ddinstall</em> **。** 「 [Kmdf 共同インストーラーの使用](installing-the-framework-s-co-installer.md)」で説明されている WDF セクション。

さらに、ドライバーとフレームワークの共同インストーラーを読み込むインストーラーを用意する必要があります。 共同インストーラーは、ドライバーのインストーラーが呼び出す必要がある[**WdfPreDeviceInstall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinstaller/nf-wdfinstaller-wdfpredeviceinstall)、 [**wdfpredeviceinstallex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinstaller/nf-wdfinstaller-wdfpredeviceinstallex)、 [**WdfPostDeviceInstall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinstaller/nf-wdfinstaller-wdfpostdeviceinstall)、 [**WdfPreDeviceRemove**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinstaller/nf-wdfinstaller-wdfpredeviceremove)、 [**WdfPostDeviceRemove**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinstaller/nf-wdfinstaller-wdfpostdeviceremove)の各関数を提供します。

PnP 以外のドライバーのインストーラーを作成する方法の例については、「 [Nonpnp](sample-kmdf-drivers.md) 」のサンプルに含まれているインストーラーを参照してください。

 

 





