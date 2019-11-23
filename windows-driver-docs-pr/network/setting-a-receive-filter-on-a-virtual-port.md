---
title: 仮想ポートでの受信フィルターの設定
description: 仮想ポートでの受信フィルターの設定
ms.assetid: F0137D59-1701-4DFC-BB30-27E477FC0706
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06d27a5486a3b0ac49b8cc53a51ac579cb19dae2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841952"
---
# <a name="setting-a-receive-filter-on-a-virtual-port"></a>仮想ポートでの受信フィルターの設定


ネットワークアダプターの NIC スイッチに仮想ポート (VPort) が作成されると、それ以降のドライバーは VPort に受信フィルターを設定できます。 VPort を作成したドライバーのみが、その VPort に受信フィルターを設定できます。

このトピックの内容は次のとおりです。

[VPort での受信フィルターの設定](#setting-a-receive-filter-on-a-vport)

[NDIS\_受信\_フィルター\_フィールド\_MAC\_ヘッダー\_VLAN\_タグなし\_または\_ゼロフラグ](#using-the-ndis_receive_filter_field_mac_header_vlan_untagged_or_zero-flag)

[フィルター識別子の使用](#using-the-filter-identifier)

[VPort での受信フィルターの処理](#handling-receive-filters-on-a-vport)

VPort の作成方法の詳細については、「[仮想ポートの作成](creating-a-virtual-port.md)」を参照してください。

**注**  既定の vport は常に存在し、明示的に作成されることはないため、後続のドライバーでは、既定の vport に受信フィルターを設定できます。 後続のドライバーは、既定の VPort を所有していません。 そのため、ネットワークアダプターにバインドされているすべてのプロトコルドライバーは、既定の VPort を使用できます。 既定の VPort には、NDIS\_既定\_VPORT\_ID の識別子値が設定されています。

 

## <a name="setting-a-receive-filter-on-a-vport"></a>VPort での受信フィルターの設定


VPort に対してフィルターを設定して構成するために、前のドライバーは、オブジェクト識別子 (OID) のメソッドの要求を[oid\_受信\_フィルター\_設定\_フィルターを設定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)します。 [**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、最初は[**ndis\_RECEIVE\_FILTER\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)構造体へのポインターが含まれています。

それまでのドライバーがこの OID メソッド要求を発行する前に、 [ **\_フィルター\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)構造体を受け取るために、NDIS を初期化\_必要があります。 ドライバーは、この構造体のメンバーを次のように設定する必要があります。

-   **FilterType**メンバーは、 [**NDIS\_RECEIVE\_FILTER\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_receive_filter_type)列挙値に設定する必要があります。

    **注**  NDIS 6.30 以降では、シングルルート i/o 仮想化 (sr-iov) インターフェイスでは**NdisReceiveFilterTypeVMQueue**フィルターの種類のみがサポートされています。

     

-   **Queueid**メンバーを NDIS\_既定\_受信\_キュー\_ID に設定する必要があります。

-   **VPortId**メンバーは、vport に関連付けられた識別子に設定する必要があります。 このドライバーは、次のいずれかの方法で VPort 識別子を取得します。

    -   Oid\_の以前の OID メソッド要求から、 [\_VPORT を作成\_\_スイッチに切り替え](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)ます。

    -   Oid\_NIC の以前の OID メソッド要求から、[列挙型\_VPORTS\_スイッチ\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vports)ます。

-   **Filterid**メンバーを NDIS\_既定\_受信\_フィルター\_ID に設定する必要があります。

    **注**  NDIS は、このメンバーに一意のフィルター識別子を割り当ててから、処理のためにミニポートドライバーに OID 要求を転送します。

     

-   [ **\_\_ndis**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)の**FieldParametersArrayOffset**、 **FieldParametersArrayNumElements**、および**FieldParametersArrayElementSize**の各メンバーは、フィルター\_パラメーター構造を受け取るように適切に設定する必要があります。これは、\_ndis の配列を定義するために適切に設定されている必要があります。これは、\_[**フィールド\_パラメーター構造を受け取る\_フィルター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters) 各 NDIS\_は、配列内の **\_フィルター\_フィールド\_パラメーター**構造体を受け取ることにより、ネットワークヘッダーの1つのフィールドに対するフィルターテスト条件を設定します。

    SR-IOV インターフェイスでは、次のフィールドテストパラメーターが定義されています。

    -   パケットの宛先メディアアクセス制御 (MAC) アドレスは、指定された MAC アドレスと同じです。

    -   パケット内の仮想 LAN (VLAN) 識別子は、指定された VLAN 識別子と同じです。

OID メソッド要求から正常に返された後、 [**ndis\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、新しいフィルター識別子を使用して[ **\_フィルター\_パラメーター構造を受け取る ndis\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)のポインターが含まれています。

## <a name="using-the-ndis_receive_filter_field_mac_header_vlan_untagged_or_zero-flag"></a>NDIS\_受信\_フィルター\_フィールド\_MAC\_ヘッダー\_VLAN\_タグなし\_または\_ゼロフラグ


NDIS の**Flags**メンバー [ **\_受信\_フィルター\_フィールド\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)構造は、受信フィルターに対して実行するアクションを指定します。 次の点は**NDIS\_RECEIVE\_FILTER\_フィールド\_MAC\_ヘッダー\_VLAN\_タグなし\_または\_ゼロ**フラグに適用されます。

-   **NDIS\_\_フィルター\_フィールドを受信した場合\_MAC\_ヘッダー\_VLAN\_タグなし\_または\_ゼロ**フラグが**フラグ**メンバーに設定されている場合、ネットワークアダプターは次のすべてのテスト条件に一致する受信パケットのみを示す必要があります。

    -   MAC アドレスが一致するパケット。

    -   VLAN タグがないか、VLAN 識別子が0のパケット。

    **NDIS\_\_フィルター\_\_フィールドを受信する場合、mac\_ヘッダー\_vlan\_タグなし\_またはゼロ**フラグが設定されている場合、ネットワークアダプターは、一致する mac アドレスと0以外の vlan 識別子を持つパケットを示すことはできません。\_

    **ただし**、仮想化スタックによって MAC アドレスフィルターが設定されていて、vlan 識別子フィルターが構成されていない場合は  \_フィルターセット要求を[設定\_\_フィルターを受信\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter) 、 **mac\_ヘッダー\_VLAN\_タグなし\_または\_ゼロフラグの\_\_、NDIS\_受信\_フィルター**を設定します。

     

-   NDIS 6.30 以降では、 **ndis\_が\_フィルター\_フィールド\_MAC\_ヘッダー\_VLAN\_タグなし\_または\_ゼロ**フラグが設定されておらず、OID によって構成された vlan 識別子フィルターが\_フィルター [\_フィルター\_設定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)されていない場合、ミニポートドライバーは次のいずれかの操作を行う必要があります。\_

    -   ミニポートドライバーは、 [OID\_受信\_フィルター\_設定\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)メソッド要求の失敗状態を返す必要があります。

    -   ミニポートドライバーは、指定された MAC アドレスフィールドを検査してフィルター処理するようにネットワークアダプターを構成する必要があります。 受信パケットに VLAN タグがある場合、ネットワークアダプターはパケットデータから VLAN タグを削除する必要があります。 ミニポートドライバーは、パケットの[**net\_buffer\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造に関連付けられている[**8021Q\_INFO\_、NDIS\_net\_buffer\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_net_buffer_list_8021q_info)に VLAN タグを配置する必要があります。

-   プロトコルドライバーによって、MAC アドレスフィルターと VLAN 識別子フィルターが[OID\_受信\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)に設定されていて、フィルター\_要求\_フィルター処理が設定されていない場合は、いずれかのフィルターフィールドに、 **mac\_ヘッダー\_VLAN\_タグなし\_または\_ゼロ**フラグが設定されません。\_\_\_\_ この場合、ミニポートドライバーは、指定された MAC アドレスと VLAN 識別子の両方に一致するパケットを示す必要があります。 つまり、ミニポートドライバーは、VLAN 識別子がゼロまたはタグなしのパケットで一致する MAC アドレスを持つパケットを示すことはできません。

## <a name="using-the-filter-identifier"></a>フィルター識別子の使用


NDIS では、\_Ndis の**Filterid**メンバーにフィルター識別子が割り当てられ、 [ **\_フィルター\_PARAMETERS 構造が受信**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)され、oid の oid メソッド要求が渡されます。これにより、\_フィルター\_、基になるミニポートドライバーに\_フィルター[が設定さ\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)ます。 VPort に設定されている各フィルターには、ネットワークアダプターの一意のフィルター識別子があります。 つまり、フィルター識別子は、ネットワークアダプターが管理する別のキューでは複製されません。

後続のドライバーは、後の OID 要求で提供されるフィルター識別子を使用して、フィルターパラメーターを変更するか、フィルターを解放する必要があります。

NDIS が VPort に対してフィルターを設定するための OID 要求を受信すると、フィルターパラメーターが検証されます。 NDIS によって必要なリソースとフィルター識別子が割り当てられると、基になるネットワークアダプターに OID 要求が送信されます。 ネットワークアダプターがフィルターに必要なソフトウェアおよびハードウェアリソースを正常に割り当てることができる場合、 **NDIS\_STATUS\_SUCCESS**による OID 要求を完了します。

ミニポートドライバーは、割り当てられた受信フィルターのフィルター識別子を保持する必要があります。 NDIS は、後の OID 要求でフィルターのフィルター識別子を使用して、受信フィルターパラメーターを変更するか、受信フィルターをクリアします。 パラメーターを変更してフィルターをクリアする方法の詳細については、「 [VM キューパラメーターの取得と更新](obtaining-and-updating-vm-queue-parameters.md)」および「 [VMQ フィルターのクリア](clearing-a-vmq-filter.md)」を参照してください。

## <a name="handling-receive-filters-on-a-vport"></a>VPort での受信フィルターの処理


ミニポートドライバーは、次の方法でフィルターに基づいてネットワークアダプターをプログラムします。

-   特定のフィルターのすべてのフィールドテストパラメーターが、VPort にパケットを割り当てるために一致している必要があります。

-   VPort には複数のフィルターを設定できます。

-   フィルターが成功した場合、パケットは VPort に割り当てられる必要があります。

ネットワークアダプターは、すべてのフィールドテストの結果を論理**AND**演算と結合します。 つまり、NDIS の配列に含まれているいずれかのフィールドテストが[ **\_フィルター\_フィールドを受信**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)した場合\_パラメーター構造が失敗した場合、ネットワークパケットが指定されたフィルター条件を満たしていない\_ます。

ネットワークアダプターは、受信したパケットをこれらのフィルター条件に対してテストするときに、指定されたテスト条件を持たないパケット内のすべてのフィールドを無視する必要があります。

 

 





