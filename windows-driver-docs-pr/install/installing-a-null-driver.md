---
title: Null ドライバーのインストール
description: Null ドライバーのインストール
ms.assetid: 8684eade-3f25-48fe-94e7-a7e76d8072ad
keywords:
- デバイス セットアップ WDK デバイスのインストール、null のドライバー
- デバイスのインストール WDK、null のドライバー
- デバイス WDK、null のドライバーをインストールします。
- null ドライバー WDK デバイスのインストール
- 存在しないドライバー WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5e4be192c2a4809e36ec37cdbda048c8bed6237
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362942"
---
# <a name="installing-a-null-driver"></a>Null ドライバーのインストール





"Null"ドライバーをインストールする場合があります (つまり、存在しないドライバー)、デバイスの場合は、デバイスは、マシンで使用されていないと、開始できません。 このようなデバイスは通常、コンピューター上に存在しませんが、null のドライバーをインストールする場合は、ことができます。 さらに、システムは、null 関数のドライバーがないデバイス ドライバーをインストールします。

INF ファイルで、null のドライバーを指定するには、次のようなエントリを使用します。

```cpp
:
[MyModels]
%MyDeviceDescription% = MyNullInstallSection, &BadDeviceHardwareID%
:

[MyNullInstallSection]
; The install section is typically empty, but can contain entries that
; copy files or modify the registry.

[MyNullInstallSection.Services]
AddService = ,2    ; no value for the service name
:
```

デバイスのハードウェア ID、*モデル*セクションがデバイスを識別、具体的には、サブシステムのベンダー ID とその他のすべての情報が関連するを使用しています。

オペレーティング システムは、[デバイス] ノードを作成 (*devnode*) デバイスが raw モードで実行できる場合は、デバイスのオペレーティング システムは開始されません、デバイスに関数のドライバーが割り当てられていないためです。 なお、ただし、そのデバイスにある場合、[ブート構成](https://docs.microsoft.com/windows-hardware/drivers/kernel/hardware-resources#logical-configuration-types-for-resource-lists)、それらのリソースは予約されています。

 

 





