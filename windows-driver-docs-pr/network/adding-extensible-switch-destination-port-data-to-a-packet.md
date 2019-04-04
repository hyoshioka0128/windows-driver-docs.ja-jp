---
title: パケットへの拡張可能スイッチ宛先ポート データの追加
description: パケットへの拡張可能スイッチ宛先ポート データの追加
ms.assetid: C921D9F8-B6FB-4B53-8CC5-CC941720FF37
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6dbf7ac44ad9e67212714e8edb367809facc01f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571743"
---
# <a name="adding-extensible-switch-destination-port-data-to-a-packet"></a>パケットへの拡張可能スイッチ宛先ポート データの追加


このトピックでは、転送拡張機能、HYPER-V 拡張可能スイッチでパケットの 1 つまたは複数の宛先ポートへの配信を指定する方法について説明します。 これらの拡張機能は、拡張可能スイッチの外部ネットワーク アダプターにバインドされている個々 の物理ネットワーク アダプターにパケットを転送できます。

**注**だけで、転送拡張機能またはスイッチ自体は、拡張可能スイッチのポートまたは個々 のネットワーク アダプターにパケットを転送できます。



次の図には、NDIS 6.40 (Windows Server 2012 R2) と後で拡張可能スイッチ ドライバー スタックを通じたパケット トラフィックのデータ パスが表示されます。 どちらの図では、拡張可能スイッチ ポートに接続されているネットワーク アダプターとの間にパケット トラフィックのデータ パスも表示されます。

![ndis 6.40 の更新された拡張可能スイッチ ポートに接続されているネットワーク アダプターとの間にパケット トラフィック用のデータ パスを示すフローチャート](images/vswitchteam2-ndis640.png)

次の図では、NDIS 6.30 (Windows Server 2012) の拡張可能スイッチ ドライバー スタックを通じたパケット トラフィックのデータ パスが表示されます。

![拡張可能スイッチ ポートに接続されているネットワーク アダプターとの間にパケット トラフィック用のデータ パスを示すフローチャート](images/vswitchteam2.png)

各拡張可能スイッチの宛先ポートがで指定された、 [ **NDIS\_切り替える\_ポート\_先**](https://msdn.microsoft.com/library/windows/hardware/hh598224)内の要素、 [ **NDIS\_スイッチ\_転送\_先\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh598210)構造体。 この配列は、の帯域外 (OOB) コンテキストのパケットの転送に含まれている[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。 このコンテキストの詳細については、[Hyper-v 拡張可能スイッチの転送コンテキスト](hyper-v-extensible-switch-forwarding-context.md)を参照してください。

転送拡張機能がバインドされ、拡張可能スイッチのドライバー スタックで有効になって場合、は、パケットが、NVGRE パケットでない限り、拡張可能スイッチのイングレス データ パスから取得したすべてのパケットの宛先ポートを判断する責任を負います。 このデータ パスの詳細については、[Hyper-v 拡張可能スイッチのデータ パスの概要](overview-of-the-hyper-v-extensible-switch-data-path.md)を参照してください。 NVGRE パケットの詳細については、[ハイブリッド転送](hybrid-forwarding.md)を参照してください。

**注**転送拡張機能をドライバー スタックで有効になっている、またはバインドされていない場合、拡張可能スイッチは、イングレス データのパスから取得するパケットの宛先ポートを決定します。



イングレス データ パス取得したパケットの宛先ポートと判断した場合、転送拡張機能は次のガイドラインに従う必要があります。

-   拡張機能を初期化する必要があります、 [ **NDIS\_スイッチ\_ポート\_先**](https://msdn.microsoft.com/library/windows/hardware/hh598224)内で構造体、 [ **NDIS\_スイッチ\_転送\_先\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh598210)対象のポートの情報を含む構造体。

    宛先ポートが外部ネットワーク アダプターに接続されていない場合、拡張機能を設定する必要があります、 **NicIndex**のメンバー、 [ **NDIS\_スイッチ\_ポート\_移行先**](https://msdn.microsoft.com/library/windows/hardware/hh598224)構造体を**NDIS\_スイッチ\_既定\_NIC\_インデックス**します。

    接続先ポートが拡張可能スイッチの外部ネットワーク アダプターに接続されている場合、拡張機能への送信要求を転送するように、基になる物理ネットワーク アダプターのインデックスを指定できます。 拡張機能は設定によって、 **NicIndex**メンバーを 0 以外の NDIS\_スイッチ\_NIC\_外部ネットワーク アダプターにバインドされている変換先のネットワーク アダプターのインデックス値。

    詳細については、[物理ネットワーク アダプターにパケットを転送](forwarding-packets-to-physical-network-adapters.md)を参照してください。

-   拡張機能は、アクティブなネットワーク アダプターの接続があるこれらのポートに対してのみ、パケットの OOB データに宛先ポートを追加する必要があります。 拡張機能が転送した場合、 [OID\_スイッチ\_NIC\_切断](https://msdn.microsoft.com/library/windows/hardware/hh598265)要求、切断されたネットワーク アダプターに関連付けられている接続先ポートを追加する必要があります。

-   パフォーマンスを向上させる、拡張機能はのみパケット配信の有効なポートの送信先を追加する必要があります。 この場合、拡張機能を設定する必要があります、 **IsExcluded**の宛先ポートのメンバー [ **NDIS\_スイッチ\_ポート\_先**](https://msdn.microsoft.com/library/windows/hardware/hh598224)構造体を FALSE にします。

-   802.1 q を保持する前に、パケット内の仮想ローカル エリア ネットワーク (VLAN) のデータに配信されます、ポート、拡張機能セット、 **PreserveVLAN**メンバーを TRUE にします。

    802.1 q を削除する前に、パケット内の仮想ローカル エリア ネットワーク (VLAN) のデータに配信されます、ポート、拡張機能セット、 **PreserveVLAN**メンバーを FALSE にします。

-   802.1 q を保持する前にパケットの優先順位のデータに配信されます、ポート、拡張機能セット、 **PreservePriority**メンバーを TRUE にします。

    802.1 q を削除する前にパケットの優先順位のデータが配信されるポートに、拡張機能セット、 **PreservePriority**メンバーを FALSE にします。

-   転送拡張機能は、パケットの複数の宛先ポートを追加する場合は、次の手順に従う必要があります。

    1.  拡張機能には、パケットの最初にアクセスする[ **NDIS\_スイッチ\_転送\_詳細\_NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh598211)構造体を使用して、 [ **NET\_バッファー\_一覧\_スイッチ\_転送\_詳細**](https://msdn.microsoft.com/library/windows/hardware/hh598259)マクロ。 次に、拡張機能、読み取り、 **NumAvailableDestinations**先ポートの配列で使用できる未使用の宛先ポート要素の数を決定するメンバー。 呼び出す必要がありますが、拡張機能では、複数の宛先ポート、配列で使用可能な必要がある場合、 [ *GrowNetBufferListDestinations* ](https://msdn.microsoft.com/library/windows/hardware/hh598158)関数で追加の宛先ポートの容量を割り当てる、配列。

        拡張機能を呼び出すと[ *GrowNetBufferListDestinations*](https://msdn.microsoft.com/library/windows/hardware/hh598158)、設定、 *NumberOfNewDestinations*パラメーターに追加する新しい変換先のポートの数をパケットです。

        また、拡張機能、設定、 *NetBufferLists*パケットへのポインターにパラメーター [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。

        **注**配列内で使用できる変換先のポートがある場合、拡張機能が呼び出す必要がありますいない[ *GrowNetBufferListDestinations*](https://msdn.microsoft.com/library/windows/hardware/hh598158)します。

    2.  場合、 [ *GrowNetBufferListDestinations* ](https://msdn.microsoft.com/library/windows/hardware/hh598158)関数が正常に取得、追加の宛先ポートでのコピー先の配列の末尾に追加されて、 [ **NDIS\_スイッチ\_転送\_先\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh598210)構造体。 この構造体へのポインターが返される、*宛先*パラメーター。

        **注**場合、 [ *GrowNetBufferListDestinations* ](https://msdn.microsoft.com/library/windows/hardware/hh598158)関数は、宛先ポートの要求の数を割り当てることができません、NDIS を返します\_状態\_リソース。

    3.  拡張機能が新しい送信先ポート要素を指定します、 [ **NDIS\_スイッチ\_転送\_先\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh598210)構造体。 拡張機能の初期化として新しい各接続先ポート、 [ **NDIS\_スイッチ\_ポート\_先**](https://msdn.microsoft.com/library/windows/hardware/hh598224)構造体。

        拡張機能の初期化を開始位置として、配列に新しい宛先ポート、 **NumDestinations**オフセット。 **NumDestinations**のメンバーである、 [ **NDIS\_スイッチ\_転送\_先\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh598210)構造体。

    4.  呼び出す必要がありますが、拡張機能には、宛先ポート要素の追加または変更が終了したら、 [ *UpdateNetBufferListDestinations* ](https://msdn.microsoft.com/library/windows/hardware/hh598303)変更をコミットします。

-   拡張機能は、パケットの 1 つの宛先ポートを追加する場合は、次の手順に従う必要があります。

    1.  拡張機能が拡張機能が割り当てたでパケットの宛先ポート情報を初期化します[ **NDIS\_スイッチ\_ポート\_先**](https://msdn.microsoft.com/library/windows/hardware/hh598224)構造体.

    2.  拡張機能の呼び出し[ *AddNetBufferListDestination* ](https://msdn.microsoft.com/library/windows/hardware/hh598133)への変更をコミットする、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)パケットの構造体。 拡張機能のアドレスを渡す、 [ **NDIS\_スイッチ\_ポート\_先**](https://msdn.microsoft.com/library/windows/hardware/hh598224)構造体、*先*パラメーター。

        **注**、拡張機能は呼び出さないでください、 [ *UpdateNetBufferListDestinations* ](https://msdn.microsoft.com/library/windows/hardware/hh598303)パケットを 1 つだけの宛先ポートに変更をコミットする関数。

-   転送拡張機能を呼び出すと[ *AddNetBufferListDestination* ](https://msdn.microsoft.com/library/windows/hardware/hh598133)または[ *UpdateNetBufferListDestinations* ](https://msdn.microsoft.com/library/windows/hardware/hh598303)をコミットします宛先ポートの変更、拡張可能スイッチのインターフェイスは拡張可能スイッチ ポートの要素で指定されている削除されない、 [ **NDIS\_切り替える\_転送\_先\_配列**](https://msdn.microsoft.com/library/windows/hardware/hh598210)構造体。 パケットが送信または受信後は、操作が完了したら、インターフェイスが必要がある場合は、ポートを削除する無料。

    **注**宛先ポートが削除された機能とのみにすることはできません転送拡張機能が転送コンテキストに宛先ポートの変更をコミットした後、 **IsExcluded**の宛先ポートのメンバー [**NDIS\_スイッチ\_ポート\_先**](https://msdn.microsoft.com/library/windows/hardware/hh598224)構造を変更することができます。 詳細については、[拡張可能スイッチの宛先ポートへのパケット配送の除外](excluding-packet-delivery-to-extensible-switch-destination-ports.md)を参照してください。

-   転送拡張機能のオブジェクト識別子 (OID) のセットの要求の処理を同期する必要があります[OID\_スイッチ\_NIC\_切断](https://msdn.microsoft.com/library/windows/hardware/hh598265)の宛先ポートを追加するそのコードで、切断されたネットワーク アダプター。

    場合、転送拡張機能の[ *FilterOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff549954)が呼び出されると、 [OID\_スイッチ\_NIC\_切断](https://msdn.microsoft.com/library/windows/hardware/hh598265)要求拡張機能は、次のいずれかで実行できます。

    -   拡張機能が呼び出された場合[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)この OID 要求を転送する必要がありますいない指定する必要がポート切断されたネットワーク アダプターを使用したパケットの宛先ポートとして。

        **注**パケットの宛先ポートのみが切断されたネットワーク アダプターを使用した 1 つである場合は、拡張機能によってパケットが破棄する必要があります。

    -   拡張機能は、NDIS を返すことができます\_状態\_保留要求を非同期的に完了します。 これにより、切断されたネットワーク アダプターを使用したパケットの宛先ポートとしてポートを追加する拡張機能です。 また、拡張機能を呼び出す、 [ *AddNetBufferListDestination* ](https://msdn.microsoft.com/library/windows/hardware/hh598133)または[ *UpdateNetBufferListDestinations* ](https://msdn.microsoft.com/library/windows/hardware/hh598303)完全なパケットの宛先ポートの追加。

        拡張機能は可能性がありますが破棄する前に、ポートに転送する必要があるパケットのようにします。

        **注**、拡張機能は、NDIS を返す場合\_状態\_保留中、呼び出すことができますも[ *ReferenceSwitchPort* ](https://msdn.microsoft.com/library/windows/hardware/hh598295)とポートの参照カウンターをインクリメントするには切断されたネットワーク アダプター。 ただし、拡張機能は転送できませんまで OID 要求呼び出した後[ *DereferenceSwitchPort* ](https://msdn.microsoft.com/library/windows/hardware/hh598142)ポートの参照カウンターをデクリメントします。



-   宛先ポートの数が 0 の場合は、転送拡張機能を呼び出す必要があります[ **NdisMSendNetBufferListsComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563668)パケットをドロップします。 拡張機能を呼び出す必要がありますも[ *ReportFilteredNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/hh598297)に破棄されたパケットの拡張可能スイッチのインターフェイスを通知します。

    **注**転送拡張機能のリンク リストを取得する場合は[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)必要があります、イングレス データ パスから複数のパケットの構造体は、破棄されたパケットのリストを作成します。 これにより、拡張機能を呼び出すことができます[ **NdisMSendNetBufferListsComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563668)と[ *ReportFilteredNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/hh598297) 1 回だけです。



-   宛先ポートの数が 0 より大きい場合は、転送拡張機能を呼び出す必要があります[ **NdisFSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff562616)のミニポート エッジへのイングレス データ パスでパケットを転送するように、拡張可能スイッチ。

    **注**転送拡張機能のリンク リストを取得する場合は[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)必要があります、イングレス データ パスから複数のパケットの構造体は、転送されたパケットのリストを作成します。 これにより、拡張機能を呼び出すことができます[ **NdisFSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff562616)パケットのリストを転送するだけで 1 回です。 さらに、拡張機能は、ポートを 1 つの宛先を持つパケットを転送する個別の一覧を管理する必要があります。 詳細については、[Hyper-v 拡張可能スイッチの送信と受信フラグ](hyper-v-extensible-switch-send-and-receive-flags.md)を参照してください。