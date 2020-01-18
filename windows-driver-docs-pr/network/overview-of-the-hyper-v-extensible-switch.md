---
title: Hyper-V 拡張可能スイッチの概要
description: このセクションでは、Hyper-v 拡張可能スイッチの概要について説明します。
ms.assetid: 78181C72-FBFD-4860-A664-C297997D780F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9a7433ef16457a9a9e5844b5eb9d894490efd38
ms.sourcegitcommit: 6d930ed810124ade8e29a617c7abcd399113696f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/17/2020
ms.locfileid: "76256758"
---
# <a name="overview-of-the-hyper-v-extensible-switch"></a>Hyper-V 拡張可能スイッチの概要

Windows Server 2012 では、hyper-v の拡張可能スイッチ (Hyper-v 仮想スイッチとも呼ばれます) が導入されています。これは、Hyper-v の親パーティションの管理オペレーティングシステムで実行される仮想イーサネットスイッチです。 このページでは、次の項目について説明します。

- [バックグラウンド読み取り](#background-reading)
- [Hyper-v 拡張可能スイッチとネットワークアダプターの種類](#types-of-hyper-v-extensible-switches-and-network-adapters)
- [拡張可能なスイッチ拡張機能の種類](#types-of-extensible-switch-extensions)
- [Hyper-v 拡張可能スイッチのアーキテクチャ図](#hyper-v-extensible-switch-architectural-diagrams)

## <a name="background-reading"></a>バックグラウンド読み取り

このテクノロジとその基盤の技術的な概要については、TechNet の次のドキュメントを参照してください。

- [Hyper-V 仮想スイッチの概要](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831823(v=ws.11))
- [Hyper-V ネットワーク仮想化の概要](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj134230(v=ws.11))
- [Hyper-V の概要](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831531(v=ws.11))

## <a name="types-of-hyper-v-extensible-switches-and-network-adapters"></a>Hyper-v 拡張可能スイッチとネットワークアダプターの種類

Hyper-v Virtual Network マネージャーを使用すると、次の種類の1つ以上の拡張可能なスイッチを作成、構成、または削除できます。

- 1つの外部ネットワークアダプターおよび1つ以上の仮想マシン (VM) ネットワークアダプターに接続するポートをサポートする外部拡張可能なスイッチ。 この種類のスイッチを使用すると、すべての Hyper-v パーティションとホスト上の物理ネットワークインターフェイスの間でパケットを送受信できます。

    また、管理オペレーティングシステムで実行されるアプリケーションとドライバーは、この種類のスイッチを使用してパケットを送受信できます。

- 1つ以上の内部ネットワークアダプターおよび1つ以上の VM ネットワークアダプターに接続するポートをサポートする内部拡張可能なスイッチ。 この種類のスイッチを使用すると、Hyper-v の親パーティションとホスト上の1つ以上の Hyper-v 子パーティションとの間でパケットを送受信できます。

    また、管理オペレーティングシステムで実行されるアプリケーションとドライバーは、この種類のスイッチを使用してパケットを送受信できます。

- 1つまたは複数の VM ネットワークアダプターに接続するポートをサポートするプライベート拡張可能なスイッチ。 この種類のスイッチでは、Hyper-v の子パーティション間でのみパケットを送受信できます。

    **注**  管理オペレーティングシステムで実行されるアプリケーションとドライバーは、この種類のスイッチを使用してパケットを送受信できません。

拡張可能な各スイッチモジュールは、Hyper-v の子および親パーティションによって使用されるネットワークアダプター上で、着信パケットと送信パケットをルーティングします。 これらのネットワークアダプターには次のものが含まれます。

- ホストで使用可能な物理ネットワークインターフェイスへの接続を提供する外部ネットワークアダプター。

    この種類のネットワークアダプターの詳細については、「[外部ネットワークアダプター](https://docs.microsoft.com/windows-hardware/drivers/network/external-network-adapters)」を参照してください。

    **注**  外部ネットワークアダプターへのアクセスを提供できるのは、外部の拡張可能なスイッチだけです。

- Hyper-v 親パーティションの管理オペレーティングシステムで実行されるプロセスの拡張可能なスイッチへのアクセスを提供する内部ネットワークアダプター。 これにより、これらのプロセスが拡張可能スイッチでパケットを送受信できるようになります。

    この種類のネットワークアダプターの詳細については、「[内部ネットワークアダプター](https://docs.microsoft.com/windows-hardware/drivers/network/internal-network-adapters)」を参照してください。

    **注**  内部ネットワークアダプターへのアクセスを提供できるのは、外部および内部の拡張可能なスイッチだけです。

- Hyper-v 子パーティションで実行されているゲストオペレーティングシステム内で公開されている VM ネットワークアダプター。 VM ネットワークアダプターは、子パーティションのゲストオペレーティングシステムで実行されるプロセスによって送信または受信されるパケットの拡張可能なスイッチへの接続を提供します。

    この種類のネットワークアダプターの詳細については、「[仮想マシンネットワークアダプター](https://docs.microsoft.com/windows-hardware/drivers/network/virtual-machine-network-adapters)」を参照してください。

各 Hyper-v 子パーティションは、1つまたは複数の VM ネットワークアダプターを持つように構成できます。 各 VM ネットワークアダプターは、拡張可能スイッチのインスタンスに関連付けられるように構成されています。 これにより、子パーティションを次のように構成できます。

- 子パーティションは、拡張可能スイッチの1つのインスタンスに関連付けられた単一の VM ネットワークアダプターを持つように構成できます。

- 子パーティションは、複数の VM ネットワークアダプターを使用するように構成できます。各 VM ネットワークアダプターは、拡張可能なスイッチのインスタンスに関連付けられています。

- 子パーティションは複数の VM ネットワークアダプターを持つように構成することができ、1つまたは複数の VM ネットワークアダプターが拡張スイッチの同じインスタンスに関連付けられています。

## <a name="types-of-extensible-switch-extensions"></a>拡張可能なスイッチ拡張機能の種類

Hyper-v 拡張可能スイッチは、独立系ソフトウェアベンダー (Isv) が次の方法でスイッチ機能を拡張できるインターフェイスをサポートしています。

- Hyper-v 拡張可能スイッチは、*拡張機能*と呼ばれる NDIS フィルタードライバーが拡張可能なスイッチドライバースタック内でバインドできるようにするインターフェイスをサポートしています。 これにより、拡張機能は、拡張可能なスイッチポートにパケットをキャプチャ、フィルター処理、および転送できます。 これにより、拡張機能は、Hyper-v パーティションで公開されているネットワークアダプターに接続されているポートにパケットを挿入、削除、またはリダイレクトすることができます。

    拡張機能をインストールした後は、Hyper-v 拡張可能スイッチの個別のインスタンスで有効または無効にすることができます。 詳細については、「 [Hyper-v 拡張可能スイッチ拡張機能のインストール](https://docs.microsoft.com/windows-hardware/drivers/network/installing-hyper-v-extensible-switch-extensions)」を参照してください。

- Windows Filtering Platform (WFP) には、インボックスフィルター拡張機能 (変更可能) が用意されています。これにより、WFP フィルターまたはコールアウトドライバーは、Hyper-v 拡張可能スイッチのデータパスに沿ってパケットを傍受できます。 これにより、wfp フィルターまたはコールアウトドライバーは、WFP 管理とシステム機能を使用して、パケット検査または変更を実行できます。

    WFP の概要については、「 [Windows Filtering Platform](https://docs.microsoft.com/windows-hardware/drivers/network/porting-packet-processing-drivers-and-apps-to-wfp)」を参照してください。

    WFP コールアウトドライバーの概要については、「 [Windows フィルタリングプラットフォームのコールアウトドライバー](https://docs.microsoft.com/windows-hardware/drivers/network/windows-filtering-platform-callout-drivers2)」を参照してください。

    **注**  拡張可能なスイッチパケットトラフィックの wfp ベースのフィルター処理を実行するには、isv は、拡張された wfp 呼び出しとデータ型を使用するように、wfp フィルターとコールアウトドライバーを拡張するだけで済みます。 Isv は独自の拡張機能を開発する必要はありません。

拡張可能なスイッチインターフェイスは、次の種類の拡張機能をサポートしています。

<a href="" id="capturing-extensions"></a>拡張機能のキャプチャ  
パケットトラフィックをキャプチャして監視する拡張機能。 この種類の拡張機能では、パケットの変更や削除、または拡張可能なスイッチポートへのパケットの配信を除外することはできません。 ただし、拡張機能のキャプチャでは、拡張機能がホストアプリケーションに送信するトラフィックの統計情報を含むパケットなど、パケットトラフィックが発生する可能性があります。

拡張可能なスイッチの各インスタンスで、複数のキャプチャ拡張機能をバインドし、有効にすることができます。

この種類の拡張機能の詳細については、「[拡張機能のキャプチャ](https://docs.microsoft.com/windows-hardware/drivers/network/capturing-extensions)」を参照してください。

<a href="" id="filtering-extensions"></a>拡張機能のフィルター処理  
これらの拡張機能は、拡張機能のキャプチャと同じ機能を持ちます。 ただし、ポートまたはスイッチのポリシー設定に基づいて、この種類の拡張機能はパケットの検査と削除、または拡張可能なスイッチポートへのパケット配信の除外を行うことができます。 フィルター拡張機能は、パケットの生成、複製、複製を行ったり、拡張可能なスイッチのデータパスに挿入したりすることもできます。

拡張可能なスイッチの各インスタンスで、複数のフィルター拡張機能をバインドし、有効にすることができます。

この種類の拡張機能の詳細については、「[拡張機能のフィルター選択](https://docs.microsoft.com/windows-hardware/drivers/network/filtering-extensions)」を参照してください。

<a href="" id="forwarding-extensions"></a>拡張機能の転送  
これらの拡張機能は、拡張機能のフィルター処理と同じ機能を持ちますが、拡張可能スイッチのコアパケット転送タスクとフィルター処理タスクを実行する責任があります。 これらのタスクには、次のものが含まれます。

- パケットが NVGRE パケットでない場合は、パケットの宛先ポートを決定します。 詳細については、「[ハイブリッド転送](https://docs.microsoft.com/windows-hardware/drivers/network/hybrid-forwarding)」を参照してください。

- セキュリティ、プロファイル、仮想 LAN (VLAN) ポリシーなどの標準ポートポリシーを適用してパケットをフィルター処理します。

**注**  拡張可能スイッチに転送拡張機能がインストールされていない場合、スイッチはパケットの宛先ポートを特定し、標準のポート設定に基づいてパケットをフィルター処理します。

拡張可能なスイッチの各インスタンスでバインドおよび有効化できる転送拡張機能は1つだけです。

この種類の拡張機能の詳細については、「[拡張機能の転送](https://docs.microsoft.com/windows-hardware/drivers/network/filtering-extensions)」を参照してください。

## <a name="hyper-v-extensible-switch-architectural-diagrams"></a>Hyper-v 拡張可能スイッチのアーキテクチャ図

次の図は、NDIS 6.40 (Windows Server 2012 R2) およびそれ以降の拡張可能スイッチインターフェイスのコンポーネントを示しています。

![ndis 6.40 以降のハイパー\-v 拡張可能スイッチアーキテクチャを示す図](images/vswitcharchitecture-ndis640.png)

次の図は、NDIS 6.30 (Windows Server 2012) 用の拡張可能スイッチインターフェイスのコンポーネントを示しています。

![sr-iov を使用した統合デバイスデータパスを示す図](images/vswitcharchitecture.png)

拡張可能スイッチインターフェイスのコンポーネントの詳細については、「 [Hyper-v 拡張可能スイッチのアーキテクチャ](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-architecture)」を参照してください。
