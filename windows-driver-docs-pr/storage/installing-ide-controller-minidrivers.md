---
title: IDE コントローラー ミニドライバーのインストール
description: IDE コントローラー ミニドライバーのインストール
ms.assetid: c1b41f89-150d-47e9-9bed-04f5796f69bd
keywords:
- IDE コント ローラー ミニドライバー WDK のストレージをインストールします。
- 記憶域の IDE コント ローラー ミニドライバー、WDK をインストールします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 942e6dcddf3490f85bb6e4eb7cde63c42befbd86
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379108"
---
# <a name="installing-ide-controller-minidrivers"></a>IDE コントローラー ミニドライバーのインストール


## <span id="ddk_installing_ide_controller_minidrivers_kg"></span><span id="DDK_INSTALLING_IDE_CONTROLLER_MINIDRIVERS_KG"></span>


このセクションでは、IDE コント ローラーのドライバーと Microsoft Windows 2000 以降のオペレーティング システムでのコント ローラー ミニドライバーに固有のインストール情報を提供します。

独自のコント ローラー ミニドライバーを提供しているベンダー ドライバーを行う必要がありますでハード ディスク コント ローラー (HDC) セットアップ クラスのメンバー、 [ **INF バージョン セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)ドライバーの INF ファイル。 以下に例を示します。

```cpp
[version]
Signature="$WINDOWS NT$"
Class=hdc
ClassGuid={4D36E96A-E325-11CE-BFC1-08002BE10318}
```

IDE コント ローラーのミニドライバーをインストールに関連付けられているその他の特別な要件はありません。

インストールの詳細については、Windows 2000 以降のオペレーティング システムでサポートされているコント ローラーのハードウェアの一覧を含むハード ディスク コント ローラーのシステム提供の INF ファイルを参照*ある*します。

Windows 2000 以降のオペレーティング システムでデバイスのインストールの詳細については、次を参照してください。 [Vendor-Supplied IDE コント ローラーのミニドライバーの要件](requirements-for-vendor-supplied-ide-controller-minidrivers.md)と[デバイス インストールの概要](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-device-and-driver-installation)します。

 

 




