---
title: OID_SRIOV_PROBED_BARS
description: NDIS は、ネットワーク アダプターの PCI Express (PCIe) ベース アドレスを登録します (バー) の値を取得する OID_SRIOV_PROBED_BARS のオブジェクト識別子 (OID) のクエリ要求を発行します。
ms.assetid: 81C3A5B5-58D5-41F4-A000-79F3F4E00DAD
ms.date: 08/08/2017
keywords: -OID_SRIOV_PROBED_BARS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 27f0aa9c863d7ca8977936c40f6669ba7db3826b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351340"
---
# <a name="oidsriovprobedbars"></a>OID\_SRIOV\_PROBED\_バー


OID のオブジェクト識別子 (OID) のクエリ要求を発行する NDIS\_SRIOV\_PROBED\_バー ネットワーク アダプターの PCI Express (PCIe) ベース アドレスを登録します (バー) の値を取得します。 この関数は、PCI バス ドライバーで実行されるクエリを次のネットワーク アダプターによって報告されたバーの値を返します。 このクエリでは、メモリまたはネットワーク アダプターで必要とされる I/O のアドレス空間を決定します。

OID の OID クエリ要求を発行する NDIS\_SRIOV\_PROBED\_ミニポート ドライバーのネットワーク アダプターの PCIe 物理機能 (PF) にあるバー。 この OID クエリ要求は、PF ミニポート ドライバー シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートする必要があります。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体には、バッファーへのポインターが含まれています。 このバッファーは、以下を格納する形式です。

-   [ **NDIS\_SRIOV\_PROBED\_バー\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451679)ネットワークの PCI バーでの読み取り操作のパラメーターを格納する構造体アダプター。

-   PCIe ネットワーク アダプターの各横棒の ULONG 値の配列。 この配列内の要素の最大数は PCI\_TYPE0\_アドレス。

<a name="remarks"></a>注釈
-------

HYPER-V 親パーティションの管理オペレーティング システムで実行され、PCI バス ドライバーでは、メモリまたは I/O の各 PCI ベース アドレスを登録 (バー) のネットワーク アダプターのアドレス空間の要件を照会します。 PCI バス ドライバーは、最初にバス アダプターを検出した場合に、このクエリを実行します。

この PCI バー クエリによって、PCI バス ドライバーは、次で決定します。

-   かどうか、PCI バーは、ネットワーク アダプターによってサポートされます。

-   バーがサポートされている場合、どのくらいのメモリまたは I/O のアドレス空間がバーに必要です。

仮想の PCI (VPCI) バス ドライバーは、HYPER-V 子パーティションのゲスト オペレーティング システムで実行されます。 VPCI バス ドライバーは VF の仮想ネットワーク アダプターを公開、PCI Express (PCIe) 仮想機能 (VF) が、子パーティションに関連付けられている場合 (*VF のネットワーク アダプター*)。 これは、前に、VPCI バス ドライバーは、必要なメモリまたは VF のネットワーク アダプターで必要とされるアドレス空間を決定する PCI バー クエリを実行する必要があります。

PCI の構成領域へのアクセスは、特権が必要であるために、HYPER-V 親パーティションの管理オペレーティング システムで実行されるコンポーネントによってのみ実行できます。 NDIS VPCI バス ドライバーでは、PCI バーを照会、発行 OID の OID クエリ要求を\_SRIOV\_PROBED\_PF ミニポート ドライバーにバー。 この OID クエリ要求によって返される結果は、メモリ アドレス領域の量は VF のネットワーク アダプターで必要になりますが確認できるように、VPCI バス ドライバーに転送されます。

**注**  OID の OID 要求\_SRIOV\_PROBED\_バーは、NDIS でのみ発行できます。 フィルター ドライバーのプロトコルなどの上にあるドライバーによって、OID 要求は発行されませんする必要があります。

 

OID\_SRIOV\_PROBED\_バー クエリ要求に含まれる、 [ **NDIS\_SRIOV\_PROBED\_バー\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451679)構造体。 ドライバーによって参照される配列内の PCI バーの値を返す必要があります、PF ミニポート ドライバーでは、この OID を処理する場合、 **BaseRegisterValuesOffset**のメンバー、 **NDIS\_SRIOV\_PROBED\_バー\_情報**構造体。 配列内の各オフセットの PF ミニポート ドライバーは、物理アダプターの PCI 構成領域内の同じオフセットにあるバーの ULONG 値に配列の要素を設定する必要があります。

同じ値は、管理オペレーティング システムで実行されている PCI ドライバによって実行される PCI バーのクエリを次に各棒、ドライバーによって返される値があります。 PF のミニポート ドライバーを呼び出すことができます[ **NdisMQueryProbedBars** ](https://msdn.microsoft.com/library/windows/hardware/hh451520)にこの情報を確認します。

PCI デバイスの横棒の詳細については、次を参照してください。、 *PCI ローカル バス仕様*します。

VF PCI バー レジスタを照会する方法の詳細については、次を参照してください。、 [、PCI ベース アドレスを登録仮想関数のクエリを実行する](https://msdn.microsoft.com/library/windows/hardware/hh440182)します。

### <a name="return-status-codes"></a>リターン状態コード

PF のミニポート ドライバーでは、OID のクエリ要求は、次のステータス コードのいずれかを返します\_SRIOV\_PROBED\_バー。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状態コード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NDIS_STATUS_SUCCESS</p></td>
<td><p>OID 要求は正常に完了しました。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>PF のミニポート ドライバーでは、シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートしていませんか、またはインターフェイスを使用して有効になっていません。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p>1 つ以上のメンバーの<a href="https://msdn.microsoft.com/library/windows/hardware/hh451679" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_PROBED_BARS_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451679)"> <strong>NDIS_SRIOV_PROBED_BARS_INFO</strong> </a>構造が無効な値を指定します。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーがより小さい (sizeof (<a href="https://msdn.microsoft.com/library/windows/hardware/hh451679" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_PROBED_BARS_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451679)"><strong>NDIS_SRIOV_PROBED_BARS_INFO</strong></a>) + PCI_TYPE0_ADDRESSES)。 PF のミニポート ドライバーを設定する必要があります、<strong>データ。QUERY_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_FAILURE</p></td>
<td><p>他の理由から、要求が失敗しました。</p></td>
</tr>
</tbody>
</table>

 

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
<td><p>NDIS 6.30 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


****
[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_SRIOV\_PROBED\_バー\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451679)

[**NdisMQueryProbedBars**](https://msdn.microsoft.com/library/windows/hardware/hh451520)

 

 




