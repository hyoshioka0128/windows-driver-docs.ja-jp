---
title: OID_WWAN_REGISTER_STATE
description: OID_WWAN_REGISTER_STATE は、登録するネットワークプロバイダーを選択します。
ms.assetid: 564de5bf-10d9-47fe-a4c1-3409d9b2aee8
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_WWAN_REGISTER_STATE ネットワークドライバー
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: e34ea14384f170c89d0528fdd7ee0e07777a5732
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843801"
---
# <a name="oid_wwan_register_state"></a>OID\_WWAN\_\_状態の登録


OID\_WWAN\_登録\_の状態に登録するネットワークプロバイダーを選択します。

ミニポートドライバーは、セットおよびクエリ要求を非同期的に処理し、最初に NDIS\_の\_状態を返し、元の要求に対して必要な\_を示し、その後、 [**ndis\_ステータス\_WWAN\_REGISTER を送信する必要があります。** ](ndis-status-wwan-register-state.md)set 要求またはクエリ要求の完了に関係なく、登録されたネットワークプロバイダーに関する情報を提供する[**NDIS\_WWAN\_登録\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_registration_state)構造を含む\_状態状態通知。

に登録するようにネットワークプロバイダーを設定する呼び出し元は、 [**NDIS\_WWAN\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_register_state)します。これにより、適切な情報を使用して\_状態構造をミニポートドライバーに登録\_ます。

<a name="remarks"></a>注釈
-------

この OID の使用方法の詳細については、「 [WWAN 登録操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-registration-operations)」を参照してください。

ミニポートドライバーは、クエリまたはセット操作を処理するときにプロバイダーネットワークにアクセスできますが、サブスクライバー Id モジュール (SIM カード) にはアクセスできません。

MB ドライバーモデルでは、自動と手動の2つの登録方法がサポートされています。 CDMA ベースのネットワークの場合、MB ドライバーモデルでは自動登録のみがサポートされます。

手動登録をサポートしているデバイスでは、 [**wwan\_DEVICE\_caps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_device_caps)構造体の**wwancontrolcaps**メンバーを WWAN\_CTRL\_CAPS\_REG\_manual に設定する必要があります。 GSM ベースのデバイスでは手動登録がサポートされている必要があることに注意してください。

登録状態が自動の場合、ミニポートドライバーは、携帯電話テクノロジに固有の選択アルゴリズムに基づいてネットワークプロバイダーを選択するようデバイスに指示し、登録を続行する必要があります。

RegisterAction 値のセマンティクスは、次のように定義されています。

-   *Wwanregisteractionautomatic*フラグは、デバイスを自動登録モードに設定し、デバイスが最適なプロバイダーネットワークを選択できるようにミニポートドライバーに指示するために、MB サービスによって使用されます。 ミニポートドライバーは、 **ProviderId**パラメーターを無視する必要があります。 この設定は、MB サービスによって明示的に変更されるまで、無線状態 (オン/オフ) とデバイスの電源サイクルの間で固定されています。

-   *Wwanregisteractionmanual*フラグは、 **ProviderId**パラメーターで識別されるプロバイダーネットワークに登録するようにミニポートドライバーに指示するために、MB サービスによって使用されます。 **Providerid**の値は、表示されているプロバイダーの1つである、WWAN\_プロバイダーのデータ構造の**providerid**メンバーからのものである必要があります。 この設定は、MB サービスによって明示的に変更されるまで、無線状態 (オン/オフ) とデバイスの電源サイクルの間で固定されています。

-   デバイスが現在プロバイダーに登録されている場合でも、異なる RegisterAction 値の間での変更は許可されます。 自動登録モードと手動登録モードを切り替える前にデバイスの登録を解除する必要がある場合、ミニポートドライバーでは、新しい登録モードに設定する前に、デバイスが登録解除に設定されていることを確認する必要があります。

-   *手動*登録モードと*自動*登録モードは、ネットワークの選択モードにのみ影響します。 オプションがオンになっている場合は、選択したネットワークに MB デバイスが登録を試みる必要があります。

### <a name="windows-10-version-1903"></a>Windows 10 バージョン 1903

この OID の新しいリビジョン3は、Windows 10 バージョン1903以降でサポートされています。 この拡張機能を使用すると、ホストはミニポートドライバーから優先無線アクセステクノロジ (飴) を照会できます。 

推奨される RAT を制御するために、ホストは、 [**WWAN_SET_REGISTER_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_set_register_state)構造体の**WWANDATACLASS**メンバーの WWAN_DATA_CLASS 値を表すビットマスクを設定します。 このメンバーは、接続に適したデータアクセステクノロジを表します。 このフィールドが**WWAN_DATA_CLASS_NONE**に設定されている場合、モデムはこのパラメーターに対してアクションを実行しません。

ホストは、現在優先されているデータクラスをミニポートドライバーから照会することもできます。 ミニポートドライバーは、 [**WWAN_REGISTRATION_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_registration_state)構造体の**preferreddataclasses**フィールドを使用して、現在モデムで設定されている優先データアクセステクノロジを報告します。

5G data クラスのサポートの詳細については、「 [MB 5G データクラスのサポート](mb-5g-data-class-support.md)」を参照してください。

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
<td><p>Windows 7 以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_設定\_登録\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_register_state)

[**NDIS\_ステータス\_WWAN\_登録\_状態**](ndis-status-wwan-register-state.md)

[WWAN 登録操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-registration-operations)

 

 




