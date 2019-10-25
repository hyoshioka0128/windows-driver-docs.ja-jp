---
title: VMQ フィルターの設定
description: VMQ フィルターの設定
ms.assetid: d40b6806-6ba8-4073-b802-57cb886ffcfb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb9b904525c35af921aa686fe55536a2064bd103
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841950"
---
# <a name="setting-a-vmq-filter"></a>VMQ フィルターの設定


受信キューが割り当てられると、それ以降のドライバーは受信キューにフィルターを設定できます。 受信キューに割り当てられたドライバーのみが、そのキューにフィルターを設定できます。

**注**  既定の受信キュー (**NDIS\_既定\_受信\_\_キューの ID**) は常に存在するため、それまでのドライバーは常に既定のキューに受信フィルターを設定できます。 後続のドライバーは、既定のキューを所有していません。 そのため、ネットワークアダプターにバインドされているすべてのプロトコルドライバーは、既定のキューを使用できます。

 

## <a name="setting-a-filter-on-a-receive-queue"></a>受信キューでのフィルターの設定


初期の構成パラメーターセットを使用して受信キューにフィルターを設定するには、その後のドライバーが Oid を発行[\_\_フィルター\_設定\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)メソッドオブジェクト識別子 (oid) 要求です。 [**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、最初は[**ndis\_RECEIVE\_FILTER\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)構造体へのポインターが含まれています。 OID メソッド要求から正常に復帰した後、 **ndis\_oid\_要求**構造の**informationbuffer**メンバーには、ndis へのポインターが含まれています **\_\_パラメーターを受け取る\_フィルターを受け取り**ます。新しいフィルター識別子を持つ構造体。

前のドライバーは、受信キューの次のフィルター構成パラメーターを使用して、 [**NDIS\_受信\_フィルター\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)構造を初期化します。

-   NDIS\_によって指定されるフィルターの種類は[ **\_フィルター\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_receive_filter_type)の列挙値を受け取ります。

    **注**  NDIS 6.20 以降では、仮想マシンキュー (VMQ) インターフェイスでサポートされているのは**NdisReceiveFilterTypeVMQueue**フィルターの種類のみです。

     

-   キューの識別子。

-   NDIS として書式設定された1つまたは複数のフィールドのテストパラメーターは、 [ **\_フィルター\_フィールド\_パラメーター構造体\_受け取り**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)ます。 VMQ では、次のフィールドテストパラメーターが定義されています。

    -   パケットの宛先メディアアクセス制御 (MAC) アドレスは、指定された MAC アドレスと同じです。

    -   パケット内の仮想 LAN (VLAN) 識別子は、指定された VLAN 識別子と同じです。

[**NDIS\_receive\_filter\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)構造体を\_oid と共に使用して、\_[フィルター\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-parameters) oid と、oid\_\_フィルター\_設定を受け取る oid を受け取り[\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)OID をフィルター処理して、フィルターの構成パラメーターを指定します。

[**NDIS\_RECEIVE\_FILTER\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)構造体の**FieldParametersArrayElementSize** **メンバーは、の配列を定義** **します**。[**NDIS\_\_フィルター\_フィールド\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)構造体を受け取ります。 各 NDIS\_は、配列内の **\_フィルター\_フィールド\_パラメーター**構造体を受け取ることにより、ネットワークヘッダーの1つのフィールドに対するフィルターテスト条件を設定します。

NDIS の**Flags**メンバー [ **\_receive\_filter\_FIELD\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)構造体は、受信フィルターに対して実行するアクションを指定します。 次の点は**NDIS\_RECEIVE\_FILTER\_フィールド\_MAC\_ヘッダー\_VLAN\_タグなし\_または\_ゼロ**フラグに適用されます。

-   **Ndis\_\_フィルター\_フィールドを受信した場合\_MAC\_ヘッダー\_VLAN\_タグなし\_、または\_ゼロ**フラグが NDIS\_Receive の**Flags**メンバーで設定され[ **\_フィルター\_フィールド\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)構造体では、ネットワークアダプターは次のすべてのテスト条件に一致する受信パケットのみを示す必要があります。

    -   MAC アドレスが一致するパケット。

    -   VLAN タグがないか、VLAN 識別子が0のパケット。

    **NDIS\_\_フィルター\_\_フィールドを受信した場合、mac\_ヘッダー\_VLAN\_タグなし\_または\_ゼロ**フラグが設定されている場合、ネットワークアダプターは、対応する mac アドレスを持つパケットを示すことはできません。0以外の VLAN 識別子。

    **注**  hyper-v 拡張可能スイッチが MAC アドレスフィルターを設定していて、VLAN 識別子フィルターが OID で構成されていない場合は、 [\_フィルターを設定\_\_フィルターを\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)と、このスイッチによって NDIS も設定され **\_受信\_フィルター\_フィールド\_MAC\_ヘッダー\_VLAN\_タグなし\_または\_ゼロ**フラグ。

     

-   **NDIS\_が\_フィルター\_フィールドを受信する場合\_MAC\_ヘッダー\_vlan\_タグなし\_または\_ゼロ**フラグが設定されておらず、OID セットによって構成された VLAN 識別子フィルターがありません[OID\_受信\_フィルター\_設定\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)を要求した場合、ミニポートドライバーは次のいずれかの操作を行う必要があります。

    -   ミニポートドライバーで NDIS 6.20 がサポートされている場合は、oid 要求の oid 要求の失敗状態を返す必要があります。 [\_受信\_フィルター\_設定\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)です。

    -   ミニポートドライバーで ndis 6.30 以降のバージョンの NDIS がサポートされている場合は、指定した MAC アドレスフィールドを検査してフィルター処理するようにネットワークアダプターを構成する必要があります。 受信パケットに VLAN タグがある場合、ネットワークアダプターはパケットデータから VLAN タグを削除する必要があります。 ミニポートドライバーは、パケットの[**net\_buffer\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造に関連付けられている[**8021Q\_INFO\_、NDIS\_net\_buffer\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_net_buffer_list_8021q_info)に VLAN タグを配置する必要があります。

-   プロトコルドライバーによって、MAC アドレスフィルターと VLAN 識別子フィルターが Oid で設定されている場合、oid [\_受信\_フィルター\_設定\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter) oid では、 **NDIS\_receive\_filter\_フィールドは設定されません\_MAC\_ヘッダー\_VLAN\_タグなし\_、または**いずれかのフィルターフィールドにゼロフラグを\_します。 この場合、ミニポートドライバーは、指定された MAC アドレスと VLAN 識別子の両方に一致するパケットを示す必要があります。 つまり、ミニポートドライバーは、VLAN 識別子がゼロまたはタグなしのパケットで一致する MAC アドレスを持つパケットを示すことはできません。

## <a name="using-the-filter-identifier"></a>フィルター識別子の使用


NDIS では、Ndis の**Filterid**メンバーにフィルター識別子が割り当てられ、 [ **\_受信\_フィルター\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)構造が割り当てられ、oid\_の oid メソッド要求が渡さ[\_フィルター\_設定\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)基になるミニポートドライバーにフィルターを適用します。 受信キューに設定されている各フィルターには、ネットワークアダプターの一意のフィルター識別子があります。 つまり、フィルター識別子は、ネットワークアダプターが管理する別のキューでは複製されません。

今後の OID 要求では、前のドライバーで NDIS によって提供されるフィルター識別子を使用する必要があります。たとえば、フィルターパラメーターを変更したり、フィルターを解放したりすることができます。

NDIS が受信キューにフィルターを設定するための OID 要求を受信すると、フィルターパラメーターが検証されます。 NDIS によって必要なリソースとフィルター識別子が割り当てられると、基になるネットワークアダプターに OID 要求が送信されます。 ネットワークアダプターがフィルターに必要なソフトウェアおよびハードウェアリソースを正常に割り当てることができる場合、 **NDIS\_STATUS\_SUCCESS**による OID 要求を完了します。

ミニポートドライバーは、割り当てられた受信フィルターのフィルター識別子を保持する必要があります。 NDIS では、受信フィルターパラメーターを変更するため、または受信フィルターをクリアするために、後の OID 要求でフィルターのフィルター識別子を使用します。 パラメーターを変更してフィルターをクリアする方法の詳細については、「 [VM キューパラメーターの取得と更新](obtaining-and-updating-vm-queue-parameters.md)」および「 [VMQ フィルターのクリア](clearing-a-vmq-filter.md)」を参照してください。

## <a name="handling-the-filter-on-a-receive-queue"></a>受信キューでのフィルター処理


ミニポートドライバーは、次の方法でフィルターに基づいてネットワークアダプターをプログラムします。

-   パケットをキューに割り当てるには、特定のフィルターのすべてのフィールドテストパラメーターが一致している必要があります。

-   キューに対して複数のフィルターを設定できます。

-   フィルターが成功した場合は、受信キューにパケットを割り当てる必要があります。

ネットワークアダプターは、すべてのフィールドテストの結果を論理**AND**演算と結合します。 つまり、NDIS の配列に含まれているいずれかのフィールドテストが[ **\_フィルター\_フィールドを受信**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)した場合\_パラメーター構造が失敗した場合、ネットワークパケットが指定されたフィルター条件を満たしていない\_ます。

ネットワークアダプターは、受信したパケットをこれらのフィルター条件に対してテストするときに、テスト条件が指定されていないパケット内のすべてのフィールドを無視する必要があります。

## <a name="receiving-packets-from-a-receive-queue"></a>受信キューからのパケットの受信


ミニポートドライバーが\_OID を受信した後[\_フィルター\_キュー\_割り当て\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-allocation-complete)要求を完了し、キューに設定されたフィルターがある場合、キューは*実行中*の状態になります。 キューがこの状態にある間、ミニポートドライバーはキューのパケットを示すことができます。 キューの状態の詳細については、「[キューの状態と操作](queue-states-and-operations.md)」を参照してください。

ミニポートドライバーが Oid を受信し[\_\_フィルター\_\_\_キューに対する完全な](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-allocation-complete)oid 要求を受信したが、キューにフィルターが設定されていない場合、ミニポートドライバーは受信を示すことができません。そのキューのパケット。 この場合、ミニポートドライバーが Oid を受け取ると、キューに対してフィルター oid 要求[\_フィルター\_設定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)し、oid 要求を完了する前に、そのキューのパケットを示すことができます\_\_フィルターを受信します。 Oid を処理している間に、ミニポートドライバーが OID を処理している間にキューのパケットを示している\_\_フィルター\_OID 要求\_フィルターを設定した場合、ミニポートドライバーは、\_の受信\_フィルター\_設定された OID を完了する必要があり\_**NDIS\_ステータス\_成功**リターンコードを持つ要求をフィルター処理します。

 

 





