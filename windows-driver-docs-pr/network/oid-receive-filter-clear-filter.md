---
title: OID_RECEIVE_FILTER_CLEAR_FILTER
description: ドライバーの問題を重なって OID は、ネットワーク アダプターで受信フィルターをクリアする OID_RECEIVE_FILTER_CLEAR_FILTER の要求を設定します。
ms.assetid: 5e92a11a-468e-431d-b4e5-7b0da3847e8a
ms.date: 08/08/2017
keywords: -OID_RECEIVE_FILTER_CLEAR_FILTER ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 00135aa3af9c79964fcdfa14622421b3a256598e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580899"
---
# <a name="oidreceivefilterclearfilter"></a>OID\_受信\_フィルター\_クリア\_フィルター


OID の要求を設定しました OID ドライバーの問題を後続\_受信\_フィルター\_オフ\_ネットワーク アダプターで受信フィルターをクリアするフィルター。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_受信\_フィルター\_クリア\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567166)構造体。

<a name="remarks"></a>コメント
-------

NDIS フィルターが表示される次の NDIS インターフェイスで使用されます。

-   [NDIS パケット結合](https://msdn.microsoft.com/library/windows/hardware/hh451601)します。 使用する方法の詳細についてはこのインターフェイスでフィルターが表示されるを参照してください[管理パケット結合受信フィルター](https://msdn.microsoft.com/library/windows/hardware/hh464026)します。

-   [シングル ルート I/O 仮想化 (SR-IOV)](https://msdn.microsoft.com/library/windows/hardware/hh440235)します。 使用する方法の詳細についてはこのインターフェイスでフィルターが表示されるを参照してください[仮想ポートで受信フィルターを設定](https://msdn.microsoft.com/library/windows/hardware/hh440224)します。

-   [バーチャル マシン キュー (VMQ)](https://msdn.microsoft.com/library/windows/hardware/ff571035)。 使用する方法の詳細についてはこのインターフェイスでフィルターが表示されるを参照してください[設定および VMQ のフィルターをクリアする](https://msdn.microsoft.com/library/windows/hardware/ff570780)します。

OID の OID の要求を設定する\_受信\_フィルター\_クリア\_フィルターは NDIS パケットの結合、SR-IOV、または VMQ インターフェイスをサポートするミニポート ドライバーに対して必須です。

NDIS プロトコルまたはフィルター ドライバーなどの上にあるドライバーは、OID を使用して\_受信\_フィルター\_オフ\_フィルターの設定、以前に設定を消去する要求フィルター。 受信フィルターを設定するドライバーだけをオフにします。

上にあるドライバーは、設定して、受信フィルターをクリアします、 **FilterId**のメンバー、 [ **NDIS\_受信\_フィルター\_クリア\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567166)フィルターの識別子を構造体。 ドライバーの以前の OID メソッド要求からフィルターの識別子を取得した[OID\_受信\_フィルター\_設定\_フィルター](oid-receive-filter-set-filter.md)します。

### <a name="additional-instructions-for-ndis-packet-coalescing"></a>NDIS に関する詳しい説明についてパケットの結合

次の点は、ミニポートおよび NDIS パケットの結合をサポートしている上位のドライバーに適用されます。

-   上位のドライバーをバインド解除またはドライバーからデタッチされる前に、ミニポート ドライバーの設定がすべての受信フィルターをオフにする必要があります。

### <a name="additional-guidelines-for-the-sr-iov-interface"></a>SR-IOV インターフェイスに関する追加のガイドライン

ミニポートと SR-IOV インターフェイスをサポートするドライバーを前提に、次の点が適用されます。

-   上にある、ドライバーは、設定されると、VPort を解放する前に、SR-IOV VPort のすべてのフィルターをクリアする必要があります。 上にあるドライバーも設定されると、ネットワーク アダプターには、そのバインドが閉じる前に、既定 VPort のすべてのフィルターをオフにする必要があります。

-   OID の OID 要求が完了しなかった場合、ミニポート ドライバーは既定以外の VPort 上のパケットを示していませんする必要があります\_受信\_フィルター\_オフ\_VPort の最後のフィルターをクリアするフィルター。

    **注**  ミニポート ドライバーも示す必要がありますいない VPort の既定以外のパケットの OID 要求を完了して場合[OID\_NIC\_スイッチ\_削除\_VPORT](oid-nic-switch-delete-vport.md) 、VPort を解放します。

     

### <a name="additional-guidelines-for-the-vmq-interface"></a>VMQ インターフェイスに関する追加のガイドライン

ミニポートおよび VMQ インターフェイスをサポートする上位のドライバーに、次の点が適用されます。

-   上にある、ドライバーは、すべてをクリアする必要があります受信キューのキューを解放する前に、VMQ に設定するフィルター。 上にあるドライバーも設定されると、ネットワーク アダプターには、そのバインドが閉じる前に、既定または drop のキューのすべてのフィルターをオフにする必要があります。

-   OID の OID 要求が完了しなかった場合、ミニポート ドライバーは受信キュー上のパケットを示していませんする必要があります\_受信\_フィルター\_オフ\_受信キューの最後のフィルターをクリアするフィルター。

    **注**  ミニポート ドライバーも示す必要がありますいない受信キュー上のパケットの OID 要求を完了して場合[OID\_受信\_フィルター\_FREE\_キュー](oid-receive-filter-free-queue.md)受信キューを解放します。

     

### <a name="return-status-codes"></a>リターン状態コード

ミニポート ドライバーの[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)関数は、次のいずれかがこの要求の値を返します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>項目</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>NDIS_STATUS_SUCCESS</strong></p></td>
<td><p>ミニポート ドライバーでは、要求が正常に完了しました。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_PENDING</strong></p></td>
<td><p>ミニポート ドライバーでは、要求を非同期的に実行されます。 ミニポート ドライバーには、すべての処理が完了したら後、は、呼び出すことによって、要求が成功する必要があります、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff563622" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563622)"> <strong>NdisMOidRequestComplete</strong> </a>関数<strong>NDIS_STATUS_SUCCESS</strong>の<em>状態</em>パラメーター。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_NOT_ACCEPTED</strong></p></td>
<td><p>ミニポート アダプタは、突然削除されました。</p></td>
</tr>
</tbody>
</table>

 

NDIS は、この要求の次のステータス コードのいずれかを返します。

<a href="" id="ndis-status-success"></a>**NDIS\_状態\_成功**  
指定したフィルターがクリアされました。

<a href="" id="ndis-status-pending"></a>**NDIS\_状態\_PENDING**  
完了待ちになっています。 NDIS では、要求が完了した後、最終的な状態コードと結果を呼び出し元の OID 要求完了ハンドラーに渡すは。

<a href="" id="ndis-status-file-not-found"></a>**NDIS\_状態\_ファイル\_いない\_が見つかりました**  
フィルターの識別子が無効です。

<a href="" id="ndis-status-invalid-length"></a>**NDIS\_状態\_無効な\_長さ**  
情報バッファーが小さすぎます。 NDIS セット、**データ。設定\_情報。BytesNeeded**内のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体に必要な最小バッファー サイズ。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>以降では、NDIS 6.20 が動作をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_受信\_フィルター\_クリア\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff567166)

[OID\_NIC\_スイッチ\_削除\_VPORT](oid-nic-switch-delete-vport.md)

[OID\_受信\_フィルター\_FREE\_キュー](oid-receive-filter-free-queue.md)

[OID\_受信\_フィルター\_設定\_フィルター](oid-receive-filter-set-filter.md)

 

 




