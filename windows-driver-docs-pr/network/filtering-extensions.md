---
title: フィルター拡張機能
description: フィルター拡張機能
ms.assetid: EDE50213-DFA0-4D8B-9E15-12AED8FDE5CA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07b6142848ac3041b641d769632f63de12f4e0db
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837751"
---
# <a name="filtering-extensions"></a>フィルター拡張機能


Hyper-v 拡張可能スイッチフィルター拡張では、拡張可能なスイッチのデータパスにパケットを検査、変更、および挿入できます。 拡張可能なスイッチポートとスイッチポリシー設定に基づいて、拡張機能はパケットをドロップするか、1つまたは複数の宛先ポートへの配信を除外することができます。

フィルター拡張機能は、受信データパスで拡張機能をキャプチャした後、送信データパスの転送拡張機能の後に呼び出されます。 これらのデータパスの詳細については、「 [Hyper-v 拡張可能スイッチのデータパス](hyper-v-extensible-switch-data-path.md)」を参照してください。

フィルター拡張機能は、受信データパスで取得されたパケットに対して次の操作を実行できます。

-   パケットトラフィックをフィルター処理し、拡張可能スイッチを介してパケットを送信するためのカスタムポートまたはスイッチポリシーを適用します。 フィルター拡張機能によって、受信データパス内のパケットがフィルター処理されるときに、パケットの送信元ポートおよびネットワークアダプター接続のみに基づいてフィルター規則を適用できます。 この情報は、パケットの[**net\_buffer\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造の帯域外 (OOB) データに格納されます。この情報は、 [**net\_buffer\_list**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-switch-forwarding-detail)\_\_の転送\_詳細を使用して取得できます。マクロ.

    **メモ** 受信データパスで取得したパケットに宛先ポートが含まれていません。 宛先ポートに基づくパケットのフィルター処理は、送信データパスで取得したパケットに対してのみ実行できます。

    カスタムポリシーは、独立系ソフトウェアベンダー (ISV) によって定義されます。 このポリシーの種類のプロパティ設定は、Hyper-v WMI 管理レイヤーを使用して管理されます。 フィルター拡張機能は、これらのプロパティ設定を使用して構成されています。オブジェクト識別子 (OID) 要求[oid\_スイッチ\_ポート\_プロパティ\_UPDATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-update)および[oid\_switch\_プロパティ\_を更新](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-update)します。

    カスタム拡張ポートまたはスイッチポリシーの詳細については、「 [Hyper-v 拡張可能スイッチポリシーの管理](managing-hyper-v-extensible-switch-extensibility-policies.md)」を参照してください。

    **メモ** 拡張可能なスイッチを介したパケット配信に対して標準ポートポリシーを適用できるのは、転送拡張機能のみです。

-   新しいパケット、変更されたパケット、または複製されたパケットを受信データパスに挿入します。

    詳細については、「 [Hyper-v 拡張可能スイッチの送信と受信の操作](hyper-v-extensible-switch-send-and-receive-operations.md)」を参照してください。

フィルター拡張機能では、送信データパスで取得されたパケットに対して次の操作を実行できます。

-   パケットトラフィックをフィルター処理し、拡張可能スイッチを介してパケットを送信するためのカスタムポートまたはスイッチポリシーを適用します。 フィルター拡張機能によって、送信データパス内のパケットがフィルター処理されるときに、パケットの送信元または送信先のポートに基づいてフィルタリング規則を適用できます。 宛先ポートデータは、パケットの[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造の OOB データに格納されます。 拡張機能は、 [*GetNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations)関数を呼び出すことによってこの情報を取得します。

-   1つまたは複数の拡張可能なスイッチの接続先ポートへのパケットの配信を除外します。 これにより、フィルター拡張機能によって、拡張可能なスイッチポートへのパケットの配信が除外されます。

    拡張可能なスイッチポートへのパケット配信を除外する方法の詳細については、「[拡張可能スイッチの接続先ポートへのパケット配信](excluding-packet-delivery-to-extensible-switch-destination-ports.md)の除外」を参照してください。

-   送信データパスのパケットの転送を延期することで、1つまたは複数の宛先ポートへのトラフィックフローを管理します。

    たとえば、サービス品質 (QoS) 機能をサポートするフィルター拡張機能では、 [**NdisFSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists)をすぐに呼び出して、優先順位の高い値を指定してパケットを転送することができます。 トラフィックフローによっては、拡張機能が優先順位の低いパケットを後で転送することが必要になる場合があります。

-   パケットデータを変更します。 フィルター拡張機能でパケット内のデータを変更する必要がある場合は、まずポートの宛先を保持せずにパケットを複製する必要があります。 次に、拡張機能は、変更されたパケットを受信データパスに挿入する必要があります。 これにより、基になる拡張機能で、変更されたパケットにポリシーを適用し、転送拡張機能がポートの宛先を追加できるようになります。

    詳細については、「[パケットトラフィックの複製](cloning-or-duplicating-packet-traffic.md)」を参照してください。

フィルター拡張機能では、OID 要求と NDIS ステータスを調べるだけでなく、次の操作を実行できます。

-   では、拡張可能なスイッチポートまたはネットワークアダプター接続の作成は、該当する拡張可能なスイッチの Oid に対して\_受け入れられていないデータ\_ステータス\_返されます。 たとえば、フィルター拡張機能は、ステータス\_データを返すことによってポート作成要求を拒否できます。これは、ドライバーが oid 設定要求を受信したときに\_受け入れられません\_、 [\_スイッチ\_ポート\_作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)します。

    **メモ** フィルター拡張機能では、ポートやネットワークアダプター接続は作成または削除されません。 拡張可能スイッチのプロトコルエッジは、ポートまたはネットワークアダプター接続の作成または削除について、基になるフィルタードライバーに通知する Oid を発行します。 詳細については、「 [Hyper-v 拡張可能スイッチポートとネットワークアダプターの状態](hyper-v-extensible-switch-port-and-network-adapter-states.md)」を参照してください。

-   は、拡張可能なスイッチまたはポートポリシーの追加または更新を拒否します。これは、該当する拡張可能なスイッチの Oid に対して\_受け入れられていないデータ\_ステータス\_返されます。 たとえば、フィルター拡張機能は、ステータス\_データを返すことによってポートポリシーの追加を拒否することができます。これは、拡張機能が oid セット要求[oid\_スイッチ\_ポート\_プロパティを受け取るときに\_受け入れられない\_\_を追加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-add)します。

    拡張可能なスイッチポリシーの詳細については、「 [Hyper-v 拡張可能スイッチポリシーの管理](managing-hyper-v-extensible-switch-extensibility-policies.md)」を参照してください。

フィルター拡張機能には、次の要件があります。

-   フィルター拡張機能は、拡張可能なスイッチインターフェイスをサポートする NDIS フィルタードライバーとして開発する必要があります。

    フィルタードライバーの詳細については、「 [NDIS フィルタードライバー](ndis-filter-drivers2.md)」を参照してください。

    フィルター拡張機能を記述する方法の詳細については、「 [Hyper-v 拡張可能スイッチ拡張機能の記述](writing-hyper-v-extensible-switch-extensions.md)」を参照してください。

    **メモ** Windows Filtering Platform (WFP) では、インボックス拡張スイッチフィルター拡張機能 (変更可能) が用意されています。 この拡張機能により、WFP フィルターまたはコールアウトドライバーは、Hyper-v 拡張可能スイッチのデータパスに沿ってパケットを傍受できます。 これにより、フィルターやコールアウトドライバーは、WFP の管理機能とシステム機能を使用して、パケット検査や変更を行うことができます。 WFP の概要については、「 [Windows Filtering Platform](porting-packet-processing-drivers-and-apps-to-wfp.md)」を参照してください。

-   フィルター拡張機能の INF ファイルでは、変更フィルタードライバーとしてドライバーをインストールする必要があります。 拡張可能なスイッチドライバースタックには、NDIS 監視フィルタードライバーをインストールできません。

    フィルタードライバーの変更の詳細については、「[フィルタードライバーの種類](types-of-filter-drivers.md)」を参照してください。

    フィルタードライバーを変更するための INF の要件の詳細については、「[変更フィルタードライバーの Inf ファイルの構成](configuring-an-inf-file-for-a-modifying-filter-driver.md)」を参照してください。

-   フィルタードライバーの INF ファイルの**Filterclass**値は、 **ms\_スイッチ\_フィルター**に設定する必要があります。 詳細については、「 [Hyper-v 拡張可能スイッチ拡張機能の INF 要件](inf-requirements-for-hyper-v-extensions.md)」を参照してください。

-   拡張可能なスイッチのインスタンスごとに、ドライバースタックで任意の数のフィルター拡張機能をバインドし、有効にすることができます。 既定では、複数のフィルター拡張機能は、インストールされた日時に基づいて並べ替えられます。 たとえば、複数のフィルター拡張機能は、拡張可能なスイッチドライバースタックに含まれており、最近インストールされた拡張機能は、スタック内の他のフィルター拡張機能の上に階層化されています。

    拡張可能なスイッチインスタンスでバインドされ、有効になった後は、拡張可能なスイッチドライバースタックのフィルター拡張機能のレイヤーを並べ替えることができます。 詳細については、「 [Hyper-v 拡張可能スイッチ拡張機能の順序変更](reordering-hyper-v-extensibility-switch-extensions.md)」を参照してください。