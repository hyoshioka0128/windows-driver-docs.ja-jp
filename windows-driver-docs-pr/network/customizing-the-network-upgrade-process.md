---
title: ネットワーク アップグレード プロセスのカスタマイズ
description: ネットワーク アップグレード プロセスのカスタマイズ
ms.assetid: c754317c-fe31-4a61-9c73-93ae71f64b03
keywords:
- ネットワーク コンポーネントのアップグレード、WDK をカスタマイズします。
- WDK のネットワーク コンポーネントをアップグレードする、カスタマイズ
- アップグレード プロセスの WDK ネットワークのカスタマイズ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f96f90dfa6dc299ee15b426aa4364a2f30a8262d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570468"
---
# <a name="customizing-the-network-upgrade-process"></a>ネットワーク アップグレード プロセスのカスタマイズ





**注**  Microsoft Windows XP では、ベンダーから提供されたネットワークのアップグレードはサポートされていない (SP1 以降)、Microsoft Windows Server 2003、および以降のオペレーティング システム。

 

システム管理者は、ネットワークのアップグレード プロセスをカスタマイズできます。

**ネットワークのアップグレード プロセスをカスタマイズするには**

1.  アップグレードするには、各ネットワーク コンポーネントのシステム上のディレクトリを作成します。

2.  手順 1. で作成した適切なディレクトリに、各ネットワーク コンポーネントのベンダーから提供されたアップグレード ファイルをコピーします。 これらのファイルには、netmap.inf ファイルのファイルを含める必要があります。 NetSetup は、アップグレードするのにには、どのネットワーク コンポーネントを識別するために、netmap.inf ファイルのファイルを使用します。

3.  含む netupg.inf ファイルを作成、 **OemNetUpgradeDirs**セクションし、任意のディレクトリに配置します。 内の各行の**OemNetUpgradeDirs** netupg.inf ファイルのセクションは、手順 1. で作成されたディレクトリへのパスを指定します。 Netupg.inf ファイルで指定された各ディレクトリは、netmap.inf ファイルのファイルを含む、ネットワーク コンポーネントのベンダーから提供されたアップグレード ファイルを含める必要があります。

4.  設定、NET\_UPGRD\_INIT\_ファイル\_netupg.inf ファイルが含まれているディレクトリに DIR 環境変数。

ネットワークのアップグレードの Winnt32 フェーズでは、NetSetup netupg.inf ファイルは内で検索、NETUPGRD で指定されたディレクトリ\_INIT\_ファイル\_DIR 環境変数。 NetSetup は、netupg.inf ファイルで指定したディレクトリごとに、netmap.inf ファイルのファイル サービスおよびネットワーク コンポーネントにアップグレードするには、その他の仕入先ファイルを検索します。 NetSetup では、これらのファイルをコンポーネントのアップグレードを処理します。 詳細については、次を参照してください。 [ネットワークのアップグレード処理](the-network-upgrade-process.md)します。

 

 





