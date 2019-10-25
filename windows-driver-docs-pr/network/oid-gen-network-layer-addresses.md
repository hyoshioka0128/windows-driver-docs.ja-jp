---
title: OID_GEN_NETWORK_LAYER_ADDRESSES
description: セットとして、OID_GEN_NETWORK_LAYER_ADDRESSES OID は、バインドされたインスタンスに関連付けられているネットワーク層のアドレスの一覧について、基になるミニポートドライバーやその他の階層化されたドライバーに通知します。
ms.assetid: 4a75c2ca-1a58-462e-876a-a65cfe63441e
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_GEN_NETWORK_LAYER_ADDRESSES ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 2d49a908fc5f128d8c70f8adf30a66f159630a77
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824392"
---
# <a name="oid_gen_network_layer_addresses"></a>OID\_GEN\_ネットワーク\_レイヤーの\_アドレス


設定として、OID\_GEN\_ネットワーク\_レイヤー\_アドレス OID は、基になるミニポートドライバーおよびその他の階層化されたインスタンスに関連付けられているネットワーク層のアドレスの一覧に関する他の階層化されたドライバーに通知します。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 以降のバージョンの Windows  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 以降のミニポートドライバー  
(省略可能)。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 ミニポートドライバー  
(省略可能)。

<a href="" id="windows-xp"></a>Windows XP  
サポートされています。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 ミニポートドライバー  
(省略可能)。

<a name="remarks"></a>注釈
-------

バインドされたインスタンスとは、呼び出し元トランスポートと、 [**NdisOpenAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenadapterex)の呼び出しによって設定されたドライバーとの間のバインドです。 トランスポート\_アドレス構造と TA\_アドレス構造を使用して、ネットワーク層のアドレスの一覧について、基になるミニポートドライバーやその他の階層化されたドライバーに通知します。 ミニポートドライバーおよびその他の階層化ドライバーでは、互換性のあるネットワーク\_アドレス\_リストとネットワーク\_アドレス構造を使用して、次のように定義して、バインドされたインターフェイスのネットワーク層アドレスの一覧を設定します。

```C++
typedef struct _NETWORK_ADDRESS_LIST {
  LONG  AddressCount; 
  USHORT  AddressType; 
  NETWORK_ADDRESS  Address[1]; 
} NETWORK_ADDRESS_LIST, *PNETWORK_ADDRESS_LIST;
```

この構造体のメンバーには、次の情報が含まれています。

<a href="" id="addresscount"></a>**AddressCount**  
**アドレス**メンバーの配列に一覧表示されているネットワーク層アドレスの数を指定します。

<a href="" id="addresstype"></a>**AddressType**  
この OID を送信するプロトコルの種類を指定します。 このメンバーは、 **Addresscount**メンバーが0に設定されている場合にのみ有効です。 **Addresscount**メンバーは0に設定され、ミニポートドライバーまたはその他の層ドライバーに、バインドされたインターフェイスのネットワーク層アドレスの一覧をクリアするように通知します。 プロトコルには、次のいずれかの値を指定できます。

<a href="" id="ndis-protocol-id-default"></a>NDIS\_プロトコル\_ID\_既定値  
既定のプロトコル

<a href="" id="ndis-protocol-id-tcp-ip"></a>NDIS\_プロトコル\_ID\_TCP\_IP  
TCP/IP プロトコル

<a href="" id="ndis-protocol-id-ipx"></a>NDIS\_プロトコル\_ID\_IPX  
NetWare IPX プロトコル

<a href="" id="ndis-protocol-id-nbf"></a>NDIS\_プロトコル\_ID\_NBF  
NetBIOS プロトコル

<a href="" id="address"></a>**先**  
ネットワーク\_アドレスの種類のネットワーク層アドレスの配列。 **Addresscount**メンバーは、この配列内の要素の数を指定します。

```C++
typedef struct _NETWORK_ADDRESS {
  USHORT  AddressLength; 
  USHORT  AddressType; 
  UCHAR   Address[1]; 
} NETWORK_ADDRESS, *PNETWORK_ADDRESS;
```

この構造体のメンバーには、次の情報が含まれています。

<a href="" id="addresslength"></a>**AddressLength**  
このネットワーク層アドレスのサイズをバイト単位で指定します。 **アドレス**メンバーには、このアドレスを指定するバイトの配列が含まれます。

<a href="" id="addresstype"></a>**AddressType**  
この OID とこのネットワーク層アドレスを送信するプロトコルの種類を指定します。 このメンバーは、ネットワーク\_アドレス\_リスト構造の**Addresscount**メンバーが0以外の値に設定されている場合にのみ有効です。 ネットワーク\_アドレス\_リストの**Addresscount**メンバーは0以外の値に設定され、ミニポートドライバーまたはその他のレイヤードドライバーに、バインドされたインターフェイスのネットワーク層アドレスの一覧を変更するように通知します。 プロトコルの種類は、上記の一覧で定義されています。

<a href="" id="address"></a>**先**  
このネットワーク層アドレスを指定するバイトの配列。 **Addresslength**メンバーは、この配列内のバイト数を指定します。

トランスポートは、 [**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)関数を呼び出すことができます。また、OID\_GEN\_ネットワーク\_レイヤー\_アドレスコードに格納されている[**要求構造\_NDIS\_oid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)を渡すことができます。 この呼び出しは、バインドされたインスタンスに、そのインスタンスに関連付けられているアドレスの変更を通知します。 この呼び出しでは、トランスポートは*NdisBindingHandle*パラメーターにバインドされたインスタンスも渡します。 バインドされたインスタンスは、トランスポートと、基になるミニポートドライバーまたはその他の階層化ドライバーの間に設定されたバインドです。 この呼び出しでは、トランスポートは、トランスポート\_アドレス構造体へのポインターを使用して、NDIS\_OID\_要求の**Informationbuffer**メンバーに入力する必要があります。 トランスポート\_アドレスは、ネットワーク\_アドレス\_リスト構造に対応し、ネットワーク層アドレスの一覧が含まれている必要があります。

たとえば、トランスポートが中間ドライバーを介してアドレスを基になるミニポートドライバーに渡すとします。 中間ドライバーもアドレスを必要とする場合は、基になるミニポートドライバーに渡す前に、それらを書き留めておく必要があります。 基になるミニポートドライバー (特に古いドライバー) は、NDIS\_STATUS の状態値を返すことができます。この値はサポートされていないか、NDIS\_ステータス\_成功した\_\_ありません。 基になるミニポートドライバーによって、操作の状態がトランスポートに反映されます。 中間ドライバーがアドレス通知を引き続き受信する必要があり、必要に応じて中間ドライバーがステータスを NDIS\_STATUS\_SUCCESS に変更する必要がある場合。そうしないと、トランスポートは NDIS\_の状態を解釈することがあり\_\_サポートされていません。これは、基になるミニポートドライバーでは、トランスポートが追加のアドレスを更新する必要がないことを示しています。 NDIS\_STATUS\_SUCCESS が返された場合、アドレスの追加や削除など、関連付けられているアドレスの変更について、基になるドライバーへの通知を継続する義務があります。

プロトコルでは、トランスポート\_アドレスの**Addresscount**メンバーを0に設定することにより、バインドされたインターフェイス上のネットワーク層アドレスの一覧をクリアするようにミニポートドライバーまたはその他の層ドライバーに通知できます。 **Addresscount**が0に設定されている場合は、NETWORK\_ADDRESS\_リストの**addresstype**メンバーが有効であり、ネットワーク\_アドレス構造の**addresstype**メンバーが有効ではありません。 一方、プロトコルでは、 **Addresscount**を0以外の値に設定して、ミニポートドライバーまたはその他の層ドライバーに対して、バインドされたインターフェイスのネットワーク層アドレスの一覧を変更するように通知できます。 この場合は、NETWORK\_ADDRESS\_LIST の**addresstype**メンバーが有効ではなく、ネットワーク\_アドレス構造の**addresstype**メンバーが有効です。

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
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)

[**NdisOpenAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenadapterex)

 

 




