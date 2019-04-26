---
title: OID_SWITCH_NIC_REQUEST
description: OID_SWITCH_NIC_REQUEST のオブジェクト識別子 (OID) メソッド要求は、カプセル化し、HYPER-V 拡張可能スイッチの外部ネットワーク アダプターに OID 要求を転送に使用されます。
ms.assetid: 7EF4D950-D18E-400A-B1DD-39768A16E4C4
ms.date: 08/08/2017
keywords: -OID_SWITCH_NIC_REQUEST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: dce1228aa7cbbdb554536ed635b8eb69f09f15b5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353226"
---
# <a name="oidswitchnicrequest"></a>OID\_スイッチ\_NIC\_要求


OID のオブジェクト識別子 (OID) メソッド要求\_切り替える\_NIC\_要求を使用してカプセル化し、HYPER-V 拡張可能スイッチの外部ネットワーク アダプターに OID 要求を転送します。 これにより、外部ネットワーク アダプターにバインドされている基になる物理ネットワーク アダプターのドライバーへの配信をカプセル化された OID 要求できます。

この OID 要求は、拡張可能スイッチ ポートに接続されている他のネットワーク アダプターに発行された OID 要求をカプセル化にも使用されます。 この場合、カプセル化された OID 要求は、拡張機能によって検査の拡張可能スイッチ ドライバー スタックを介して転送されます。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_スイッチ\_NIC\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/hh598214)構造体。 この構造体には、OID 要求の転送情報を指定します。 この構造体は、元のポインターも含まれています。 **NDIS\_OID\_要求**が転送される OID 要求の構造体。

<a name="remarks"></a>注釈
-------

HYPER-V 拡張可能スイッチのインターフェイスに着信した OID 要求をカプセル化して、拡張可能スイッチ コントロール パスに転送するためにします。 これらの OID 要求を以下に示します。

-   ハードウェアでは、インターネット プロトコル セキュリティ (IPsec)、仮想マシン キュー (VMQ) およびシングル ルート I/O 仮想化 (SR-IOV) の要求を含めて、OID の要求をオフロードします。 これらの OID 要求は、上位のプロトコルまたは HYPER-V 親パーティションの管理オペレーティング システムで実行されているフィルター ドライバーによって発行されます。

    拡張可能スイッチのプロトコルのエッジが内での OID 要求をカプセル化、拡張可能スイッチのインターフェイスでこれらの OID 要求が届いたら、 [ **NDIS\_切り替える\_NIC\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/hh598214)構造体。 プロトコルのエッジは、次のように、この構造体のメンバーを設定します。

    -   **DestinationPortId**と**DestinationNicIndex**メンバーが外部ネットワーク アダプターの対応する値に設定されます。

    -   OID 要求が、HYPER-V 子パーティションから送られた場合、 **SourcePortId**と**SourceNicIndex**メンバーで使用されるポートとネットワーク アダプターの対応する値に設定されて、パーティション。 それ以外の場合、 **SourcePortId**と**SourceNicIndex**メンバーが 0 に設定します。

        **注**転送または OID 要求をリダイレクトする場合、拡張機能がこれらのメンバーの値を保持する必要があります。



    -   **OidRequest**メンバーへのポインターに設定されます、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)カプセル化された OID 要求の構造体。

    プロトコルのエッジが、OID を発行\_切り替える\_NIC\_外部ネットワーク アダプターに拡張可能スイッチ コントロールのパスをカプセル化された OID 要求を転送するように要求します。

    基になる転送拡張機能は、外部ネットワーク アダプターにバインドされている物理ネットワーク アダプターをカプセル化されたハードウェア オフロード OID 要求をリダイレクトできます。 たとえば、拡張機能は、外部ネットワーク アダプターにバインドされている、拡張可能スイッチ チームからの物理ネットワーク アダプターをサポートする場合に転送できます OID\_切り替える\_NIC\_内の物理アダプターに要求ハードウェアをサポートする負荷分散フェールオーバー (LBFO) チームの負荷を軽減します。 この手順の詳細については、次を参照してください。[を管理するハードウェア オフロード OID 要求を物理ネットワーク アダプター](https://msdn.microsoft.com/library/windows/hardware/hh598194)します。

    拡張可能スイッチ チームの詳細については、次を参照してください。[型の物理ネットワーク アダプターの構成](https://msdn.microsoft.com/library/windows/hardware/hh582274)します。

-   など、マルチキャストの OID 要求[OID\_802\_3\_追加\_マルチキャスト\_アドレス](oid-802-3-add-multicast-address.md)と[OID\_802\_3\_削除\_マルチキャスト\_アドレス](oid-802-3-delete-multicast-address.md)します。 これらの OID 要求は、上位のプロトコルと、管理オペレーティング システムまたは HYPER-V 子パーティションのゲスト オペレーティング システムのいずれかで実行されているフィルター ドライバーによって発行されます。

    拡張可能スイッチのプロトコルのエッジが内での OID 要求をカプセル化、拡張可能スイッチのインターフェイスでこれらの OID 要求が届いたら、 [ **NDIS\_切り替える\_NIC\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/hh598214)構造体。 またプロトコル エッジを設定、 **SourcePortId**と**SourceNicIndex**メンバーを OID 要求が発行されたポートとネットワーク アダプターの対応する値。 プロトコルのエッジが、OID を発行\_切り替える\_NIC\_基になる拡張機能によって検査の拡張可能スイッチ コントロールのパスをカプセル化された OID 要求を転送するように要求します。

    **注**プロトコル エッジがここでは、設定、 **DestinationPortId**と**DestinationNicIndex**メンバーをゼロにします。 これは、カプセル化された OID 要求がコントロール パスの拡張機能に配信されることを指定します。

    基になる転送拡張機能カプセル化された OID 要求を検査できメンバーが指定したマルチキャスト アドレス情報を保持できます。 たとえば、拡張機能は、拡張可能スイッチ ポートに転送するマルチキャスト パケットが発生した場合にこの情報を必要があります。

    詳細については、次を参照してください。 [Hyper-v 子パーティションから OID の要求を転送](https://msdn.microsoft.com/library/windows/hardware/hh598150)します。

転送拡張機能は、OID を発行できますも\_スイッチ\_NIC\_要求を転送するために、外部ネットワーク アダプターにバインドされている物理ネットワーク アダプターに OID 要求をカプセル化します。 これにより、独自の OID 要求を発信または外部ネットワーク アダプターにバインドされている物理ネットワーク アダプターに既存の OID 要求をリダイレクトする拡張機能です。 これを行うには、拡張機能は以下の手順を実行する必要があります。

1.  拡張機能の呼び出し[ *ReferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598294)を変換先の物理ネットワーク アダプターのインデックスの参照カウンターをインクリメントします。 これにより、エントリの中に、その参照カウンターが 0 以外の場合、拡張可能スイッチのインターフェイスは物理ネットワーク アダプターの接続が削除されません。

    **注**の参照カウンターが 0 以外の場合、拡張可能スイッチのインターフェイスは物理ネットワーク アダプターの接続を切断でした。 詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチのポートおよびネットワーク アダプターの状態](https://msdn.microsoft.com/library/windows/hardware/hh598182)します。

2.  拡張機能は、初期化することにより、OID 要求をカプセル化します、 [ **NDIS\_スイッチ\_NIC\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/hh598214)次のように構造体。

    -   **DestinationPortId**メンバーは、外部ネットワーク アダプターが接続されている拡張可能スイッチ ポートの識別子を設定する必要があります。
    -   **DestinationNicIndex**メンバーは、基になる物理ネットワーク アダプターの 0 以外のインデックス値に設定する必要があります。
    -   HYPER-V 子パーティションでは、代わりに、拡張機能が発生した場合、 **SourcePortId**と**SourceNicIndex**メンバーで使用されるポートとネットワーク アダプターの対応する値に設定されますパーティション。 それ以外の場合、 **SourcePortId**と**SourceNicIndex**メンバーが 0 に設定します。

        たとえば、子パーティション用にハードウェア オフロード リソース拡張機能を管理している場合は、設定があります、 **SourcePortId**と**SourceNicIndex**のどのカプセル化されたパーティションを指定するメンバーハードウェア オフロード OID 要求です。

    -   **OidRequest**メンバーが初期化されたへのポインターを設定する必要があります[ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)カプセル化された OID 要求の構造.

3.  拡張機能の呼び出し[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830) OID 要求を指定したコピー先の拡張可能スイッチ ポートとネットワーク アダプターに転送するようにします。

4.  NDIS を呼び出すと、 [ *FilterOidRequestComplete* ](https://msdn.microsoft.com/library/windows/hardware/ff549956)関数では、拡張機能の呼び出し[ *DereferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598141)をオフにします変換先の物理ネットワーク アダプターのインデックスの参照カウンターです。

### <a name="return-status-codes"></a>リターン状態コード

拡張可能スイッチの基になるミニポート edge OID の OID のクエリ要求が完了すると\_切り替える\_NIC\_要求し、次のステータス コードの 1 つを返します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状態コード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NDIS_STATUS_SUCCESS</p></td>
<td><p>OID 要求は正常に完了しました。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_<em>Xxx</em></p></td>
<td><p>他の理由から、要求が失敗しました。</p></td>
</tr>
</tbody>
</table>



<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>NDIS 6.30 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


****
[**NDIS\_状態\_を示す値**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[**NDIS\_スイッチ\_NIC\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/hh598214)