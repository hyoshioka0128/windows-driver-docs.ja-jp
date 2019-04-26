---
title: HYPER-V 拡張可能スイッチ コントロールのパスの NDIS 状態の表示
description: NDIS 状態表示用の Hyper-V 拡張可能スイッチ制御パス
ms.assetid: D52FAC95-64EC-4A99-807A-B39DB136D8F9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67fb1a1a709881b42ea1c5612e5038729d64d4ca
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341912"
---
# <a name="hyper-v-extensible-switch-control-path-for-ndis-status-indications"></a>NDIS 状態表示用の Hyper-V 拡張可能スイッチ制御パス


このトピックでは、コントロールのパスを基になる物理アダプターから NDIS 状態インジケーターを移動させるについて説明します。 HYPER-V 拡張可能スイッチの外部ネットワーク アダプターを使用した 1 つまたは複数の基になる物理アダプターのチームを構成することができます。

たとえば、拡張可能スイッチの外部ネットワーク アダプターは、NDIS マルチプレクサー (マルチプレクサー) の中間ドライバーの仮想ミニポート端にバインドできます。 MUX 中間ドライバー自体は、ホスト上の 1 つまたは複数の物理ネットワーク チームにバインドできます。 この構成と呼ばれる、*拡張可能スイッチ チーム*します。 拡張可能スイッチ チームの詳細については、次を参照してください。[型の物理ネットワーク アダプターの構成](types-of-physical-network-adapter-configurations.md)します。

この構成では、拡張可能スイッチ拡張機能は拡張可能スイッチ チームのすべてのネットワーク アダプターに公開されます。 これにより、転送拡張機能が拡張可能スイッチのドライバー スタックを構成し、チーム内の個々 のネットワーク アダプターの使用を管理するの。 たとえば、拡張機能では、個々 のアダプターに送信されるパケットを転送することによって、over、チーム分散フェールオーバー (LBFO) のソリューション ロードのサポートを提供できます。 このような拡張機能と呼ばれる、*チーミング プロバイダー*します。 プロバイダーのチーミングの詳細については、次を参照してください。[プロバイダーの拡張機能のチーミング](teaming-provider-extensions.md)します。

**注**  このような操作は、転送拡張機能でのみ実行できます。 この種類のドライバーの詳細については、次を参照してください。[転送拡張機能](forwarding-extensions.md)します。

 

次の図には、NDIS 6.40 (Windows Server 2012 R2) 以降は、基になる拡張可能スイッチ チームによって発行された NDIS 状態インジケーターの拡張可能スイッチ コントロール パスが表示されます。

![ndis 6.40 の vswitch チームからの ndis 状態インジケーターの vswitch コントロール パス](images/vswitch-status-controlpath2-ndis640.png)

次の図には、NDIS 6.30 (Windows Server 2012) の基になるの拡張可能スイッチ チームによって発行された NDIS 状態インジケーターの拡張可能スイッチ コントロール パスが表示されます。

![ndis 6.30 の vswitch チームからの ndis 状態インジケーターの vswitch コントロール パス](images/vswitch-status-controlpath2.png)

**注**  、拡張可能スイッチのインターフェイスで NDIS フィルター ドライバーと呼ばれる*拡張可能スイッチの拡張機能*と呼ばれるドライバー スタック、*拡張可能スイッチ ドライバー スタック*.

 

拡張可能スイッチは、次の方法で基になる物理アダプターまたは拡張可能スイッチ チームからの NDIS 状態インジケーターをサポートします。

-   拡張可能スイッチのインターフェイスで NDIS 状態を示す値が到着すると、内で示す値をカプセル化、 [ **NDIS\_切り替える\_NIC\_状態\_を示す値**](https://msdn.microsoft.com/library/windows/hardware/hh598217)構造体。 拡張可能スイッチに関する問題のミニポート edge し、 [ **NDIS\_状態\_スイッチ\_NIC\_状態**](https://msdn.microsoft.com/library/windows/hardware/hh598205)これを含むことを示しています構造体。

    転送拡張機能は、この通知を受信すると、カプセル化されたデータ変更を示す値を複製できます。 これにより、指定されたステータスまたは基になる拡張可能スイッチ チームの能力を変更する転送拡張機能です。

-   チーミング プロバイダーは、ハードウェアのアダプターのチームの構成に参加できるように動作する転送拡張機能を開始することでオフロード[ **NDIS\_状態\_スイッチ\_NIC\_ステータス**](https://msdn.microsoft.com/library/windows/hardware/hh598205)オフロード テクノロジに関連することを示すものです。

    たとえば、プロバイダーが開始できる、 [ **NDIS\_状態\_スイッチ\_NIC\_状態**](https://msdn.microsoft.com/library/windows/hardware/hh598205)をカプセル化されたを示す値[ **NDIS\_状態\_受信\_フィルター\_現在\_機能**](https://msdn.microsoft.com/library/windows/hardware/hh439814)オフロード機能を変更することを示す値アダプターのチームでの仮想マシン キュー (VMQ)。

-   プロバイダーのチーム化を開始できますも、 [ **NDIS\_状態\_スイッチ\_NIC\_状態**](https://msdn.microsoft.com/library/windows/hardware/hh598205)を示す値を他のネットワーク アダプターを変更するには拡張可能スイッチ チーム以外の構成。

    たとえば、拡張機能を開始できる、 [ **NDIS\_状態\_スイッチ\_NIC\_状態**](https://msdn.microsoft.com/library/windows/hardware/hh598205)でカプセル化された[ **NDIS\_状態\_スイッチ\_ポート\_削除\_VF** ](https://msdn.microsoft.com/library/windows/hardware/hh598206)を示す値。 この通知は、仮想マシン (VM) ネットワーク アダプターと PCI Express (PCIe) 仮想機能 (VF) 間のバインドを削除します。 VF は、シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートする、基になる物理ネットワーク アダプターによって公開されます。

    このバインドが削除された後、パケットは VM のネットワーク アダプターと基になる、SR-IOV 対応の物理アダプターの VF 間で直接の代わりに拡張可能スイッチ ポートを介して配信されます。 これにより、拡張可能スイッチ ポートの受信または拡張可能スイッチ ポート経由で送信されるパケットに適用するポリシー。

**注**  拡張可能スイッチ拡張機能が NDIS フィルター ドライバーをすべてに適用される NDIS 状態インジケーターをフィルター処理と同じガイドラインに従う必要があります。 詳細については、次を参照してください。[フィルター モジュールの状態インジケーター](filter-module-status-indications.md)します。

 

方法を開始できる転送拡張機能の詳細については[ **NDIS\_状態\_スイッチ\_NIC\_状態**](https://msdn.microsoft.com/library/windows/hardware/hh598205) 、指示を参照してください[NDIS 状態インジケーターを管理する物理ネットワーク アダプターから](managing-ndis-status-indications-from-physical-network-adapters.md)します。

 

 





