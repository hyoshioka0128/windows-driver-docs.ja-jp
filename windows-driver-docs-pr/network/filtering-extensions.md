---
title: フィルター拡張機能
description: フィルター拡張機能
ms.assetid: EDE50213-DFA0-4D8B-9E15-12AED8FDE5CA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6474dd4ba003fd7ae3b991793c58b266e23c6eb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353343"
---
# <a name="filtering-extensions"></a>フィルター拡張機能


拡張機能をフィルター処理、HYPER-V 拡張可能スイッチは、検査、変更、および拡張可能スイッチのデータ パスにパケットを挿入できます。 拡張可能スイッチ ポートとスイッチのポリシー設定に基づいて、拡張機能はパケットをドロップするか、1 つまたは複数の宛先ポートへの配信を除外します。

出口データ パスの転送拡張機能の前後のイングレス データ パスの拡張機能を取得した後、フィルター拡張機能が呼び出されます。 これらのデータ パスの詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチのデータ パス](hyper-v-extensible-switch-data-path.md)します。

フィルター拡張機能は、イングレス データ パス取得したパケットを使用して、次を実行できます。

-   パケット トラフィックをフィルター処理しカスタム ポートを適用するか、拡張可能スイッチを通じてパケット配信ポリシーを切り替えます。 フィルター処理の拡張機能では、イングレス データ パス内のパケット フィルター処理、ときに、パケットが元のソース ポートおよびネットワーク アダプター接続のみに基づいてフィルタ リング規則を適用できます。 パケットのアウト オブ バンド (OOB) データにこの情報が格納されている[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体し、を使用して取得できます、 [ **NET\_バッファー\_一覧\_スイッチ\_転送\_詳細**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-switch-forwarding-detail)マクロ。

    **注**イングレス データ パス取得したパケットには宛先ポートが含まれていません。 パケットの宛先ポートに基づいてフィルター処理は、送信データ パス取得したパケットにのみ実行できます。

    カスタム ポリシーは、独立系ソフトウェア ベンダー (ISV) によって定義されます。 このポリシーの種類のプロパティの設定は、HYPER-V の WMI 管理層によって管理されます。 これらのオブジェクト識別子 (OID) 要求プロパティの設定とフィルター処理の拡張機能が構成されている[OID\_スイッチ\_ポート\_プロパティ\_UPDATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-update)と[OID\_スイッチ\_プロパティ\_UPDATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-update)します。

    カスタムの拡張可能なポートやスイッチ ポリシーの詳細については、次を参照してください。[を管理する Hyper-v 拡張可能なスイッチ ポリシー](managing-hyper-v-extensible-switch-extensibility-policies.md)します。

    **注**拡張可能スイッチを介してパケット配信のための標準ポート ポリシーを適用できる転送拡張機能のみです。

-   イングレス データのパスには、新しい、変更、または複製されたパケットを挿入します。

    詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチの送信と受信操作](hyper-v-extensible-switch-send-and-receive-operations.md)します。

フィルター拡張機能は、送信データ パス取得したパケットを使用して、次を実行できます。

-   パケット トラフィックをフィルター処理しカスタム ポートを適用するか、拡張可能スイッチを通じてパケット配信ポリシーを切り替えます。 フィルター処理の拡張機能には、エグレス データ パス内のパケットがフィルター処理、ときに、パケットの送信元または送信先のポートに基づくフィルタ リング規則を適用できます。 OOB データのパケットの宛先ポート データが格納されている[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体。 拡張機能は、呼び出すことでこの情報を取得、 [ *GetNetBufferListDestinations* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations)関数。

-   パケットの 1 つまたは複数の拡張可能スイッチの宛先ポートへの配信を除外します。 これにより、拡張可能スイッチのポートへのパケットの配信を除外するフィルターの拡張機能です。

    拡張可能スイッチ ポートにパケット配信を除外する方法の詳細については、次を参照してください。[拡張可能スイッチの宛先ポートへのパケット配送の除外](excluding-packet-delivery-to-extensible-switch-destination-ports.md)します。

-   延期エグレス データ パスのパケットを転送することで、1 つまたは複数の宛先ポートへのトラフィック フローを管理します。

    直ちに呼び出すサービス (QoS) 機能の品質をサポートする拡張機能をフィルター処理するなど、 [ **NdisFSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfsendnetbufferlists)より高度で指定されたパケットを転送するには優先度値。 によって、トラフィック フローは後で、低い優先度値を持つパケットを転送するように、拡張機能もかまいません。

-   パケット データを変更します。 フィルター処理の拡張機能は、データ パケットを変更する必要があります、ポートの送信先を維持せず、パケットを最初に複製にする必要があります。 次に、拡張機能では、イングレス データのパスに変更されたパケットを挿入する必要があります。 これにより、変更されたパケットのポリシーを適用する基になる拡張機能と、転送拡張機能は、ポートの送信先を追加できます。

    詳細については、次を参照してください。[パケット トラフィックの複製](cloning-or-duplicating-packet-traffic.md)します。

OID 要求と NDIS 状態インジケーターを検査、だけでなくフィルター拡張機能は、次の操作を行うことができます。

-   状態を返すことによって、拡張可能スイッチ ポートまたはネットワーク アダプターの接続の作成を拒否\_データ\_いない\_適用可能な拡張可能スイッチの Oid を承諾します。 状態を返すことによって、フィルター処理の拡張機能がポートの作成要求を拒否するなど、\_データ\_いない\_ドライバーの OID 設定要求の受信時に合意[OID\_スイッチ\_ポート\_作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)です。

    **注**フィルター拡張機能を作成またはポートを削除またはしないでネットワーク アダプターの接続。 拡張可能スイッチのプロトコルのエッジは、作成またはポートまたはネットワーク アダプターの接続の削除について、基になるフィルター ドライバーに通知する Oid を発行します。 詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチのポートおよびネットワーク アダプターの状態](hyper-v-extensible-switch-port-and-network-adapter-states.md)します。

-   状態を返すことによって追加または拡張可能スイッチまたはポートのポリシーの更新プログラムを拒否\_データ\_いない\_適用可能な拡張可能スイッチの Oid を承諾します。 状態を返すことによって、フィルター処理の拡張機能がポート ポリシーの追加を拒否するなど、\_データ\_いない\_、拡張機能の OID 設定要求の受信時に合意[OID\_スイッチ\_ポート\_プロパティ\_追加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-add)します。

    ポリシーの拡張可能スイッチの詳細については、次を参照してください。[を管理する Hyper-v 拡張可能なスイッチ ポリシー](managing-hyper-v-extensible-switch-extensibility-policies.md)します。

フィルター拡張機能では、次の要件があります。

-   フィルター拡張機能は、拡張可能スイッチのインターフェイスをサポートする NDIS フィルター ドライバーとして開発する必要があります。

    フィルター ドライバーの詳細については、次を参照してください。 [NDIS フィルター ドライバー](ndis-filter-drivers2.md)します。

    フィルター拡張機能の記述方法の詳細については、次を参照してください。[書き込みの Hyper-v 拡張可能スイッチ拡張機能](writing-hyper-v-extensible-switch-extensions.md)します。

    **注**Windows フィルタ リング プラットフォーム (WFP) は、インボックスの拡張可能スイッチ拡張機能 (Wfplwfs.sys) をフィルター処理を提供します。 この拡張機能は、WFP フィルターまたは HYPER-V 拡張可能スイッチのデータ パスに沿ったパケットをインターセプトするコールアウト ドライバーを使用します。 これにより、フィルターまたはコールアウト ドライバー WFP 管理とシステム関数を使用してパケット検査または変更を実行します。 WFP の概要については、次を参照してください。 [Windows フィルタ リング プラットフォーム](porting-packet-processing-drivers-and-apps-to-wfp.md)します。

-   フィルター拡張機能の INF ファイルでは、変更フィルター ドライバーとドライバーをインストールする必要があります。 NDIS 監視フィルターは、拡張可能スイッチ ドライバー スタックでドライバーをインストールすることはできません。

    フィルター ドライバーを変更する方法の詳細については、次を参照してください。[型のフィルター ドライバー](types-of-filter-drivers.md)します。

    フィルター ドライバーを変更するための INF 要件の詳細については、次を参照してください。[変更フィルター ドライバーの INF ファイルを構成する](configuring-an-inf-file-for-a-modifying-filter-driver.md)します。

-   **FilterClass** INF ファイルの値は、フィルター ドライバーに設定する必要があります**ms\_切り替える\_フィルター**します。 詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチ拡張機能の要件を INF](inf-requirements-for-hyper-v-extensions.md)します。

-   任意の数のフィルター処理の拡張機能は、バインドされ、拡張可能スイッチのインスタンスごとにドライバー スタックで有効になっていることができます。 既定では、複数のフィルター処理拡張機能がインストールされているときにに基づいて並べ替えられています。 など、複数のフィルター処理拡張機能に、最近インストールされた拡張機能が、スタック内の他のフィルター処理拡張機能の上に配置を拡張可能スイッチのドライバー スタックで配置されます。

    バインドを実行し、拡張可能スイッチのインスタンスで有効になっているが後で拡張可能スイッチのドライバー スタックのフィルター処理の拡張機能のレイヤーを並べ替えることができます。 詳細については、次を参照してください。[の並べ替えの Hyper-v 拡張可能スイッチの拡張](reordering-hyper-v-extensibility-switch-extensions.md)します。