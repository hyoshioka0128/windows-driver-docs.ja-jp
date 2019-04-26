---
title: Netupg.inf ファイルの作成
description: Netupg.inf ファイルの作成
ms.assetid: 8ee000e0-abd1-4a06-9f38-2a7971bc2c97
keywords:
- netupg.inf files WDK
- ネットワーク コンポーネントのアップグレード、WDK をカスタマイズします。
- WDK のネットワーク コンポーネントをアップグレードする、カスタマイズ
- アップグレード プロセスの WDK ネットワークのカスタマイズ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73b0a899d68714290fa88887ee35c2b902902e7f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357386"
---
# <a name="creating-a-netupginf-file"></a>Netupg.inf ファイルの作成





**注**  Microsoft Windows XP では、ベンダーから提供されたネットワークのアップグレードはサポートされていない (SP1 以降)、Microsoft Windows Server 2003、および以降のオペレーティング システム。

 

Netupg.inf ファイルにはと呼ばれる 1 つのセクションが含まれています**OemNetUpgradeDirs**します。 このセクションでは、各エントリには、Microsoft のサポートされているネットワーク コンポーネントのベンダーから提供されたアップグレード ファイルを含むディレクトリへの完全パスを指定します。 アップグレード中のすべてのネットワーク構成の対応するエントリがあります、 **OemNetUpgradeDirs**セクション。

Netupg.inf ファイルの例を次に示します。

```INF
[OemNetUpgradeDirs]
c:\temp\adapter1
c:\temp\adapter2
c:\temp\protocol1
c:\temp\netclient1
c:\temp\netservice1
```

指定された各ディレクトリ、 **OemNetUpgradeDirs**セクション netmap.inf ファイルのファイルを含める必要があります。 このファイルは、ネットワーク コンポーネントのベンダーによって提供されるは、アップグレードされたオペレーティング システムに対応する ID に、アップグレード前のデバイス、ハードウェアまたはネットワーク コンポーネントの互換性のある ID をマップします。

 

 





