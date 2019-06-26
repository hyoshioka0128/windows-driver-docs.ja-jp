---
title: OID_GEN_NETWORK_LAYER_ADDRESSES
description: セットとして OID_GEN_NETWORK_LAYER_ADDRESSES OID ミニポート ドライバーを基になるとバインドされたインスタンスに関連付けられているネットワーク層のアドレスの一覧について複数層の他のドライバーに通知します。
ms.assetid: 4a75c2ca-1a58-462e-876a-a65cfe63441e
ms.date: 08/08/2017
keywords: -OID_GEN_NETWORK_LAYER_ADDRESSES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 09263514e2bb79c5a29b8cf58f4285f74091dae0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383667"
---
# <a name="oidgennetworklayeraddresses"></a>OID\_GEN\_ネットワーク\_レイヤー\_アドレス


OID、セットとして\_GEN\_ネットワーク\_レイヤー\_アドレス OID は、基になるミニポート ドライバーやバインドのインスタンスに関連付けられているネットワーク層のアドレスの一覧について階層型の他のドライバーに通知します。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
(省略可能)。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
任意。

<a href="" id="windows-xp"></a>Windows XP  
サポートされています。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
任意。

<a name="remarks"></a>注釈
-------

バインドのインスタンスは、呼び出し元のトランスポートへの呼び出しで設定するドライバーの間のバインド[ **NdisOpenAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisopenadapterex)します。 トランスポートは、トランスポートを使用して\_アドレスと TA\_アドレス構造を基になるミニポート ドライバーおよびその他の通知がネットワーク層のアドレスの一覧のドライバーを階層化します。 ミニポート ドライバーやその他の階層型のドライバーを使用して、互換性のあるネットワーク\_アドレス\_一覧とネットワーク\_アドレス構造体、バインドされたインターフェイスのネットワーク層のアドレスの一覧を設定する次のように定義します。

```C++
typedef struct _NETWORK_ADDRESS_LIST {
  LONG  AddressCount; 
  USHORT  AddressType; 
  NETWORK_ADDRESS  Address[1]; 
} NETWORK_ADDRESS_LIST, *PNETWORK_ADDRESS_LIST;
```

この構造体のメンバーには、次の情報が含まれます。

<a href="" id="addresscount"></a>**AddressCount**  
配列内に表示されているネットワーク層のアドレスの数を指定します、**アドレス**メンバー。

<a href="" id="addresstype"></a>**AddressType**  
この OID を送信するプロトコルの種類を指定します。 このメンバーは有効な場合、 **AddressCount**メンバーが 0 に設定されます。 **AddressCount**メンバー ミニポート ドライバーまたはバインドされたインターフェイス上のネットワーク層のアドレスの一覧を消去するその他の複数層のドライバーに通知する 0 に設定されます。 プロトコルには、次の値のいずれかを指定できます。

<a href="" id="ndis-protocol-id-default"></a>NDIS\_プロトコル\_ID\_既定  
既定のプロトコル

<a href="" id="ndis-protocol-id-tcp-ip"></a>NDIS\_プロトコル\_ID\_TCP\_IP  
TCP/IP プロトコル

<a href="" id="ndis-protocol-id-ipx"></a>NDIS\_プロトコル\_ID\_IPX  
NetWare IPX プロトコル

<a href="" id="ndis-protocol-id-nbf"></a>NDIS\_プロトコル\_ID\_NBF  
NetBIOS プロトコル

<a href="" id="address"></a>**アドレス**  
ネットワークの種類のネットワーク層のアドレスの配列\_アドレス。 **AddressCount**メンバーは、この配列内の要素の数を指定します。

```C++
typedef struct _NETWORK_ADDRESS {
  USHORT  AddressLength; 
  USHORT  AddressType; 
  UCHAR   Address[1]; 
} NETWORK_ADDRESS, *PNETWORK_ADDRESS;
```

この構造体のメンバーには、次の情報が含まれます。

<a href="" id="addresslength"></a>**AddressLength**  
このネットワーク層のアドレスのバイト単位のサイズを指定します。 **アドレス**メンバーには、このアドレスを指定するバイトの配列が含まれています。

<a href="" id="addresstype"></a>**AddressType**  
この OID とこのネットワーク層のアドレスを送信するプロトコルの種類を指定します。 このメンバーは有効な場合、 **AddressCount**ネットワーク内のメンバー\_アドレス\_リスト構造が 0 以外の値に設定されます。 **AddressCount**ネットワーク内のメンバー\_アドレス\_一覧は、ミニポート ドライバーまたはバインドされたインターフェイス上のネットワーク層のアドレスのリストを変更するその他の複数層のドライバーに通知する 0 以外の値に設定されます。 プロトコルの種類は、上記の一覧で定義されます。

<a href="" id="address"></a>**アドレス**  
このネットワーク層のアドレスを指定するバイトの配列。 **AddressLength**メンバーは、この配列内のバイト数を指定します。

トランスポートが呼び出すことができます、 [ **NdisOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisoidrequest)関数を渡すことができます、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)OID で塗りつぶされている構造\_GEN\_ネットワーク\_レイヤー\_アドレス コード。 この呼び出しでは、そのインスタンスに関連付けられているアドレスが変更されたバインドのインスタンスに通知します。 この呼び出しで、トランスポートも渡す、バインドされたインスタンスで、 *NdisBindingHandle*パラメーター。 バインドされたインスタンスが、トランスポートと基になるミニポート ドライバーまたはその他の複数層のドライバーの間のバインディング設定です。 この呼び出しで、トランスポートを入力する必要があります、 **InformationBuffer**の NDIS メンバー\_OID\_トランスポートへのポインターを要求\_アドレス構造体。 トランスポート\_アドレスがネットワークに対応\_アドレス\_構造体を一覧表示し、ネットワーク層のアドレスの一覧を含める必要があります。

トランスポートが基になるミニポート ドライバーに中間のドライバーを使用して住所を渡すとします。 中間のドライバーには、アドレスも必要とする場合、基になるミニポート ドライバーに渡す前にメモがかかります。 基になるミニポート ドライバー、古いドライバーでは特に、NDIS のステータス値を返すことができます\_状態\_いない\_サポートされているか、NDIS\_状態\_成功します。 基になるミニポート ドライバーでは、トランスポートに対するバックアップ操作の状態を伝達します。 中間ドライバーでは、アドレスの通知を受信し続ける必要があります、その中間のドライバーが NDIS に状態を変更する必要があります必要がある場合\_状態\_成功します。トランスポートが NDIS を解釈場合がありますそれ以外の場合、\_状態\_いない\_基になるミニポート ドライバーをトランスポートが追加のアドレスを発行する必要がないことを示す値を更新するように、サポートします。 場合 NDIS\_状態\_成功が返される、基になるドライバーのアドレスの追加と削除を含む、関連付けられているアドレスの変更の通知を続行する義務のあるトランスポート。

プロトコルを設定できる、 **AddressCount**トランスポートのメンバー\_ミニポート ドライバーまたはバインドされたインターフェイス上のネットワーク層のアドレスの一覧を消去するその他の複数層のドライバーに通知する、0 のアドレス。 場合**AddressCount** 0 に設定されている、 **AddressType**ネットワーク内のメンバー\_アドレス\_リストが有効では、 **AddressType**内のメンバーネットワーク\_構造体のアドレスが無効です。 これに対して、プロトコルを設定できます**AddressCount**ミニポート ドライバーまたはバインドされたインターフェイス上のネットワーク層のアドレスのリストを変更するその他の複数層のドライバーに通知する 0 以外の値。 この場合、 **AddressType**ネットワーク内のメンバー\_アドレス\_リストが無効です、 **AddressType**ネットワーク内のメンバー\_アドレス構造体が無効です。

<a name="requirements"></a>必要条件
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


[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisoidrequest)

[**NdisOpenAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisopenadapterex)

 

 




