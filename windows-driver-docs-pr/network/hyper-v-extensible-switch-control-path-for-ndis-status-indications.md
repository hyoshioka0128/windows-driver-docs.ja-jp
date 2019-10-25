---
title: NDIS ステータス表示用の hyper-v 拡張可能スイッチ制御パス
description: NDIS 状態表示用の Hyper-V 拡張可能スイッチ制御パス
ms.assetid: D52FAC95-64EC-4A99-807A-B39DB136D8F9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49cc4854af6c6748337c137093fc02a654176037
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823927"
---
# <a name="hyper-v-extensible-switch-control-path-for-ndis-status-indications"></a>NDIS 状態表示用の Hyper-V 拡張可能スイッチ制御パス


このトピックでは、基盤となる物理アダプターからの NDIS ステータスを示すコントロールパスについて説明します。 1つまたは複数の基になる物理アダプターを、Hyper-v 拡張可能スイッチの外部ネットワークアダプターとチーミングすることができます。

たとえば、拡張可能スイッチの外部ネットワークアダプターは、NDIS マルチプレクサー (MUX) 中間ドライバーの仮想ミニポートエッジにバインドできます。 MUX 中間ドライバー自体は、ホスト上の1つまたは複数の物理ネットワークのチームにバインドできます。 この構成は、*拡張可能なスイッチチーム*と呼ばれています。 拡張可能なスイッチチームの詳細については、「[物理ネットワークアダプターの構成の種類](types-of-physical-network-adapter-configurations.md)」を参照してください。

この構成では、拡張可能なスイッチ拡張機能は、拡張可能なスイッチチームのすべてのネットワークアダプターに公開されます。 これにより、拡張可能なスイッチドライバースタックの転送拡張機能が、チーム内の個々のネットワークアダプターの構成と使用を管理できるようになります。 たとえば、拡張機能は、送信パケットを個々のアダプターに転送することによって、チームで負荷分散フェールオーバー (LBFO) ソリューションのサポートを提供できます。 このような拡張機能は、*チーミングプロバイダー*と呼ばれます。 チーミングプロバイダーの詳細については、「[チーミングプロバイダーの拡張機能](teaming-provider-extensions.md)」を参照してください。

**注**  この並べ替えの操作は、転送拡張機能によってのみ実行できます。 この種類のドライバーの詳細については、「[拡張機能の転送](forwarding-extensions.md)」を参照してください。

 

次の図は、NDIS 6.40 (Windows Server 2012 R2) 以降の基盤となる拡張可能なスイッチチームによって発行された NDIS ステータス表示の拡張可能なスイッチ制御パスを示しています。

![ndis 6.40 の vswitch チームからの ndis ステータスを示す vswitch 制御パス](images/vswitch-status-controlpath2-ndis640.png)

次の図は、NDIS 6.30 (Windows Server 2012) の基盤となる拡張可能なスイッチチームによって発行された NDIS ステータス表示の拡張可能なスイッチ制御パスを示しています。

![ndis 6.30 の vswitch チームからの ndis ステータスを示す vswitch 制御パス](images/vswitch-status-controlpath2.png)

**注**  拡張可能なスイッチインターフェイスでは、NDIS フィルタードライバーは拡張*可能なスイッチ拡張機能*と呼ばれ、ドライバースタックは*拡張可能なスイッチドライバースタック*と呼ばれます。

 

拡張可能なスイッチは、次の方法で、基盤となる物理アダプターまたは拡張可能なスイッチチームからの NDIS ステータスをサポートします。

-   NDIS ステータスの表示が拡張可能スイッチインターフェイスに到着すると、 [**ndis\_スイッチ\_NIC\_状態\_示さ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication)れる構造体の内部に示された情報がカプセル化されます。 次に、拡張可能スイッチのミニポートエッジは、この構造を含む[ **\_NIC\_状態を示す\_スイッチの\_の状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-nic-status)を示します。

    転送拡張機能は、この表示を受け取ると、カプセル化されたデータを変更するように指示を複製できます。 これにより、転送拡張機能は、基になる拡張可能なスイッチチームの指定された状態または機能を変更できます。

-   チーミングプロバイダーとして動作する転送拡張機能は、 [**NDIS\_の状態\_スイッチ\_NIC\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-nic-status)の情報が関連付けられています。オフロードテクノロジ。

    たとえば、プロバイダーは Ndis\_の状態を開始できます[ **\_スイッチ\_NIC\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-nic-status)をカプセル化された NDIS\_状態で\_\_を[**受信\_フィルター\_現在**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-receive-filter-current-capabilities)アダプターチームの仮想マシンキュー (VMQ) のオフロード機能を変更する機能を示します。

-   また、チーミングプロバイダーは、 [**NDIS\_の状態\_切り替え\_NIC\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-nic-status)の表示を開始して、拡張可能なスイッチチーム以外のネットワークアダプター構成を変更することもできます。

    たとえば、拡張機能は、Ndis\_の状態を開始し[ **\_スイッチに\_NIC\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-nic-status)の状態をカプセル化された[**ndis\_状態\_スイッチ\_ポート**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-port-remove-vf)\_\_の VF を削除します。 この表示では、仮想マシン (VM) ネットワークアダプターと PCI Express (PCIe) 仮想関数 (VF) の間のバインドが削除されます。 VF は、シングルルート i/o 仮想化 (SR-IOV) インターフェイスをサポートする、基になる物理ネットワークアダプターによって公開されます。

    このバインドが削除された後、パケットは、VM ネットワークアダプターと、基になる SR-IOV 物理アダプターの VF の間ではなく、拡張可能なスイッチポートを介して配信されます。 これにより、拡張可能なスイッチポートで受信または送信されたパケットに、拡張可能なスイッチポートポリシーを適用できます。

**注**  拡張可能なスイッチ拡張機能は、すべての ndis フィルタードライバーに適用される ndis ステータスをフィルター処理する場合と同じガイドラインに従う必要があります。 詳細については、「[フィルターモジュールの状態](filter-module-status-indications.md)の表示」を参照してください。

 

転送拡張機能が Ndis\_の状態を開始する方法の詳細については[ **\_\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-nic-status) 「[物理ネットワークアダプターからの ndis ステータス](managing-ndis-status-indications-from-physical-network-adapters.md)の表示の管理」を参照してください。

 

 





