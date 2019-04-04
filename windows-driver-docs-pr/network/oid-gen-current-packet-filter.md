---
title: OID_GEN_CURRENT_PACKET_FILTER
description: クエリとして OID_GEN_CURRENT_PACKET_FILTER OID に含まれるネットワーク パケットの種類は受信ミニポート ドライバーから表示を報告します。
ms.assetid: d5a32626-caff-4708-a134-d80a845dee91
ms.date: 08/08/2017
keywords: -OID_GEN_CURRENT_PACKET_FILTER ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: b7ac4d4f4033f6f4082f9aa5e44eb189bbf99b73
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536007"
---
# <a name="oidgencurrentpacketfilter"></a>OID\_GEN\_現在\_パケット\_フィルター


クエリ、OID として\_GEN\_現在\_パケット\_フィルター OID をレポートに含まれるネットワーク パケットの種類は、ミニポート ドライバーからインジケーターを受信します。

OID、セットとして\_GEN\_現在\_パケット\_フィルター OID をプロトコルはミニポート ドライバーからインジケーターを受信ネットワーク パケットの種類を指定します。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
必須。 (「解説」を参照してください セクション)

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
必須。

<a href="" id="windows-xp"></a>Windows XP  
サポートされています。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
必須。

<a name="remarks"></a>注釈
-------

NDIS 6.0 とそれ以降のミニポート ドライバーでは、クエリが要求されていないと、セットは必須です。 NDIS は、ミニポート ドライバーにクエリを処理します。 ミニポート ドライバーでは、初期化中にパケット フィルター情報を報告します。

ミニポート ドライバーでは、システムが filter ライブラリを提供する 1 つとして、メディアの種類を報告します。 パケット フィルターは OR 演算を使用して、次の種類を範囲に結合します。

<a href="" id="ndis-packet-type-directed"></a>NDIS\_パケット\_型\_ダイレクト  
有向パケット。 有向パケット含む宛先アドレスが NIC のステーションのアドレスと一致しません

<a href="" id="ndis-packet-type-multicast"></a>NDIS\_パケット\_型\_マルチキャスト  
マルチキャスト アドレスのパケットがマルチキャスト アドレスの一覧内のアドレスに送信します。

プロトコル ドライバーは、イーサネット (802.3) を受信できるアドレスをマルチキャストまたは機能のパケットの種類を指定することでマルチキャスト パケット数。 マルチキャスト アドレスの一覧または機能のアドレスを設定すると、グループ NIC ドライバーの有効化するマルチキャスト アドレスを決定します。

<a href="" id="ndis-packet-type-all-multicast"></a>NDIS\_パケット\_型\_すべて\_マルチキャスト  
すべてのマルチキャスト アドレス パケット、マルチキャスト アドレスの一覧に列挙されたものだけでなく。

<a href="" id="ndis-packet-type-broadcast"></a>NDIS\_パケット\_型\_ブロードキャスト  
パケットをブロードキャストします。

<a href="" id="ndis-packet-type-promiscuous"></a>NDIS\_パケット\_型\_PROMISCUOUS  
VLAN のフィルタ リングが有効かどうかや、VLAN 識別子がかどうかに一致するかどうかに関係なくすべてのパケットを指定します。

<a href="" id="ndis-packet-type-all-functional"></a>NDIS\_パケット\_型\_すべて\_機能  
すべてのパケット機能アドレス、機能の現在のアドレスで使用されているだけでなく。

<a href="" id="ndis-packet-type-all-local"></a>NDIS\_パケット\_型\_すべて\_ローカル  
インストールされているプロトコルによって送信されたすべてのパケットとすべてのパケットで識別される NIC で示される、指定された*NdisBindingHandle*します。

<a href="" id="ndis-packet-type-functional"></a>NDIS\_パケット\_型\_機能  
機能のアドレスの機能の現在のアドレスに含まれるアドレスに送信されるパケット。

<a href="" id="ndis-packet-type-group"></a>NDIS\_パケット\_型\_グループ  
現在のグループ アドレスに送信されるパケット。

<a href="" id="ndis-packet-type-mac-frame"></a>NDIS\_パケット\_型\_MAC\_フレーム  
トークン リング NIC を受信する NIC ドライバーのフレームです。

<a href="" id="ndis-packet-type-smt"></a>NDIS\_パケット\_型\_SMT  
FDDI の NIC を受信する SMT パケット。

<a href="" id="ndis-packet-type-source-routing"></a>NDIS\_パケット\_型\_ソース\_ルーティング  
すべてのソース パケットをルーティングします。 プロトコル ドライバーには、このビットが設定、NDIS ライブラリはソースのルーティング仲介役として機能しようとします。

ミニポート アダプターがメディアの種類**NdisMedium802\_3**または**NdisMedium802\_5**NDIS は、マルチキャストおよび機能のアドレスと共に、パケットの受信を無効にします。呼び出し中に、 [ **NdisOpenAdapterEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563715)関数。

プロトコル ドライバーに他のすべてのメディアの種類を持つミニポート アダプターの中にいつでもパケットの受信を開始できます、 [ **NdisOpenAdapterEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563715)呼び出します。 プロトコルがする前にパケットを受信できるさらに注意してください。 **NdisOpenAdapterEx**を返します。 一般に、最善の努力は、パケット フィルタ リングとパケット フィルターが 0 の場合でも受信表示をプロトコルを処理するドライバーを準備する必要があります。

クエリの場合は、NDIS は、OR 演算子を使用して結合されるバインドのフィルターを返します。

セットに対して、指定されたパケットのフィルターには、バインディングの前のパケット フィルターが置き換えられます。 ミニポート ドライバーには、パケットの種類以前有効になっているプロトコル ドライバーには、新しいフィルターでその型を指定しない場合、プロトコル ドライバーはこの種類のパケットを受信しません。

ミニポート アダプターがメディアの種類**NdisMedium802\_3**または**NdisMedium802\_5**への応答で特定のパケットの種類のミニポート ドライバーがビットに設定されていない場合、このクエリでは、プロトコル ドライバーではその種類のパケットは受信しません。 プロトコル ドライバーがパケットの受信を無効に呼び出すことによって、その結果、 [ **NdisOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff563710)または[ **NdisCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561711)関数がゼロのフィルターを使用します。

その他のすべてのメディアの種類を持つミニポート アダプターの NDIS は、パケットの種類をチェックしません。 これらのメディアの種類は、プロトコル ドライバーが 0 のフィルターを指定することでパケットの受信を無効にできません。

ときに、ミニポート ドライバーの[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数が呼び出されると、ミニポート ドライバーのパケット フィルターを 0 に設定する必要があります。 パケット フィルターが 0 の場合に表示されるインジケーターは無効になります。 ミニポート ドライバーの後に*MiniportInitializeEx*関数が返される、OID を設定できるプロトコル ドライバー\_GEN\_現在\_パケット\_のため 0 以外の値をフィルター処理そのプロトコルで受信したパケットを示すために、ミニポート ドライバーを有効にします。

NDIS で無作為検出モードが有効な場合\_パケット\_型\_無作為検出ビットの場合でも、送信側のネットワーク ノードはないにリダイレクトするには、パケットを受信するプロトコル ドライバーが続行されます。 NDIS は、すべてのパケットが、NIC にはプロトコル ドライバーから送信します。

特定のパケット フィルターを設定する (またはそれ以降) にバインドされているその他のプロトコル ドライバーのパケット フィルターは変更しません同じ NIC などの場合は 1 つのバインドされているプロトコルは、無作為検出モードを有効、他のプロトコルがバインドされているドライバーは独自のパケット フィルターを使用して明示的に要求していないパケットを受信されません。

**ネイティブの 802.11 パケット フィルター**

ネイティブの 802.11 ミニポート ドライバーには、次の標準的なパケット フィルターの種類のみをサポートする必要があります。

-   NDIS\_パケット\_型\_ダイレクト

-   NDIS\_パケット\_型\_マルチキャスト

-   NDIS\_パケット\_型\_ブロードキャスト

-   NDIS\_パケット\_型\_PROMISCUOUS

有効な場合、これらの標準的なパケット フィルターは 802.11 データ パケットに適用できるのみです。

さらに、ネイティブ 802.11 ミニポート ドライバーでは、ネイティブ 802.11 メディアに固有では、次のパケット フィルター種類をサポートする必要があります。

<a href="" id="ndis-packet-type-802-11-raw-data"></a>NDIS\_パケット\_型\_802\_11\_RAW\_データ  
802.11 メディア アクセス制御 (MAC) プロトコル データ ユニット (MPDU) フレームの 802.11 のステーションで受信した形式のデータがすべて含まれています。 このフィルターが設定されている場合、ドライバーは MPDU フラグメントから MAC サービスのデータ ユニット (MSDU) パケットの再構成を示します前に変更されていないすべて MPDU フラグメントを示す必要があります。

MPDU フラグメントが暗号化されている場合で、前に、示された、フラグメントを解読にする必要がありますできません。 ただし、ミニポート ドライバーには、戻したおよび MSDU パケットを示す前に各 MPDU フラグメントが復号化する必要があります。

有効な場合、この種類のフィルターにのみ影響 NDIS など、他の標準のパケット フィルター\_パケット\_型\_ダイレクトまたは NDIS\_パケット\_型\_ブロードキャストします。

生の 802.11 データ パケットを指定する方法の詳細については、[Raw 802.11 パケットのことを示す](https://msdn.microsoft.com/library/windows/hardware/ff554833)を参照してください。

<a href="" id="ndis-packet-type-802-11-directed-mgmt"></a>NDIS\_パケット\_型\_802\_11\_ダイレクト\_管理  
802.11 管理パケットが送られます。 有向パケット含む宛先アドレスが NIC のステーションのアドレスと一致しません

<a href="" id="ndis-packet-type-802-11-multicast-mgmt"></a>NDIS\_パケット\_型\_802\_11\_マルチキャスト\_管理  
マルチキャスト 802.11 管理パケット、マルチキャスト アドレスの一覧内のアドレスに送信します。

<a href="" id="ndis-packet-type-802-11-all-multicast-mgmt"></a>NDIS\_パケット\_型\_802\_11\_すべて\_マルチキャスト\_管理  
すべてのマルチキャスト 802.11 管理パケット、802.11 MAC ヘッダーの宛先アドレスがマルチキャスト アドレスの一覧をかどうかに関係なく、802.11 ステーションで受信します。

<a href="" id="ndis-packet-type-802-11-broadcast-mgmt"></a>NDIS\_パケット\_型\_802\_11\_ブロードキャスト\_管理  
802.11 ステーションで受信した 802.11 の管理のパケットをブロードキャストします。

<a href="" id="ndis-packet-type-802-11-promiscuous-mgmt"></a>NDIS\_パケット\_型\_802\_11\_PROMISCUOUS\_管理  
すべて 802.11 管理によって受信されたパケット、802.11 ステーションです。

<a href="" id="ndis-packet-type-802-11-raw-mgmt"></a>NDIS\_パケット\_型\_802\_11\_RAW\_管理  
802.11 MPDU 管理、フレームのすべての 802.11 のステーションで受信した形式でデータが含まれています。 このフィルターが設定されている場合、ドライバーは MPDU フラグメントから MAC の管理プロトコル データ ユニット (MMPDU) パケットの再構成を示します前に変更されていないすべて MPDU フラグメントを示す必要があります。

有効な場合、この種類のフィルターにのみ影響 802.11 他の管理パケット フィルター、NDIS\_パケット\_型\_802\_11\_ダイレクト\_MGMT または NDIS\_パケット\_型\_802\_11\_マルチキャスト\_管理

生の 802.11 管理パケットを指定する方法の詳細については、[Raw 802.11 パケットのことを示す](https://msdn.microsoft.com/library/windows/hardware/ff554833)を参照してください。

<a href="" id="ndis-packet-type-802-11-directed-ctrl"></a>NDIS\_パケット\_型\_802\_11\_ダイレクト\_CTRL  
802.11 コントロール パケットが送られます。 有向パケット含む宛先アドレスが NIC のステーションのアドレスと一致しません

<a href="" id="ndis-packet-type-802-11-broadcast-ctrl"></a>NDIS\_パケット\_型\_802\_11\_ブロードキャスト\_CTRL  
802.11 ステーションで受信した 802.11 のコントロールのパケットをブロードキャストします。

<a href="" id="ndis-packet-type-802-11-promiscuous-ctrl"></a>NDIS\_パケット\_型\_802\_11\_PROMISCUOUS\_CTRL  
802.11 ステーションで受信したすべての 802.11 コントロール パケット。

ミニポート ドライバーが 802.11 ネットワーク モニター (NetMon) をネイティブ モードまたは拡張可能なアクセス ポイント (AP) モードで動作して場合、ドライバーは OID のセットの要求では、次のパケット フィルターを有効にする必要があります\_GEN\_現在\_パケット\_フィルター。

-   NDIS\_パケット\_型\_PROMISCUOUS

-   NDIS\_パケット\_型\_802\_11\_RAW\_データ

-   NDIS\_パケット\_型\_802\_11\_PROMISCUOUS\_管理

-   NDIS\_パケット\_型\_802\_11\_RAW\_管理

-   NDIS\_パケット\_型\_802\_11\_PROMISCUOUS\_CTRL

その他の 802.11 のネイティブ モードで動作しているさらに、NetMon NDIS を除き、これらのパケット フィルター設定を有効にしないでミニポート ドライバー\_パケット\_型\_802\_11\_PROMISCUOUS\_CTRL キー。 NetMon モードで動作していないのミニポート ドライバーには、NDIS が有効にできます必要に応じて\_パケット\_型\_802\_11\_PROMISCUOUS\_OID のセット要求を通じて CTRL\_GEN\_現在\_パケット\_フィルター。

**注**  ミニポート ドライバーが 802.11 のネイティブ モード、NetMon と OID 以外の場合に\_GEN\_現在\_パケット\_フィルターが設定されている、存在する場合、ドライバーはセットの要求を失敗しない必要がありますOID データでは、無作為検出、または未加工のフィルターの設定が有効にします。

 

NetMon と ExtAP 動作モードの詳細については、次のトピックを参照してください。

[ネットワーク モニターの操作モード](https://msdn.microsoft.com/library/windows/hardware/ff568369)

[拡張可能なアクセス ポイントの操作モード](https://msdn.microsoft.com/library/windows/hardware/ff549858)

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[*MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)

[**NdisCoOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff561711)

[**NdisOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff563710)

[**NdisOpenAdapterEx**](https://msdn.microsoft.com/library/windows/hardware/ff563715)

 

 




