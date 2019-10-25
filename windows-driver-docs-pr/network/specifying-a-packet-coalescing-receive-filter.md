---
title: パケット結合受信フィルターの指定
description: パケット結合受信フィルターの指定
ms.assetid: 0369A63D-4CDE-448A-8472-EEEB7B859B8D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: acf4455ee98b9827555743e52a20e0ba8c3a00f1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841875"
---
# <a name="specifying-a-packet-coalescing-receive-filter"></a>パケット結合受信フィルターの指定


追加のドライバーでは、NDIS パケット合体をサポートする1つ以上の受信フィルターをミニポートドライバーに設定できます。 前のドライバーでは、\_NDIS の**MaxPacketCoalescingFilters**メンバーに指定されているミニポートドライバーが[ **\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)の構造を受け取ることができる受信フィルターの最大数を指定できます。

このプロトコルドライバーでは、ndis [ **\_バインド\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)構造体内で、NDIS [ **\_受信\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)の構造を取得する  に**注意**してください。 このフィルタードライバーは、ndis **\_RECEIVE\_filter\_CAPABILITIES**構造を取得します。これは、 [**ndis\_filter\_ATTACH\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)構造体に含まれています。

 

この後のドライバーは、\_Oid の OID メソッド要求を発行することによってミニポートドライバーにフィルターをダウンロードし、 [\_\_フィルターを設定して受信\_フィルター設定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)します。 この OID 要求の[ **\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、呼び出し元が割り当てたバッファーへのポインターが含まれています。 このバッファーは、次のものが含まれるように書式設定されます。

-   Ndis\_は、NDIS 受信フィルターのパラメーターを指定する[ **\_フィルター\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)構造を受け取ります。

    この構造体を初期化する方法の詳細については、「[受信フィルターの指定](#specifying-a-receive-filter)」を参照してください。

-   ネットワークパケットヘッダー内のフィールドのフィルターテスト条件を指定する、 [ **\_フィルター\_フィールド\_パラメーター構造を受け取る NDIS\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)の配列。

    これらの構造体を初期化する方法の詳細については、「[ヘッダーフィールドのテストを指定](#specifying-header-field-tests)する」を参照してください。

## <a name="specifying-a-receive-filter"></a>受信フィルターの指定


前のドライバーは、フィルターの構成パラメーターを使用して、 [**NDIS\_receive\_filter\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)構造体を初期化することによって、パケット合体受信フィルターを指定します。 **NDIS\_RECEIVE\_FILTER\_PARAMETERS**構造体を初期化すると、その後のドライバーは次の規則に従う必要があります。

-   **FilterType**メンバーは、 **NdisReceiveFilterTypePacketCoalescing**の TYPE 列挙値\_TYPE 列挙値を[**受け取る\_フィルターの\_を NDIS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_receive_filter_type)に設定する必要があります。

-   **Queueid**メンバーを NDIS\_既定\_受信\_キュー\_ID に設定する必要があります。

    **注**  NDIS 6.30 以降、パケット合体受信フィルターは、ネットワークアダプターの既定の受信キューでのみサポートされています。 この受信キューには、NDIS\_既定\_受信\_キュー\_ID の識別子が設定されています。

     

-   それまでのドライバーが新しい受信フィルターを作成している場合は、 **Filterid**メンバーを NDIS\_DEFAULT\_RECEIVE\_FILTER\_ID に設定する必要があります。

    **  NDIS**によって受信フィルターの oid メソッド要求が転送される前に、受信フィルターの一意のフィルター識別子 (ID) が生成されます。これにより[\_\_フィルターが\_受信](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)し、フィルターがミニポートドライバーに\_設定されます。     

-  それまでのドライバーが既存の受信フィルターを変更している場合は、 **filterid**メンバーを受信フィルターの0以外のフィルター id に設定する必要があります。 その後のドライバーは、 [ENUM\_フィルター\_列挙型の\_フィルターを受け取る oid\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)oid メソッド要求を発行するときに、受信フィルターのフィルター ID を取得します。 受信フィルターを変更する方法の詳細については、「[パケット合体受信フィルターの変更](modifying-packet-coalescing-receive-filters.md)」を参照してください。

-   [**NDIS\_受信\_フィルター\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)構造体の**FieldParametersArrayElementSize**メンバーは、**を定義**するように設定する必要が**あります。** フィールドパラメーターの配列。 配列の各要素は、受信フィルターのヘッダーフィールドテストのパラメーターを指定する、 [ **\_フィルター\_フィールド\_パラメーター構造を受け取る NDIS\_を受け取り**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)ます。

-   **Requestedfilteridbitcount**メンバーを0に設定する必要があります。

-   **MaxCoalescingDelay**は、受信フィルターに一致する最初のパケットがネットワークアダプターに保存され、結合される最大時間 (ミリ秒単位) に設定する必要があります。 フィルターに一致する最初のパケットを受信するとすぐに、ネットワークアダプターはパケットを結合し、有効期限が**MaxCoalescingDelay**メンバーの値に設定されているハードウェアタイマーを開始します。

このドライバーでは、フィールドパラメーター配列内のヘッダーフィールドテストが、関連付けられている MAC とプロトコルヘッダーがパケット内に存在する順序と同じ順序になるように並べ替える必要があります。

たとえば、前のドライバーで IP version 4 (IPv4) プロトコルフィールドのフィルターパラメーターを指定する前に、まず、MAC ヘッダープロトコルフィールド (NdisMacHeaderFieldProtocol) のフィルターパラメーターを指定する必要があります。 このように、ドライバーは、フィールドが IPv4 パケットに対して正しい EtherType 値 (0x0800) に設定されていることを確認するヘッダーフィールドテストを指定します。 テストが失敗した場合、アダプターは IPV4 プロトコルフィールドのテストを実行する必要はありません。

## <a name="specifying-header-field-tests"></a>ヘッダーフィールドのテストの指定


各受信フィルターでは、1つまたは複数のテスト条件 (*ヘッダーフィールドテスト*) を指定できます。 ネットワークアダプターは、これらのテストを実行して、受信したパケットをアダプターのハードウェア合体バッファーに結合する必要があるかどうかを判断します。 また、このドライバーでは、さまざまなメディアアクセスコントロール (MAC)、IP version 4 (IPv4)、および IP version 6 (IPv6) のヘッダーフィールドに対して個別のフィルターテストを指定できます。

ネットワークアダプターのフィルター処理を最適化するために、ヘッダーフィールドのテストは、パケットデータ内のバイトオフセット/長さの指定ではなく、標準化されたヘッダーフィールド名に基づいています。 ヘッダー/フィールド名を使用することにより、ネットワークアダプターのハードウェアまたはファームウェアは、受信したパケットに対して複数のヘッダーフィールドテストを実行する方法を最適化できます。

各受信フィルターには、 [**NDIS\_receive\_filter\_field\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)構造体によって指定された1つ以上のヘッダーフィールドテストを含めることができます。 各**NDIS\_受信\_フィルター\_フィールド\_パラメーター**構造は、 **FieldParametersArrayOffset**、 **FieldParametersArrayNumElements**、およびによって参照されるフィールドパラメーター配列の要素です。および**FieldParametersArrayElementSize**のメンバーは、 [**NDIS\_\_フィルター\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)構造体を受け取ります。

ミニポートドライバーは、oid の OID メソッド要求を処理するときに、次のガイドラインに従う必要があります。 [\_受信\_フィルター\_設定\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter):

-   **Ndis\_\_フィルター\_フィールドを受信した場合\_MAC\_ヘッダー\_VLAN\_タグなし\_、または\_ゼロ**フラグが NDIS\_Receive の**Flags**メンバーで設定され[ **\_フィルター\_フィールド\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)の構造では、ネットワークアダプターは、一致する MAC アドレスを持つ受信パケット、タグなしのパケット、または VLAN 識別子が0のパケットのみを示す必要があります。 つまり、ネットワークアダプターは、MAC アドレスが一致し、0以外の VLAN 識別子を持つパケットを示すことはできません。

-   **NDIS\_が\_フィルター\_フィールドを受信する場合\_MAC\_ヘッダー\_vlan\_タグなし\_または\_ゼロ**フラグが設定されておらず、OID セットによって構成された VLAN 識別子フィルターがありません[OID\_受信\_フィルター\_設定\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)を要求した場合、ミニポートドライバーは次のいずれかの操作を行う必要があります。

    -   ミニポートドライバーで NDIS 6.20 がサポートされている場合は、oid 要求の oid 要求の失敗状態を返す必要があります。 [\_受信\_フィルター\_設定\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)です。

    -   ミニポートドライバーで ndis 6.30 以降のバージョンの NDIS がサポートされている場合は、指定した MAC アドレスフィールドを検査してフィルター処理するようにネットワークアダプターを構成する必要があります。 受信パケットに VLAN タグがある場合、ネットワークアダプターはパケットデータから VLAN タグを削除する必要があります。 ミニポートドライバーは、パケットの[**net\_buffer\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造に関連付けられている[**8021Q\_INFO\_、NDIS\_net\_buffer\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_net_buffer_list_8021q_info)に VLAN タグを配置する必要があります。

-   前のドライバーによって、MAC アドレスフィルターと、Ndis 内の VLAN 識別子フィルターが設定されている場合、 [ **\_フィルター\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)構造を受け取ると、 **ndis\_受信\_フィルター\_フィールド\_MAC\_設定されません。\_ヘッダー\_VLAN\_のいずれかのフィルターフィールドにタグなし\_または\_ゼロ**フラグを付けます。 この場合、ミニポートドライバーは、指定された MAC アドレスと VLAN 識別子の両方に一致するパケットを示す必要があります。 つまり、ミニポートドライバーは、VLAN 識別子がゼロまたはタグなしのパケットで一致する MAC アドレスを持つパケットを示すことはできません。

 

 





