---
title: OID_GEN_RECEIVE_SCALE_PARAMETERS
description: クエリとして NDIS と関連付けたドライバーできます OID を使用 OID_GEN_RECEIVE_SCALE_PARAMETERS、現在の受信側 NIC のスケーリング (RSS) のパラメーターをクエリする
ms.assetid: a54190f7-0d2e-4f85-84c2-05fc9ec4994a
ms.date: 08/08/2017
keywords: -OID_GEN_RECEIVE_SCALE_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: ebd164b14c13c5ca30fdec357c1225afcae3d9e7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553848"
---
# <a name="oidgenreceivescaleparameters"></a>OID\_GEN\_受信\_スケール\_パラメーター


クエリとして NDIS と関連付けたドライバーできます OID を使用\_GEN\_受信\_スケール\_現在のクエリを実行するパラメーターの OID が NIC の側のスケーリング (RSS) パラメーターを受け取る NDIS を返します、 [ **NDIS\_受信\_スケール\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567228) RSS の現在のパラメーターを定義する構造体。

セットとして NDIS と関連付けたドライバー使用 OID\_GEN\_受信\_スケール\_NIC の現在の RSS パラメーターを設定するパラメーターの OID ミニポート ドライバーが受信、NDIS\_受信\_スケール\_RSS パラメーターを定義するパラメーターの構造体。

> [!NOTE]
> RSSv2 でこの OID は、スケーリング、特定のエンティティの現在の RSS パラメーターをクエリにのみ使用します。 RSSv2 をサポートするミニポート ドライバーでは、次を参照してください。 [OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md)間接指定テーブル以外の RSS パラメーターを設定します。

<a name="remarks"></a>注釈
-------

NDIS ミニポート ドライバーでは、クエリが要求されていないと、RSS をサポートするドライバーに対して必要です。 NDIS は、ミニポート ドライバーにクエリを処理します。

TCP/IP ドライバーは IPv4 を構成し、1 つの OID と IPv6 の OID 要求の設定\_GEN\_受信\_スケール\_パラメーター。 つまり、スタックは、IPv4 と IPv6 の両方に対して RSS が有効にする必要があります、設定に対応するフラグの両方、 **HashInformation**のメンバー、 [ **NDIS\_受信\_スケール\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567228)構造と送信の 1 つの OID 要求。 また、IPv4 と IPv6 の同じ秘密キーを使用して、IPv4 のみが有効になっている場合でも、キーが 40 (バイト単位) を必ず。

基になるミニポート アダプターは、最新の OID を使用する必要があります\_GEN\_受信\_スケール\_受け取ったパラメーター OID 設定します。 たとえば、ミニポート OID の取得\_GEN\_受信\_スケール\_IPv4 ハッシュを使用してパラメーターの OID は型がありません、コントロールが以前に有効な場合は、IPv4 RSS を無効にする必要があります。

**注**  遮断のドライバーを使用して、 [OID\_GEN\_受信\_ハッシュ](oid-gen-receive-hash.md)OID を有効にし、ハッシュ計算を構成するのには、RSS を有効にしなくてもフレームを受信します。

 

**注**  プロトコル ドライバーを無効にする必要がありますがハッシュの計算値を受け取り ([OID\_GEN\_受信\_ハッシュ](oid-gen-receive-hash.md)) RSS を有効にする前にします。 RSS が有効になっている場合、プロトコル ドライバー無効 RSS が有効にする前に、ハッシュ計算を受け取ります。 ミニポート ドライバーのセットの要求が失敗する**NDIS\_状態\_無効な\_OID**または**NDIS\_状態\_いない\_サポートされています。** 場合は、RSS を有効にする OID\_GEN\_受信\_ハッシュが現在有効になっています。

 

**注**  間接指定テーブルと秘密キーは後に追加された、 [ **NDIS\_受信\_スケール\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567228)構造体のメンバー。 間接指定テーブルと秘密キーの詳細については、次を参照してください。 **NDIS\_受信\_スケール\_パラメーター**します。

 

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
<td><p>NDIS 6.0 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_受信\_スケール\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff567228)

[OID\_GEN\_受信\_ハッシュ](oid-gen-receive-hash.md)

 

 




