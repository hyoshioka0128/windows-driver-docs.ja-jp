---
title: Null のドライバーをインストールします。
description: Null のドライバーをインストールします。
ms.assetid: 8684eade-3f25-48fe-94e7-a7e76d8072ad
keywords:
- デバイス セットアップ WDK デバイスのインストール、null のドライバー
- デバイスのインストール WDK、null のドライバー
- デバイス WDK、null のドライバーをインストールします。
- null ドライバー WDK デバイスのインストール
- 存在しないドライバー WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f371e29e64de92310352164b9c1e7a8f2f6d461
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530774"
---
# <a name="installing-a-null-driver"></a>Null のドライバーをインストールします。





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

オペレーティング システムは、[デバイス] ノードを作成 (*devnode*) デバイスが raw モードで実行できる場合は、デバイスのオペレーティング システムは開始されません、デバイスに関数のドライバーが割り当てられていないためです。 なお、ただし、そのデバイスにある場合、[ブート構成](https://msdn.microsoft.com/library/windows/hardware/ff547012#logical-configuration-types-for-resource-lists)、それらのリソースは予約されています。

 

 





