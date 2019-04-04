---
title: 物理ネットワーク アダプターからの発信元の NDIS 状態インジケーター
description: 物理ネットワーク アダプターからの NDIS 状態表示の生成
ms.assetid: D588CD7E-98A3-4BA8-A467-6492DA2186CA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9261ff1785e113957e549d2028a5ba17651d633
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578356"
---
# <a name="originating-ndis-status-indications-from-physical-network-adapters"></a>物理ネットワーク アダプターからの NDIS 状態表示の生成


このトピックでは、スイッチに接続されているネットワーク アダプターの NDIS 状態インジケーターを送信する転送拡張機能を拡張可能スイッチで使用されるメソッドを説明します。 次の種類のアダプターの NDIS 状態を示す値を開始できるは、拡張機能。

-   1 つ以上の物理アダプターにバインドされている基になる、[外部ネットワーク アダプター](external-network-adapters.md)の拡張可能スイッチ。

    たとえば、外部ネットワーク アダプターは、NDIS マルチプレクサー (マルチプレクサー) の中間ドライバーの仮想ミニポート端にバインドできます。 MUX driver は、ホスト上の 1 つまたは複数の物理ネットワーク チームにバインドされます。 この構成と呼ばれる、*拡張可能スイッチ チーム*します。

    この構成で拡張可能スイッチの拡張機能は、チーム内のすべてのネットワーク アダプターに公開されます。 これにより、拡張機能の構成と、チーム内の個々 のネットワーク アダプターの使用を管理できます。 たとえば、転送拡張機能では、個々 のアダプターに送信されるパケットを転送することによって、over、チーム分散フェールオーバー (LBFO) のソリューション ロードのサポートを提供できます。 拡張可能スイッチ チームを管理する転送拡張機能が呼ばれる、*チーミング プロバイダー*します。 プロバイダーのチーミングの詳細については、[プロバイダーの拡張機能のチーミング](teaming-provider-extensions.md)を参照してください。

-   HYPER-V 子パーティション内で公開され、拡張可能スイッチ ポートに接続される仮想マシン (VM) ネットワーク アダプター。

次の図は、物理環境から NDIS 状態インジケーターと NDIS 6.40 (Windows Server 2012 R2) 以降の VM ネットワーク アダプターの HYPER-V 拡張可能スイッチ コントロール パスを示します。

![ndis 6.40 およびそれ以降の物理マシンと vm のネットワーク アダプターから ndis 状態インジケーターの vswitch コントロール パス](images/vswitch-status-controlpath3-ndis640.png)

次の図は、物理環境から NDIS 状態インジケーターの HYPER-V 拡張可能スイッチ コントロール パスと NDIS 6.30 (Windows Server 2012) の VM のネットワーク アダプターを示します。

![物理から状態インジケーターの ndis および ndis 6.30 の vm のネットワーク アダプターの vswitch コントロール パス](images/vswitch-status-controlpath3.png)

**注**  、拡張可能スイッチのインターフェイスでは、NDIS フィルター ドライバーと呼ばれます*拡張*と呼ばれるドライバー スタック、*ドライバー スタックの拡張可能スイッチ*。

 

転送拡張機能は、後続の拡張可能スイッチのドライバー スタックのドライバーをカプセル化されたハードウェア オフロード状態インジケーターを取得できます。 これは、基になる物理アダプターの拡張可能スイッチの外部ネットワーク アダプターにバインドされているチームの現在のオフロード機能を変更する拡張機能もできます。 アダプターのチームが外部ネットワーク アダプターにバインドされると、チームの一般的な機能のみが NDIS または上位のプロトコルとフィルター ドライバーにアドバタイズされます。 拡張機能は、チーム内で一部のアダプターでサポートされている機能を提供するカプセル化された状態のインジケーターを送信して提供機能を拡張できます。 たとえば、拡張機能がカプセル化されたに発行できます[ **NDIS\_状態\_受信\_フィルター\_現在\_機能**](https://msdn.microsoft.com/library/windows/hardware/hh439814)現在有効な変更を示す値には、チーム全体でのフィルター機能が表示されます。

**注**  転送拡張機能と、カプセル化された状態の問題が発生することだけです。 この種類の拡張機能の詳細については、[転送拡張機能](forwarding-extensions.md)を参照してください。

 

通常、転送拡張機能では、基になる物理アダプターのアドバタイズされたハードウェア オフロード機能を変更するのカプセル化された NDIS 状態インジケーターが生成されます。 たとえば、ハードウェアのオフロードの次の種類の状態インジケーターを開始できるは、拡張機能。

-   インターネット プロトコル セキュリティ (IPsec)。

-   仮想マシン キュー (VMQ)。

-   シングル ルート I/O 仮想化 (SR-IOV)。

転送拡張機能は、HYPER-V 子パーティションに割り当てられているハードウェア オフロード リソースを変更するのカプセル化された NDIS 状態インジケーターも取得できます。 NDIS 6.30 以降では、拡張機能をカプセル化された発行[ **NDIS\_状態\_スイッチ\_ポート\_削除\_VF** ](https://msdn.microsoft.com/library/windows/hardware/hh598206)VM のネットワーク アダプターと PCI Express (PCIe) 仮想機能 (VF) 間のバインドを削除するを示す値。 VF が公開され、サポートする、基になる物理ネットワーク アダプターでサポートされている、[シングル ルート I/O 仮想化 (SR-IOV)](single-root-i-o-virtualization--sr-iov-.md)インターフェイス。

メンバーを設定する必要があります、転送拡張機能では、カプセル化された NDIS 状態を示す値のハードウェアのオフロード リソースについて、基になる物理アダプターの作成元である場合、 [ **NDIS\_スイッチ\_NIC\_ステータス\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/hh598217)次のように構造体。

-   **DestinationPortId**にメンバーを設定する必要があります**NDIS\_スイッチ\_既定\_ポート\_ID**します。
-   **DestinationNicIndex**にメンバーを設定する必要があります**NDIS\_スイッチ\_既定\_NIC\_インデックス**

-   **SourcePortId**メンバーは、外部ネットワーク アダプターが接続されている拡張可能スイッチ ポートの識別子を設定する必要があります。

-   **SourceNicIndex**にメンバーを設定する必要があります**NDIS\_スイッチ\_既定\_NIC\_インデックス**します。 これにより、外部ネットワーク アダプターにバインドされている全体の拡張可能スイッチ チームからのものとして解釈される状態の表示ができます。

    **注**  転送拡張機能にこのメンバーを設定する必要がありますも**NDIS\_スイッチ\_既定\_NIC\_インデックス**場合、単一の物理ネットワークのみアダプターは、外部ネットワーク アダプターにバインドされます。

     

-   **StatusIndication**へのポインターにメンバーを設定する必要があります、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)構造体。 この構造体には、カプセル化された NDIS 状態表示のデータが含まれています。

メンバーを設定する必要があります、転送拡張機能には、HYPER-V 子パーティションのハードウェアのオフロード リソース用の NDIS 状態表示が発信をしている場合、 [ **NDIS\_スイッチ\_NIC\_ステータス\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/hh598217)次のように構造体。

-   **DestinationPortId**と**DestinationNicIndex**メンバーは、パーティションによって使用されるネットワーク接続のポートとネットワーク アダプターのインデックスの対応する値に設定する必要があります。

-   **SourcePortId**にメンバーを設定する必要があります**NDIS\_スイッチ\_既定\_ポート\_ID**します。

-   **SourceNicIndex**にメンバーを設定する必要があります**NDIS\_スイッチ\_既定\_NIC\_インデックス**します。

-   **StatusIndication**へのポインターにメンバーを設定する必要があります、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)構造体。 この構造体には、カプセル化された NDIS 状態表示のデータが含まれています。

拡張機能がカプセル化された NDIS 状態表示を発行するときは、次の手順に従う必要があります。

1.  拡張機能の呼び出し[ *ReferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598294)元または転送先のネットワーク アダプター接続の参照カウンターをインクリメントします。 これにより、エントリの中に、その参照カウンターが 0 以外の場合、拡張可能スイッチのインターフェイスはネットワーク アダプターの接続が削除されません。

    拡張機能を呼び出すと[ *ReferenceSwitchNic*](https://msdn.microsoft.com/library/windows/hardware/hh598294)、次の方法でパラメーターを設定します。

    -   転送拡張機能には、基になる物理アダプターのカプセル化された NDIS 状態表示が発信場合、設定、 *SwitchPortId*パラメーターに指定された値を**SourcePortId**メンバー。 また、拡張機能、設定、 *SwitchNicIndex*パラメーターに指定された値を**SourceNicIndex**メンバー。

    -   転送拡張機能は、HYPER-V 子パーティションの NDIS 状態を示す値を発信元は場合、設定、 *SwitchPortId*パラメーターに指定された値を**DestinationPortId**メンバー。 また、拡張機能、設定、 *SwitchNicIndex*パラメーターに指定された値を**DestinationNicIndex**メンバー。

    **注**  場合[ *ReferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598294) NDIS を返さない\_状態\_成功した場合、カプセル化された NDIS 状態表示を発行することはできません.

     

2.  拡張機能の呼び出し[ **NdisFIndicateStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff561824)をカプセル化された状態の通知を転送します。

    **注**  呼び出す必要がありますが、拡張機能では、フィルター選択された OID 要求の転送する場合[ **NdisFIndicateStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff561824)への呼び出しのコンテキスト内でその[ *FilterStatus* ](https://msdn.microsoft.com/library/windows/hardware/ff549973)関数。

     

3.  後[ **NdisFIndicateStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff561824)拡張機能の呼び出しから返される[ *DereferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598141)の参照カウンターをオフにします送信元または送信先のネットワーク アダプター接続します。 拡張機能セット、 *SwitchPortId*と*SwitchNicIndex*を同じパラメーター値への呼び出しで使用されるその it [ *ReferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598294).

 

 





