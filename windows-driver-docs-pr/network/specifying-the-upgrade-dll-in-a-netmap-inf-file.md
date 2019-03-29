---
title: Netmap.inf ファイル内のアップグレード DLL の指定
description: Netmap.inf ファイル内のアップグレード DLL の指定
ms.assetid: 01735a7d-ee33-427d-befa-7429fd64353b
keywords:
- ネットワーク コンポーネントのアップグレード WDK、netmap.inf ファイルのファイル
- ネットワーク コンポーネント、WDK netmap.inf ファイルのファイルをアップグレードします。
- WDK netmap.inf ファイルのファイル
- DLL の WDK netmap.inf ファイルをアップグレードします。
- デバイス Id の WDK netmap.inf ファイル
- ネットワークの移行-DLL の WDK netmap.inf ファイル
- Dll の WDK ネットワークのアップグレード
- ベンダーから提供されたファイルの WDK netmap.inf ファイルのファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 419782188d85fb046e836d9120c5fa8a1725e792
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582273"
---
# <a name="specifying-the-upgrade-dll-in-a-netmapinf-file"></a>Netmap.inf ファイル内のアップグレード DLL の指定





**注**  Microsoft Windows XP では、ベンダーから提供されたネットワークのアップグレードはサポートされていない (SP1 以降)、Microsoft Windows Server 2003、および以降のオペレーティング システム。

 

Netmap.inf ファイルのファイルが必要、 **OemUpgradeSupport**セクション。 アップグレードするには、各ネットワーク コンポーネント、 **OemUpgradeSupport**セクションを次の形式を持つエントリを含める必要があります。

*postupgrade-ID* = *network-migration-DLL*\[ , *Inf-file-name*\]

この場合

*postupgrade ID*は、ネットワーク コンポーネントの Windows 2000 または」の説明に従って、NetSetup によって取得された以降のデバイス ID、[ネットワークのアップグレード プロセスのフェーズを Winnt32](winnt32-phase-of-the-network-upgrade-process.md)します。

*ネットワークの移行-DLL*ネットワーク移行 NetSetup は、ネットワーク コンポーネントのアップグレードに読み込む必要がある DLL の名前を指定します。 Netmap.inf ファイルのファイルでは、1 つだけ移行 DLL を指定できます。 Netmap.inf ファイルのファイルには、複数のコンポーネントのデバイス ID のマッピングが含まれている場合、同じ移行 DLL によってこのようなすべてのコンポーネントをアップグレードする必要があります。

*Inf ファイル名*ネットワーク コンポーネントをインストールする INF ファイルの名前を指定します。

 

 





