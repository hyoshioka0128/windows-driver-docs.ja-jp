---
title: OID_NDK_SET_STATE
description: NDIS およびそれ以降のドライバーは、set 要求として、OID_NDK_SET_STATE OID を使用して、ミニポートアダプターの NDK 機能の状態を設定します。
ms.assetid: 5BA49F42-FE37-4860-B68F-92A7F4007639
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_NDK_SET_STATE ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 017e0e4a059b37e0e9b0470366b510ea34af4650
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844106"
---
# <a name="oid_ndk_set_state"></a>OID\_NDK\_\_状態の設定


NDIS およびそれ以降のドライバーは、set 要求として OID\_NDK\_設定\_状態 OID を使用して、ミニポートアダプターの NDK 機能の状態を設定します。

NDK サービスを提供する NDIS 6.30 以降のミニポートドライバーでは、この OID がサポートされている必要があります。 それ以外の場合、この OID は省略可能です。

<a name="remarks"></a>注釈
-------

NDIS は、この OID を[**ndis\_\_oid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)の**informationbuffer**メンバーと共に発行します。これは、**ブール値**と**informationbufferlength**メンバーを指す要求構造体は sizeof (**boolean**) と等しくなります。

-   **ブール**値が**TRUE**で **\*NetworkDirect**キーワード値が0以外の場合は、ミニポートアダプターの NDK 機能を有効にする必要があります。

    ミニポートドライバーは、次の手順に従って、 **\*の NetworkDirect**キーワード値を読み取ることができます。

    1.  ミニポートドライバーが初期化されたときに[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)関数によって返された NDIS ハンドルを使用して[**NdisOpenConfigurationEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenconfigurationex)を呼び出します。 **NdisOpenConfigurationEx**の呼び出しの詳細については、「 [NDIS 6.0 ミニポートドライバーでのレジストリの読み取り](https://docs.microsoft.com/windows-hardware/drivers/network/reading-the-registry-in-an-ndis-6-0-miniport-driver)」を参照してください。

    2.  [**NdisReadConfiguration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreadconfiguration)を呼び出し、次のように渡します。

        -   *キーワード*パラメーターの "\*NetworkDirect"

        -   *ParameterType*パラメーターの**NdisParameterInteger**

-   **ブール**値が**FALSE**の場合は、ミニポートアダプターの NDK 機能を無効にする必要があります。

NDK 機能を有効または無効にするには、ミニポートドライバーの[*Miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)コールバック関数が、 [Ndk 機能の有効化と無効化](https://docs.microsoft.com/windows-hardware/drivers/network/enabling-and-disabling-ndk-functionality)に関する手順に従う必要があります。

**  NDK**対応のミニポートドライバーでは、 [**NdisMNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent)を[*miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)関数のコンテキストから呼び出すことはできません。これを行うとデッドロックが発生する可能性があるためです。 代わりに、他のコンテキストから**NdisMNetPnPEvent**を呼び出すか、作業項目をキューに置いてください。

 

NDK 対応のミニポートドライバーの[*Miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)関数は、エラーが発生しない限り、OID\_NDK\_\_設定された oid に対して、状態 **\_成功**を返す必要があります。 ドライバーは、 **NDIS\_STATUS\_PENDING**を返さないようにする必要があります。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>サポートなし</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2012</p></td>
</tr>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>NDIS 6.30 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NdisMNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent)

[**NdisQueueIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisqueueioworkitem)

[**NdisReadConfiguration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreadconfiguration)

[**NDK\_アダプター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_adapter)

[OID\_NDK\_\_状態の設定](oid-ndk-set-state.md)

 

 




