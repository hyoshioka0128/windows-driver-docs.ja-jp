---
title: OID_RECEIVE_FILTER_SET_FILTER
description: 上にある、ドライバーは、ネットワーク アダプターに対してフィルターを設定する OID_RECEIVE_FILTER_SET_FILTER の OID メソッド要求を発行します。
ms.assetid: ec3e119e-662f-48a6-8c68-20da20590b24
ms.date: 08/08/2017
keywords: -OID_RECEIVE_FILTER_SET_FILTER ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 05cdff68157c6151a304593e91feff71971b0145
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528357"
---
# <a name="oidreceivefiltersetfilter"></a>OID\_受信\_フィルター\_設定\_フィルター

OID の OID メソッド要求を発行する上位のドライバー\_受信\_フィルター\_設定\_ネットワーク アダプターに対してフィルターを設定するフィルター。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体には、呼び出し元が割り当てたバッファーへのポインターが含まれています。 このバッファーは、以下を格納する形式です。

-   [ **NDIS\_受信\_フィルター\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567181) NDIS のパラメーターを指定する構造体は、フィルターを受信します。

-   配列の[ **NDIS\_受信\_フィルター\_フィールド\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567169)フィルターを指定する構造体のフィールドの条件をテストします。ネットワーク パケットのヘッダー。

OID メソッドの要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体ポインターが含まれています、 [ **NDIS\_受信\_フィルター\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567181)構造体。 上にあるドライバーは、新しい受信フィルターを作成するは、NDIS は新しいフィルターの識別子を持つこの構造体を更新します。

<a name="remarks"></a>注釈
-------

NDIS フィルターが表示される次の NDIS インターフェイスで使用されます。

-   [NDIS パケット結合](https://msdn.microsoft.com/library/windows/hardware/hh451601)します。 使用する方法の詳細についてはこのインターフェイスでフィルターが表示されるを参照してください[管理パケット結合受信フィルター](https://msdn.microsoft.com/library/windows/hardware/hh464026)します。

-   [シングル ルート I/O 仮想化 (SR-IOV)](https://msdn.microsoft.com/library/windows/hardware/hh440235)します。 使用する方法の詳細についてはこのインターフェイスでフィルターが表示されるを参照してください[仮想ポートで受信フィルターを設定](https://msdn.microsoft.com/library/windows/hardware/hh440224)します。

-   [バーチャル マシン キュー (VMQ)](https://msdn.microsoft.com/library/windows/hardware/ff571035)。 使用する方法の詳細についてはこのインターフェイスでフィルターが表示されるを参照してください[設定および VMQ のフィルターをクリアする](https://msdn.microsoft.com/library/windows/hardware/ff570780)します。

OID の OID メソッド要求\_受信\_フィルター\_設定\_フィルターは NDIS パケットの結合、SR-IOV、または VMQ インターフェイスをサポートするミニポート ドライバーに対して必須です。

上にあるドライバーを初期化します、 [ **NDIS\_受信\_フィルター\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567181)要求フィルター構成構造体。 NDIS フィルター識別子を割り当てます、 **FilterId**の NDIS メンバー\_受信\_フィルター\_パラメーター構造体し、メソッド要求を基になるミニポート ドライバーに渡します。

受信キューが設定されている各フィルターには、ネットワーク アダプターのフィルターの一意な識別子があります。 つまり、フィルターの識別子は、ネットワーク アダプターを管理する別のキューでは複製されません。 NDIS 受信キューにフィルターを設定する OID 要求を受け取ると、フィルター パラメーターを確認します。 NDIS は、必要なリソースとフィルターの識別子を割り当て後、は、基になるネットワーク アダプターに OID 要求を送信します。 NDIS の戻り値を持つ OID 要求が完了する場合は、ネットワーク アダプターは、フィルター、必要なソフトウェアとハードウェア リソースを割り当てることができますが正常に、\_状態\_成功します。

**注**NDIS 6.30 以降では、受信パケットの結合フィルターは、既定でのみサポート、ネットワーク アダプターのキューの受信します。 この受信キューが識別子の NDIS\_既定\_受信\_キュー\_id。



ミニポート ドライバーでは、割り当てられた受信のフィルターのフィルターの識別子を保持する必要があります。 NDIS は、以降の OID 要求で受信フィルター パラメーターを変更または受信のフィルターをクリアするフィルターの識別子を使用します。

ドライバーの受信後、ミニポート、 [OID\_受信\_フィルター\_キュー\_割り当て\_完了](oid-receive-filter-queue-allocation-complete.md)要求とそれが、キューのキューに設定されているフィルター*を実行している*状態。 この状態で、ミニポート ドライバーは、呼び出すことによって、キューにあるパケットの兆候を開始できます[ **NdisMIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff563598)します。

### <a name="additional-guidelines-for-the-sr-iov-interface"></a>SR-IOV インターフェイスに関する追加のガイドライン

次の点は、SR-IOV 対応インターフェイスをサポートするミニポート ドライバーに適用されます。

-   SR-IOV インターフェイスで、既定値または既定以外の仮想ポート (VPort) で受信キューが作成されます。

    **注**以降 Windows Server 2012、SR-IOV インターフェイスのみをサポートで既定の受信、VPort のキューに登録します。

    OID セットの要求を通じて、SR-IOV VPort が割り当てられた後[OID\_NIC\_スイッチ\_作成\_VPORT](oid-nic-switch-create-vport.md)OID の OID 要求と VPort のフィルターの設定は重なってドライバー\_受信\_フィルター\_設定\_フィルター。

    **注**だけで、VPort を割り当て、上にあるドライバーはその VPort に対してフィルターを設定することができます。

-   既定 VPort が常に存在するので、ドライバーが重なって常にフィルターを設定できます VPort の既定の。

-   VPort が作成されたときにに受信フィルターが設定されていません。 この場合、ミニポート ドライバー示す必要がありますいないミニポート ドライバー OID の OID 要求を受信する前に、いずれかの受信パケットその VPort\_受信\_フィルター\_設定\_VPort のフィルター処理します。 この OID 要求が発行されると、ミニポート ドライバーはその VPort 上のパケットを指定できます。

    **注**OID の OID 要求を処理中、ミニポート ドライバーを VPort 上のパケットを示している場合\_受信\_フィルター\_設定\_フィルター、OID 要求を完了し、NDISを返す必要があります\_ステータス\_成功状態コード。

### <a name="additional-guidelines-for-the-vmq-interface"></a>VMQ インターフェイスに関する追加のガイドライン

VMQ インターフェイスをサポートするミニポート ドライバーに、次の点が適用されます。

-   VMQ の受信キューが割り当てられた後のドライバーの関連フィルターの設定は OID の OID 要求と受信キューで\_受信\_フィルター\_設定\_フィルター。

    **注**だけで受信キューに割り当てられているプロトコル ドライバーはそのキューにフィルターを設定することができます。

-   既定のキューが常に存在するので、ドライバーを後続常にフィルターを設定、既定のキューに。 ネットワーク アダプターでは、ドロップ キューをサポートする場合、後続のドライバーと、フィルターがドロップ キューを設定できます。

    上にあるドライバーは、既定または drop のキューを所有していません。 そのため、ネットワーク アダプターにバインドされているすべてのプロトコル ドライバーは、既定値を使用して、またはキューを削除します。

-   受信キューが作成されたときにに受信フィルターが設定されていません。 この場合、ミニポート ドライバー示す必要がありますいないその受信キューで受信パケットがすべてミニポート ドライバー OID の OID 要求を受信する前に\_受信\_フィルター\_設定\_受信キューのフィルター。 この OID 要求が発行されると、ミニポート ドライバーはそのパケットの受信キューを指定できます。

    **注**OID の OID 要求を処理中、ミニポート ドライバーをキューにパケットを示している場合\_受信\_フィルター\_設定\_フィルター、OID 要求を完了し、NDISを返す必要があります\_ステータス\_成功状態コード。

### <a name="return-status-codes"></a>リターン状態コード

ミニポート ドライバーでは、OID の OID メソッド要求の次のステータス コードのいずれかを返します\_受信\_フィルター\_設定\_フィルター。

<a href="" id="ndis-status-success"></a>NDIS\_状態\_成功  
フィルターは、キューに正常に設定されました。 情報バッファーが含まれていますが、更新された[ **NDIS\_受信\_フィルター\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567181)構造体。

<a href="" id="ndis-status-pending"></a>NDIS\_状態\_PENDING  
完了待ちになっています。 最終的な状態コードと結果は、呼び出し元の OID 要求完了ハンドラーに渡されるされます。

<a href="" id="ndis-status-invalid-parameter"></a>NDIS\_状態\_無効な\_パラメーター  
1 つ以上の上にあるドライバーが提供されているパラメーターが無効です。

<a href="" id="ndis-status-invalid-length"></a>NDIS\_状態\_無効な\_長さ  
情報バッファーが小さすぎます。 NDIS セット、**データ。メソッド\_情報。BytesNeeded**内のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体に必要な最小バッファー サイズ。

<a href="" id="ndis-status-not-supported"></a>NDIS\_状態\_いない\_サポートされています。  
ミニポート ドライバーの NDIS バージョン 6.20 が動作より前のバージョンです。

<a href="" id="ndis-status-failure"></a>NDIS\_状態\_エラー  
他の理由から、要求が失敗しました。

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
<td><p>以降では、NDIS 6.20 が動作をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NdisMIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff563598)

[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_受信\_フィルター\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff567181)

[**NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)

[**NET\_バッファー\_一覧\_受信\_フィルター\_ID**](https://msdn.microsoft.com/library/windows/hardware/ff568406)

[OID\_NIC\_スイッチ\_作成\_VPORT](oid-nic-switch-create-vport.md)

[OID\_受信\_フィルター\_クリア\_フィルター](oid-receive-filter-clear-filter.md)

[OID\_受信\_フィルター\_キュー\_割り当て\_完了](oid-receive-filter-queue-allocation-complete.md)