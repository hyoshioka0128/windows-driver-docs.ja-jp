---
title: IDE コントローラー ミニドライバーのインストール
description: IDE コントローラー ミニドライバーのインストール
ms.assetid: c1b41f89-150d-47e9-9bed-04f5796f69bd
keywords:
- IDE コント ローラー ミニドライバー WDK のストレージをインストールします。
- 記憶域の IDE コント ローラー ミニドライバー、WDK をインストールします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 984e040b1b7d48ba59f136f727624a671bdaa235
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571188"
---
# <a name="installing-ide-controller-minidrivers"></a>IDE コントローラー ミニドライバーのインストール


## <span id="ddk_installing_ide_controller_minidrivers_kg"></span><span id="DDK_INSTALLING_IDE_CONTROLLER_MINIDRIVERS_KG"></span>


このセクションでは、IDE コント ローラーのドライバーと Microsoft Windows 2000 以降のオペレーティング システムでのコント ローラー ミニドライバーに固有のインストール情報を提供します。

独自のコント ローラー ミニドライバーを提供しているベンダー ドライバーを行う必要がありますでハード ディスク コント ローラー (HDC) セットアップ クラスのメンバー、 [ **INF バージョン セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547502)ドライバーの INF ファイル。 以下に例を示します。

```cpp
[version]
Signature="$WINDOWS NT$"
Class=hdc
ClassGuid={4D36E96A-E325-11CE-BFC1-08002BE10318}
```

IDE コント ローラーのミニドライバーをインストールに関連付けられているその他の特別な要件はありません。

インストールの詳細については、Windows 2000 以降のオペレーティング システムでサポートされているコント ローラーのハードウェアの一覧を含むハード ディスク コント ローラーのシステム提供の INF ファイルを参照*ある*します。

Windows 2000 以降のオペレーティング システムでデバイスのインストールの詳細については、次を参照してください。 [Vendor-Supplied IDE コント ローラーのミニドライバーの要件](requirements-for-vendor-supplied-ide-controller-minidrivers.md)と[デバイス インストールの概要](https://msdn.microsoft.com/library/windows/hardware/ff549455)します。

 

 




