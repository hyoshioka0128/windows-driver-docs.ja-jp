---
title: 非 PnP ドライバーのインストール
description: 非 PnP ドライバーのインストール
ms.assetid: 99676d85-feb2-482c-a91b-cfc48be5904c
keywords:
- カーネル モード ドライバー フレームワーク WDK は、ドライバーをインストールします。
- フレームワーク ベースのドライバー WDK KMDF をインストールします。
- INF ファイル WDK KMDF、非 PnP ドライバー
- 非 PnP ドライバー WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc0bcb4b4edf61ff7a2a160d96339ce1afb6ecd3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371140"
---
# <a name="installing-a-non-pnp-driver"></a>非 PnP ドライバーのインストール


ドライバーがプラグ アンド プレイ (PnP) デバイスをサポートしていない場合、ドライバー パッケージは、INF を含む INF ファイルを含める必要があります<em>DDInstall</em>**します。CoInstallers**セクションと INF <em>DDInstall</em>**します。WDF**セクションで説明されている[KMDF 共同インストーラーを使用して](installing-the-framework-s-co-installer.md)します。

さらに、インストーラーを読み込むには、ドライバー、フレームワークの共同インストーラーを提供する必要があります。 共同インストーラーでは、 [ **WdfPreDeviceInstall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinstaller/nf-wdfinstaller-wdfpredeviceinstall)、 [ **WdfPreDeviceInstallEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinstaller/nf-wdfinstaller-wdfpredeviceinstallex)、 [ **WdfPostDeviceInstall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinstaller/nf-wdfinstaller-wdfpostdeviceinstall)、 [ **WdfPreDeviceRemove**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinstaller/nf-wdfinstaller-wdfpredeviceremove)、および[ **WdfPostDeviceRemove** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinstaller/nf-wdfinstaller-wdfpostdeviceremove)関数をドライバーのインストーラーを呼び出す必要があります。

非 PnP ドライバーのインストーラーを作成する方法の例は、インストーラーに含まれているを参照してください、[非 PNP](sample-kmdf-drivers.md)サンプル。

 

 





