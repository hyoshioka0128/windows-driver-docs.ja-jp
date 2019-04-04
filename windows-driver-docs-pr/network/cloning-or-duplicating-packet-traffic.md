---
title: トラフィックのパケットの複製
description: トラフィックのパケットの複製
ms.assetid: 6BAE348D-B5BA-4B74-8D9B-79B146427D8C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc9a33e7534e39642cf8f1b4968015836df93c59
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535947"
---
# <a name="cloning-packet-traffic"></a>トラフィックのパケットの複製


このトピックでは、拡張可能な HYPER-V の拡張機能の複製、または重複するパケットを切り替えるし、拡張可能スイッチのデータ パスに挿入するについて説明します。 パケットの複製の詳細については、[複製 NET\_バッファー\_リスト構造](cloned-net-buffer-list-structures.md)を参照してください。

**注**このページは、情報とでのダイアグラムに精通していることを前提としています。 [Hyper-v 拡張可能スイッチの概要](overview-of-the-hyper-v-extensible-switch.md)と[ハイブリッド転送](hybrid-forwarding.md)します。

**注**、拡張可能スイッチのインターフェイスで NDIS フィルター ドライバーと呼ばれる*拡張可能スイッチの拡張機能*と呼ばれるドライバー スタック、*ドライバー スタックの拡張可能スイッチ*します。 拡張機能に関する詳細については、[Hyper-v 拡張可能スイッチ拡張機能](hyper-v-extensible-switch-extensions.md)を参照してください。

フィルター処理および転送拡張機能の拡張可能スイッチは、次のガイドラインに従って、拡張可能スイッチのイングレスまたはエグレス データ パスに複製されたパケットを挿入できます。

-   拡張機能に割り当てる必要があります最初、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568389)複製されたパケットの構造体。 拡張機能はパケット データを複製されたパケットに元のパケットをコピーしする必要があります。 パケットのクローンを作成する方法の詳細については、[派生 NET\_バッファー\_リスト構造](derived-net-buffer-list-structures.md)を参照してください。

-   拡張機能の割り当て後に、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568389)呼び出す必要があります、構造、 [ *AllocateNetBufferListForwardingContext* ](https://msdn.microsoft.com/library/windows/hardware/hh598134)ハンドラー関数にパケットを転送の拡張可能スイッチのコンテキストを割り当てられません。

    転送コンテキストは、パケットの帯域外の (OOB) データに存在します。 その発信元ポートと 1 つまたは複数の宛先ポートの配列など、パケットの転送情報が含まれています。

    転送コンテキストに関する詳細については、[Hyper-v 拡張可能スイッチの転送コンテキスト](hyper-v-extensible-switch-forwarding-context.md)を参照してください。

-   拡張機能は、既存のソース ポート呼び出すことによって、複製されたパケットを元のパケットからをなど、OOB データをコピーする必要があります[ *CopyNetBufferListInfo*](https://msdn.microsoft.com/library/windows/hardware/hh598136)します。 拡張機能のイングレス データ パスにパケットを挿入する場合、これも元のパケットの OOB データから宛先ポートをコピーする必要があります。

    OOB のデータをコピーするとき、拡張機能は次のガイドラインに従います。

    -   フィルター処理の拡張機能、イングレス データ パスにパケットを挿入する場合、呼び出す必要があります[ *CopyNetBufferListInfo* ](https://msdn.microsoft.com/library/windows/hardware/hh598136) NDIS と\_スイッチ\_コピー\_NBL\_情報\_フラグ\_保持\_宛先フラグが指定されていません。 これにより、元のパケットの宛先ポートを複製されたパケットにコピーされません。 このパケットは、フィルター処理の拡張機能は、イングレス データのパスに挿入、ときに宛先ポートは、基になる転送拡張機能 (ドライバー スタックで有効になっている) 場合か、拡張可能スイッチのミニポート edge パケットに追加します。

    -   呼び出す必要がありますが、フィルター処理の拡張機能エグレス データのパスにパケットを挿入する場合、 [ *CopyNetBufferListInfo* ](https://msdn.microsoft.com/library/windows/hardware/hh598136) NDIS と\_スイッチ\_コピー\_NBL\_情報\_フラグ\_保持\_宛先フラグを指定します。 これにより、元のパケットの宛先は、複製されたパケットにコピーするポート。

-   呼び出された後、パケットの宛先ポートに変更が場合、フィルター処理の拡張機能を複製、またはエグレス データのパスから取得したパケットを複製する場合[ *CopyNetBufferListInfo* ](https://msdn.microsoft.com/library/windows/hardware/hh598136)でNDIS\_スイッチ\_コピー\_NBL\_情報\_フラグ\_保持\_宛先フラグを指定します。 この手順の詳細については、[パケットの拡張可能スイッチ ソース ポート データを変更する](modifying-a-packet-s-extensible-switch-source-port-data.md)を参照してください。

-   転送拡張機能が複製またはイングレス データのパスから取得したパケットを複製する場合、パケットの受信データのパスに挿入する前に、パケットの宛先ポートを新しいを追加する必要があります。 この手順の詳細については、[を追加する拡張可能なスイッチ宛先ポート データ パケットに](adding-extensible-switch-destination-port-data-to-a-packet.md)を参照してください。

-   拡張機能の呼び出し後[ *CopyNetBufferListInfo*](https://msdn.microsoft.com/library/windows/hardware/hh598136)、元のパケットに含まれていたのと同じソース ポート情報は、パケットに割り当てられます。

    拡張機能を呼び出すことができます[ *SetNetBufferListSource* ](https://msdn.microsoft.com/library/windows/hardware/hh598300)パケットのアウト オブ バンド (OOB) データ ソースのポート情報を変更します。

    拡張機能は、特定のポートから送信されたかのように扱う場合にパケットを必要があります。 これにより、パケットに適用するには、そのポートのポリシーができます。 拡張機能の呼び出し[ *SetNetBufferListSource* ](https://msdn.microsoft.com/library/windows/hardware/hh598300)パケットの発信元ポートを変更します。

    ただし、ある可能性があります、拡張機能にパケットの送信元ポートの識別子を割り当てる必要のある状況**NDIS\_スイッチ\_既定\_ポート\_ID**します。 など、拡張機能に設定するソース ポート識別子**NDIS\_スイッチ\_既定\_ポート\_ID**でデバイスに送信されるパケットの独自のコントロール、外部ネットワークです。

-   標準の NDIS データ パスで拡張不能スイッチ OOB データでは、パケットが送信または受信で指定されているかどうかに応じて異なる値が多くの場合があります。 たとえば、 [ **NDIS\_IPSEC\_オフロード\_V2\_ヘッダー\_NET\_バッファー\_一覧\_情報** ](https://msdn.microsoft.com/library/windows/hardware/ff565812) OOB データは、送信および受信 – 固有の構造体の共用体

    拡張可能スイッチのデータ パスでは、両方と拡張機能ドライバー スタックのすべてのパケット移動は、送信し、受け取ります。 このため、拡張不能スイッチでパケットの OOB データ[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体は、送信のいずれかであるまたは期間を通じての形式の受信ドライバー スタックをフローします。

    この OOB データの形式は、拡張可能スイッチに元のパケットが到着したソースの拡張可能スイッチ ポートに依存します。 ソース ポートが外部ネットワーク アダプターに接続されている場合は、拡張不能スイッチ OOB データが受信形式になります。 他のポートでは、この OOB データは送信形式になります。

    ソース ポートの情報が格納されている、 [ **NDIS\_スイッチ\_転送\_詳細\_NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh598211)共用体のパケットの OOB データの[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。 拡張機能を使用してデータを取得する、 [ **NET\_バッファー\_一覧\_スイッチ\_転送\_詳細**](https://msdn.microsoft.com/library/windows/hardware/hh598259)マクロ。

    **注**、拡張機能のパケットのクローンを作成する場合[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造が考慮する必要が拡張不能スイッチ OOB データに追加する場合OOB データまたは変更します。 拡張機能を呼び出すことができます[ *CopyNetBufferListInfo* ](https://msdn.microsoft.com/library/windows/hardware/hh598136)ソース パケットから複製されたパケットに OOB のすべてのデータをコピーします。 この関数を OOB 送信を維持または形式が表示されるパケットにデータをコピーします。



-   拡張機能は、パケットを複製、複製されたパケット データは、ローカルにありますまたは*信頼*HYPER-V 親パーティションの親のオペレーティング システムのメモリ。 このメモリは、子パーティションでアクセスできません。 そのためと見なされます「安全」同期されていない更新プログラムからによってそのパーティションで実行されるゲスト オペレーティング システム。

    元のパケットを複製すると、拡張機能を取得する必要があります、 [ **NDIS\_スイッチ\_転送\_詳細\_NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh598211)共用体を使用して、複製されたパケットの[ **NET\_バッファー\_一覧\_スイッチ\_転送\_詳細**](https://msdn.microsoft.com/library/windows/hardware/hh598259)マクロ。 拡張機能を設定する必要があります、 **IsPacketDataSafe**メンバーを TRUE にします。 これは、信頼されているメモリ内のすべてのパケット データがあることを指定します。

フィルター処理および転送拡張機能は、イングレスまたはエグレス データ パスに複製されたパケットを挿入する次のガイドラインに従う必要があります。

-   拡張機能を呼び出す必要があります[ **NdisFSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff562616)イングレス データのパスに複製されたパケットを挿入します。 拡張機能を設定する必要があります、 *SendFlags*パラメーター拡張可能スイッチの適切なフラグ設定を使用します。 これらの詳細については、フラグの設定を参照してください[HYPER-V 拡張可能スイッチの送信と受信フラグ](hyper-v-extensible-switch-send-and-receive-flags.md)します。

    NDIS が、拡張機能を呼び出すときに[ *FilterSendNetBufferListsComplete* ](https://msdn.microsoft.com/library/windows/hardware/ff549967) 、複製されたパケットの送信要求を完了する関数を拡張機能を呼び出す必要があります[ *FreeNetBufferListForwardingContext* ](https://msdn.microsoft.com/library/windows/hardware/hh598153)を割り当てられた転送のコンテキストを解放します。 拡張機能を解放または再利用する前にこれにする必要があります、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568389)パケットの構造体。

    **注**拡張機能は、エグレス データのパスから取得したパケットのパケット データやソース ポートを変更する場合に、イングレス データのパスの複製されたパケットを挿入する必要があります。 パケットの宛先ポートが維持されない場合は、イングレス データ パスに複製されたパケットを挿入、ことも必要があります。



-   拡張機能を呼び出す必要があります[ **NdisFIndicateReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff561820)エグレス データのパスに複製されたパケットを挿入します。 拡張機能を設定する必要があります、 *ReceiveFlags*パラメーター拡張可能スイッチの適切なフラグ設定を使用します。

    NDIS が、拡張機能を呼び出すときに[ *FilterReturnNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff549964) 、複製されたパケットの受信要求を完了する関数を拡張機能を呼び出す必要があります[ *FreeNetBufferListForwardingContext* ](https://msdn.microsoft.com/library/windows/hardware/hh598153)解放または再利用する前に、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568389)用の構造、パケットです。

    **注**転送拡張機能を呼び出す前に[ **NdisFIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff561820)、複製されたパケットの宛先ポートを決定し、パケットにこのデータを追加する必要がありますがOOB データ。



-   拡張機能のパケットのクローンを作成する場合[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568389)構造体には、元のパケットの所有権を保持する必要があります**NET\_バッファー\_一覧**複製されたパケットを送信または要求を受信するまでの構造が完了します。 拡張機能を使用する必要があります、 **ParentNetBufferList** 、複製されたパケットのメンバー **NET\_バッファー\_一覧**にリンクする元のパケット構造**NET\_バッファー\_一覧**構造体。

    **注**で NDIS 6.30 (Windows Server 2012)、拡張機能を使用できる、 **ParentNetBufferList**が元のパケットにリンクするメンバーは、これを行うには必要ありません。 拡張機能を使用する必要が NDIS 6.40 (Windows Server 2012 R2) 以降では、 **ParentNetBufferList**元のパケットにリンクするメンバー。

    複製されたパケットの送信または受信要求が完了した、拡張機能の送信を完了または元のパケットの要求を受信する必要があります。

    **注**場合は、拡張機能には、パケットが複製[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568389)構造体後に、元のパケットの要求を受信または送信を完了できます。複製されました。

-   拡張機能は、パケットを複製、送信を完了にしたり、その複製はすぐに元のパケットの要求を受信できます。

出口データ パス内のパケットを転送先またはフィルター処理拡張機能に取得した場合、拡張機能のパケット データを変更またはソース ポートを変更した場合、このデータ パス内のパケットの複製バージョンを挿入できません。 ただし、拡張機能では、受信データのパスにこれらのパケットを挿入できます。 これにより、パケットを転送し、拡張可能スイッチのデータ パスで正しくフィルター処理できます。

**注**フィルター拡張機能は、のみ、パケットの宛先ポートが維持されない場合、イングレス データ パスに複製されたパケットを挿入できます。

たとえば、複数の宛先ポートでのパケットは、拡張可能スイッチのエグレス データ パスで取得したことを想定しています。 1 つの宛先ポートには、データのカプセル化などの特別な処理が必要な場合、転送先またはフィルター処理の拡張機能は次の手順でこれを処理します。

1.  特別な処理が必要なポートへのパケット配信を除外します。 拡張機能は設定によって、 **IsExcluded**の宛先ポートのメンバー [ **NDIS\_スイッチ\_ポート\_先**](https://msdn.microsoft.com/library/windows/hardware/hh598224)いずれかの値構造体。 この手順の詳細については、[拡張可能スイッチの宛先ポートへのパケット配送の除外](excluding-packet-delivery-to-extensible-switch-destination-ports.md)を参照してください。

2.  元のパケットを複製し、パケット データの必要な処理を実行します。

    **注**フィルター拡張機能は、複製されたパケットの宛先ポートを追加する必要があります。 このデータは、転送拡張機能または拡張可能スイッチのミニポート エッジによって後で追加されます。

3.  エグレス データ パス上の元のパケットを呼び出すことによって転送[ **NdisMIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff563598)します。

4.  イングレス データ パスの複製されたパケットを呼び出して、挿入[ **NdisFSendNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff562616)します。

拡張可能スイッチのイングレスおよびエグレス データ パスの詳細については、[Hyper-v 拡張可能スイッチ データ パス](hyper-v-extensible-switch-data-path.md)を参照してください。

**注**パケット トラフィックを複製できません拡張機能をキャプチャします。 ただし、パケットのトラフィックを発生することです。 詳細については、[パケットの発信トラフィック](originating-packet-traffic.md)を参照してください。











