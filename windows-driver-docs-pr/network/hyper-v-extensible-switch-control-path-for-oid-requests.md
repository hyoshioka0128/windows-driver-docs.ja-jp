---
title: OID 要求用の Hyper-V 拡張可能スイッチ制御パス
description: OID 要求用の Hyper-V 拡張可能スイッチ制御パス
ms.assetid: 69ABBD54-F794-4A0A-8F50-915CA1EDD95C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7c17da023d8e4373fe6b21dbc55c60c649e8e0a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383719"
---
# <a name="hyper-v-extensible-switch-control-path-for-oid-requests"></a>OID 要求用の Hyper-V 拡張可能スイッチ制御パス


このトピックでは、HYPER-V 拡張可能スイッチのオブジェクト識別子 (OID) 要求の間で移動するコントロールのパスについて説明します。

次の図には、OID 要求 NDIS 6.40 (Windows Server 2012 R2) と後で拡張可能スイッチ コントロール パスが表示されます。

![ndis 6.40 の vswitch oid コントロール パスの図](images/vswitch-oid-controlpath-ndis640.png)

次の図では、NDIS 6.30 (Windows Server 2012) の OID 要求の拡張可能スイッチ コントロール パスが表示されます。

![ndis 6.30 の vswitch oid コントロール パスの図](images/vswitch-oid-controlpath.png)

**注**  、拡張可能スイッチのインターフェイスで NDIS フィルター ドライバーと呼ばれる*拡張可能スイッチの拡張機能*と呼ばれるドライバー スタック、*拡張可能スイッチ ドライバー スタック*.

 

転送拡張機能、フィルター処理などの拡張可能スイッチの拡張機能は、許可またはポートやスイッチのポリシーに基づくトラフィックのパケットを拒否しています。 これらの拡張ポリシーの決定を適用するためには、これらの拡張機能は、以下を実行できる必要があります。

-   新しいまたは更新された構成と拡張可能スイッチ、ポート、およびそのネットワーク アダプターの接続の状態に関する拡張可能スイッチのインターフェイスから必要な情報を受信します。

-   スイッチまたはポートのポリシーの新規または更新されたプロパティの拡張可能スイッチのインターフェイスから必要な情報を受信します。

-   拡張可能スイッチ、ポート、およびそのネットワーク アダプターの接続の現在の構成を取得する拡張可能スイッチのインターフェイスへの OID 要求を発行します。

拡張可能スイッチのインターフェイスは、そのコンポーネントの構成の変更に関する拡張機能を基になるを通知し、拡張可能な発行することによってポリシーのパラメーターは OID セット要求を切り替えます。 これらの変更について、基になる拡張機能を通知する拡張可能スイッチのプロトコルの端でこれらの要求が発行されます。 これらの OID 要求は、拡張可能スイッチの基になるミニポート エッジに拡張可能スイッチのドライバー スタックを移動します。

拡張可能スイッチのミニポート エッジは OID 要求を完了します。 ただし、いくつか拡張可能スイッチの OID 要求基になる拡張機能は、通知を拒否するには、OID 要求を失敗ことができます。 たとえば、作成される新しいポートに関する拡張機能を拡張可能スイッチのプロトコルのエッジに通知をするときに要求を発行、OID セットの[OID\_切り替える\_ポート\_作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)です。 基になるフィルター処理または転送拡張機能は、状態が、OID 要求を実行してポートの作成を拒否できます\_データ\_いない\_受理します。 この手順の詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチ構成の変更に関する OID 要求を受信](receiving-oid-requests-about-hyper-v-extensible-switch-configuration-changes.md)します。

**注**  拡張機能が拡張可能スイッチの OID 要求を拒否しては場合は、要求が完了したときにステータスを監視にする必要があります。 拡張機能は、拡張可能スイッチ コントロール パスの拡張機能を基になるか、拡張可能スイッチのインターフェイスに OID 要求が拒否されたかどうかを決定するこれを行う必要があります。

 

**注**  スタックを使用して要求を再開する[ **NdisFRestartFilter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfrestartfilter)拡張可能スイッチの OID 要求が保留中は完了しません。 このため、スタックの再起動を待機している拡張機能は、実行中の OID 要求を完了する必要があります。

 

拡張可能スイッチの OID 要求のほとんどは、拡張可能スイッチのインターフェイスでのみ実行できます。 ただし、拡張可能スイッチ、ポート、およびそのネットワーク アダプターの接続の構成に関する情報を取得する拡張機能によって一部の拡張可能スイッチ OID 要求を発行できます。 詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチの構成を照会](querying-the-hyper-v-extensible-switch-configuration.md)します。

 

 





