---
title: HYPER-V 拡張可能スイッチの構成変更の OID 要求の受信
description: Hyper-V 拡張可能スイッチ構成変更に関する OID 要求の受信
ms.assetid: 9149BFF3-59B3-4563-A1A1-34FDD115964E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5178593ec01cc71c61a03d1f01305a2e36670e66
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572021"
---
# <a name="receiving-oid-requests-about-hyper-v-extensible-switch-configuration-changes"></a>Hyper-V 拡張可能スイッチ構成変更に関する OID 要求の受信

拡張可能スイッチのインターフェイスは拡張可能スイッチのコンポーネントの構成の変更点について、基になる拡張機能を通知し、拡張可能な発行することによってポリシーのパラメーターは、オブジェクト識別子 (OID) のセット要求を切り替えます。 これらの要求は、拡張可能スイッチ コンポーネントの構成とポリシー パラメーターの変更について、基になる拡張機能を通知する拡張可能スイッチのプロトコルの端で発行されます。 これらの OID 要求は、拡張可能スイッチの基になるミニポート エッジに拡張可能スイッチのドライバー スタックを移動します。

次の図には、OID 要求 NDIS 6.40 (Windows Server 2012 R2) と後で拡張可能スイッチ コントロール パスが表示されます。

![ndis 6.40 の vswitch oid コントロール パスの図](images/vswitch-oid-controlpath-ndis640.png)

次の図では、NDIS 6.30 (Windows Server 2012) の OID 要求の拡張可能スイッチ コントロール パスが表示されます。

![ndis 6.30 の vswitch oid コントロール パスの図](images/vswitch-oid-controlpath.png)

**注**、拡張可能スイッチのインターフェイスで NDIS フィルター ドライバーと呼ばれる*拡張可能スイッチの拡張機能*と呼ばれるドライバー スタック、*ドライバー スタックの拡張可能スイッチ*します。 

拡張可能スイッチのプロトコルの edge では、次の種類の通知の OID のセット要求を発行します。

-   拡張可能スイッチのポートの構成を変更します。

    プロトコル ドライバーの問題など、 [OID\_切り替える\_ポート\_作成](https://msdn.microsoft.com/library/windows/hardware/hh598272)に拡張可能スイッチのポートの作成の基になる拡張機能を通知します。 プロトコル ドライバーの問題では同様に、 [OID\_スイッチ\_ポート\_削除](https://msdn.microsoft.com/library/windows/hardware/hh598273)ポートの削除に関する拡張機能を通知します。

    この OID 通知の種類の詳細については、[Hyper-v 拡張可能スイッチ ポート](hyper-v-extensible-switch-ports.md)を参照してください。

-   拡張可能スイッチのポートへのネットワーク アダプターの接続に変更します。

    プロトコル ドライバーの問題など、 [OID\_切り替える\_NIC\_CONNECT](https://msdn.microsoft.com/library/windows/hardware/hh598262)に拡張可能スイッチのポートにネットワーク アダプターの接続について、基になる拡張機能を通知します。 プロトコル ドライバーの問題では同様に、 [OID\_スイッチ\_NIC\_切断](https://msdn.microsoft.com/library/windows/hardware/hh598265)に拡張機能、ネットワーク アダプターがポートから切断されていることを通知します。

    この OID 通知の種類の詳細については、[Hyper-v 拡張可能スイッチのネットワーク アダプター](hyper-v-extensible-switch-network-adapters.md)を参照してください。

-   拡張可能スイッチ ポートやスイッチ ポリシーに変更します。

    プロトコル ドライバーの問題など、 [OID\_切り替える\_プロパティ\_追加](https://msdn.microsoft.com/library/windows/hardware/hh598280)に拡張可能スイッチのプロパティの追加についての基になる拡張機能を通知します。 プロトコル ドライバーの問題では同様に、 [OID\_スイッチ\_ポート\_プロパティ\_削除](https://msdn.microsoft.com/library/windows/hardware/hh598276)ポートのプロパティの削除に関する拡張機能を通知します。

    この OID 通知の種類の詳細については、[管理の Hyper-v 拡張可能なスイッチのポリシー](managing-hyper-v-extensible-switch-extensibility-policies.md)を参照してください。

    **注**拡張機能が拡張可能スイッチの基になるミニポート edge によって管理されている既定のポートやスイッチ ポリシーへの変更の通知されません。

-   保存または実行時のポートのデータを復元します。

    プロトコル ドライバーの問題など、 [OID\_切り替える\_NIC\_保存](https://msdn.microsoft.com/library/windows/hardware/hh598280)に拡張可能スイッチに指定したポートの実行時データを保存する基になる拡張機能を通知します。 これらの Oid は、HYPER-V の状態がされているときに発行される保存したり、別のホストに移行します。 プロトコル ドライバーの問題では同様に、 [OID\_切り替える\_NIC\_復元](https://msdn.microsoft.com/library/windows/hardware/hh598267)に拡張機能で拡張可能スイッチ ポートの実行時データが復元されることを通知します。

    この OID 通知の種類の詳細については、[Hyper-v 拡張可能スイッチ実行時データの管理](managing-hyper-v-extensible-switch-run-time-data.md)を参照してください。

拡張可能スイッチ拡張機能のミニポート ドライバーは、これらの OID 要求を完了します。 ただしがいくつかの拡張可能スイッチ OID 要求基になる拡張機能では、通知を拒否する OID 要求を失敗ことができます。 たとえば、拡張可能スイッチ プロトコル ドライバーに通知する拡張可能スイッチで作成される新しいポートに関する、フィルター ドライバー、要求を発行、OID セットの[OID\_切り替える\_ポート\_を作成します](https://msdn.microsoft.com/library/windows/hardware/hh598272)。 基になるフィルター処理または転送拡張機能は、状態が、OID 要求を実行してポートの作成を拒否できます\_データ\_いない\_受理します。

拡張可能スイッチ拡張機能が次のガイドラインに従う必要がありますとその[ *FilterOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff549954)関数は拡張可能スイッチの OID 要求に対して呼び出されます。

-   データを指していますが、拡張機能は変更しないで、 *OidRequest*パラメーター。

-   拡張機能、いくつかの拡張可能スイッチの OID の要求の状態が、OID 要求を完了できる\_データ\_いない\_ACCEPTED です。 これは vetoes OID 要求が発行された、拡張可能スイッチ コンポーネントに対する操作です。

    拡張機能をたとえば、完了することができます、 [OID\_スイッチ\_NIC\_作成](https://msdn.microsoft.com/library/windows/hardware/hh598263)状態要求\_データ\_いない\_ACCEPTED です。 ドライバーは、ネットワーク接続が作成されている指定したポートで構成されているそのポリシーを満たすことができない場合に実行する必要があります。

    拡張機能は、oid には次のこの方法で要求を完了できます。

    -   [OID\_スイッチ\_NIC\_を作成します。](https://msdn.microsoft.com/library/windows/hardware/hh598263)

    -   [OID\_スイッチ\_ポート\_を作成します。](https://msdn.microsoft.com/library/windows/hardware/hh598272)

    -   [OID\_スイッチ\_ポート\_プロパティ\_追加](https://msdn.microsoft.com/library/windows/hardware/hh598275)

    -   [OID\_スイッチ\_ポート\_プロパティ\_削除](https://msdn.microsoft.com/library/windows/hardware/hh598276)

    -   [OID\_スイッチ\_ポート\_プロパティ\_UPDATE](https://msdn.microsoft.com/library/windows/hardware/hh598278)

    -   [OID\_スイッチ\_プロパティ\_追加](https://msdn.microsoft.com/library/windows/hardware/hh598280)

    -   [OID\_スイッチ\_プロパティ\_削除](https://msdn.microsoft.com/library/windows/hardware/hh598281)

    -   [OID\_スイッチ\_プロパティ\_UPDATE](https://msdn.microsoft.com/library/windows/hardware/hh598283)

-   呼び出す必要がありますが、拡張機能が、OID 要求が完了しない場合[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)拡張可能スイッチのドライバー スタック ダウン要求を転送します。

    **注**ドライバー呼び出しの前に[ **NdisFOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff561830)、ドライバーを呼び出す必要があります[ **NdisAllocateCloneOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff560706)に割り当て、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体し、新しい構造に、要求の情報を転送します。

    拡張機能は、OID の完了結果を監視する必要があります要求するときにその[ *FilterOidRequestComplete* ](https://msdn.microsoft.com/library/windows/hardware/ff549956)関数が呼び出されます。 これにより、拡張可能スイッチのコンポーネントでの操作が正常に完了したか、基になる拡張機能によって拒否されたかどうかを判断する拡張機能です。

    フィルター処理し、OID 要求を転送する方法の詳細については、[NDIS フィルター ドライバーでの OID 要求のフィルタ リング](filtering-oid-requests-in-an-ndis-filter-driver.md)を参照してください。


-   NDIS と上位のプロトコルとフィルター ドライバーは、基になる物理ネットワーク アダプターに、ハードウェア オフロード テクノロジの OID 要求を発行することができます。 これには、仮想マシン キュー (VMQ)、インターネット プロトコル セキュリティ (IPsec)、シングル ルート I/O 仮想化 (SR-IOV) などのオフロード テクノロジの OID 要求が含まれます。

    拡張可能スイッチのインターフェイスでこれらの OID 要求が届いたら、OID 要求内でカプセル化、 [ **NDIS\_切り替える\_NIC\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/hh598214). 拡張可能スイッチのプロトコルのエッジがの OID 要求を発行し、 [OID\_切り替える\_NIC\_要求](https://msdn.microsoft.com/library/windows/hardware/hh598266)この構造体を格納しています。

-   転送拡張機能を拡張可能スイッチは、外部ネットワーク アダプターにバインドされている 1 つまたは複数の物理アダプターには、NDIS ハードウェア オフロード テクノロジのサポートを提供できます。 この構成で拡張可能スイッチの外部ネットワーク アダプターは、NDIS マルチプレクサー (マルチプレクサー) の中間ドライバーの仮想ミニポート端にバインドされます。 MUX 中間ドライバーは、ホスト上の 1 つまたは複数の物理ネットワーク チームにバインドされます。 この構成と呼ばれる、*拡張可能スイッチ チーム*します。 拡張可能スイッチ チームの詳細については、[型の物理ネットワーク アダプターの構成](types-of-physical-network-adapter-configurations.md)を参照してください。

    この構成で拡張可能スイッチ拡張機能は、チーム内のすべてのネットワーク アダプターに公開されます。 これにより、転送拡張機能が拡張可能スイッチのドライバー スタックを構成し、チーム内の個々 のネットワーク アダプターの使用を管理するの。 たとえば、拡張機能では、個々 のアダプターに送信されるパケットを転送することによって、over、チーム分散フェールオーバー (LBFO) のソリューション ロードのサポートを提供できます。 このような拡張機能と呼ばれる、*チーミング プロバイダー*します。 プロバイダーのチーミングの詳細については、[プロバイダーの拡張機能のチーミング](teaming-provider-extensions.md)を参照してください。

    OID を処理することによって要求[OID\_スイッチ\_NIC\_要求](https://msdn.microsoft.com/library/windows/hardware/hh598266)、ハードウェア オフロードのアダプターのチームの構成に参加プロバイダーをチーミングすることができます。 たとえば、拡張機能は OID の独自の OID 要求を生成できます\_スイッチ\_NIC\_ハードウェアのパラメーターを持つ物理アダプターを構成する要求の負荷を軽減します。

    詳細を処理する方法について、 [OID\_スイッチ\_NIC\_要求](https://msdn.microsoft.com/library/windows/hardware/hh598266)OID の要求を参照してください[物理ネットワーク アダプターへの OID 要求の転送](forwarding-oid-requests-to-physical-network-adapters.md)します。

    **注**フィルター ドライバーの拡張機能の OID 要求を生成できます[OID\_スイッチ\_NIC\_要求](https://msdn.microsoft.com/library/windows/hardware/hh598266)拡張可能なにバインドされている任意の物理アダプターにプライベートの Oid を発行するには外部ネットワーク アダプターを切り替えます。

**注**スタックを使用して要求を再開する[ **NdisFRestartFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff562611)拡張可能スイッチの OID 要求が保留中は完了しません。 このため、スタックの再起動を待機している拡張機能は、実行中の OID 要求を完了する必要があります。

拡張可能スイッチ OID 要求の管理パスの詳細については、[Hyper-v 拡張可能スイッチ コントロール パスの OID 要求](hyper-v-extensible-switch-control-path-for-oid-requests.md)を参照してください。









