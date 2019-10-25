---
title: OID_GEN_RECEIVE_SCALE_PARAMETERS
description: クエリとして、NDIS およびそれ以降のドライバーは OID_GEN_RECEIVE_SCALE_PARAMETERS OID を使用して、NIC の現在の RECEIVE side scaling (RSS) パラメーターを照会できます。
ms.assetid: a54190f7-0d2e-4f85-84c2-05fc9ec4994a
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_GEN_RECEIVE_SCALE_PARAMETERS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: d1a045daf09cf3cf5804aa12871f29b83871335a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844605"
---
# <a name="oid_gen_receive_scale_parameters"></a>OID\_GEN\_\_の\_パラメーターの受信


クエリとして、NDIS およびそれ以降のドライバーでは、OID\_GEN\_受信\_スケール\_パラメーター OID を使用して、NIC の現在の RECEIVE side scaling (RSS) パラメーターを照会できます。 NDIS は、現在の RSS パラメーターを定義する[**ndis\_RECEIVE\_SCALE\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_parameters)構造体を返します。

セットとして、NDIS およびそれ以降のドライバーでは、OID\_GEN\_受信\_スケール\_パラメーター OID を使用して、NIC の現在の RSS パラメーターを設定します。 ミニポートドライバーは、RSS パラメーターを定義する NDIS\_RECEIVE\_SCALE\_PARAMETERS 構造体を受け取ります。

> [!NOTE]
> RSSv2 では、この OID は、指定されたスケーリングエンティティの現在の RSS パラメーターに対してのみクエリを実行するために使用されます。 RSSv2 をサポートするミニポートドライバーについては、間接テーブル以外の RSS パラメーターを設定する[OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md)を参照してください。

<a name="remarks"></a>注釈
-------

NDIS ミニポートドライバーの場合、クエリは要求されず、RSS をサポートするドライバーにはこのセットが必要です。 NDIS はミニポートドライバーのクエリを処理します。

TCP/IP ドライバーは、OID\_GEN の1つの OID セット要求を使用して IPv4 と IPv6 を構成し、\_\_パラメーターを受け取る\_を生成します。 つまり、スタックが IPv4 と IPv6 の両方で RSS を有効にする必要がある場合は、NDIS の**Hashinformation**メンバーに対応する両方のフラグを設定して、 [**RECEIVE\_SCALE\_PARAMETERS 構造体\_受信**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_parameters)し、1つの OID 要求を送信します。 また、ipv4 と IPv6 の両方が有効になっている場合でも、IPv4 と IPv6 は同じシークレットキーを使用し、キーは常に40バイトになります。

基になるミニポートアダプターは、最近使用した OID\_GEN\_受け取る\_拡張\_パラメーターの OID 設定を受け取る必要があります。 たとえば、ミニポートが OID\_\_GEN を受け取ると、IPv4 ハッシュの種類が指定されていない\_の\_パラメーター OID を受け取ることができます。これを有効にした場合は、IPv4 RSS を無効にする必要があります。

**注**  は、\_ハッシュ OID を[受け取る oid\_GEN\_](oid-gen-receive-hash.md)使用して、RSS を有効にせずに受信フレームに対してハッシュ計算を有効化および構成することができます。

 

  プロトコルドライバーは、RSS を有効にする前に、受信ハッシュ計算 ([OID\_GEN\_receive\_hash](oid-gen-receive-hash.md)) を無効にする必要がある**ことに注意**してください。 RSS が有効になっている場合、受信ハッシュ計算を有効にする前に、プロトコルドライバーが RSS を無効にします。 ミニポートドライバーは、 **NDIS\_状態\_無効\_oid**または NDIS\_の状態にあるセット要求を失敗させる必要があります\_ハッシュが有効になっ**ていません**。enabled.

 

[**NDIS\_\_\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_parameters)構造体のメンバーを受け取ると、間接テーブルと秘密キーが追加**さ  ます**。 間接テーブルとシークレットキーの詳細については、「 **NDIS\_RECEIVE\_SCALE\_PARAMETERS**」を参照してください。

 

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
<td><p>NDIS 6.0 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_受信\_スケール\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_parameters)

[OID\_GEN\_RECEIVE\_HASH](oid-gen-receive-hash.md)

 

 




