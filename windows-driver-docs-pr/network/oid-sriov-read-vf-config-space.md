---
title: OID_SRIOV_READ_VF_CONFIG_SPACE
description: 上にある、ドライバーは、オブジェクト識別子 (OID) メソッドへの要求を OID_SRIOV_READ_VF_CONFIG_SPACE の PCI Express (PCIe) の構成領域からの指定した PCIe 仮想機能 (VF) ネットワーク アダプターのデータの読み取りを発行します。
ms.assetid: 48CD54F5-F18F-4BC1-A93A-A824EC041605
ms.date: 08/08/2017
keywords: -OID_SRIOV_READ_VF_CONFIG_SPACE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 1b516c0fc8e5d555a173d25e92a0085c71a5b169
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351349"
---
# <a name="oidsriovreadvfconfigspace"></a>OID\_SRIOV\_読み取り\_VF\_CONFIG\_領域


上位のドライバーの OID オブジェクト識別子 (OID) メソッド要求を発行する\_SRIOV\_読み取り\_VF\_CONFIG\_領域の指定した PCIe PCI Express (PCIe) の構成領域からデータを読み取る仮想機能 (VF) ネットワーク アダプターにします。

この OID メソッド要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体呼び出し元が割り当てたバッファーへのポインターが含まれています。 このバッファーは、以下を格納する形式です。

-   [ **NDIS\_SRIOV\_読み取り\_VF\_CONFIG\_領域\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451681)構造が含まれていますが、VF の PCI 構成領域の読み取り操作のパラメーターです。

-   PCI の構成領域から読み取られるデータの追加バッファー領域。

<a name="remarks"></a>注釈
-------

VF のミニポート ドライバーは、HYPER-V 子パーティションのゲスト オペレーティング システムで実行されます。 このため、VF のミニポート ドライバーは VF の PCI 構成領域などのハードウェア リソースを直接アクセスすることはできません。 ミニポート ドライバー PCIe 物理機能 (PF) にのみを VF の PCI 構成領域にアクセスできます。 PF のミニポート ドライバーでは、HYPER-V 親パーティションの管理オペレーティング システムで実行され、VF リソースへのアクセスには特権します。

VF PCI OID の OID メソッド要求を管理オペレーティング システムの問題で実行されているドライバーの後続の構成領域を読み取るために\_SRIOV\_読み取り\_VF\_CONFIG\_PF する領域ミニポート ドライバー。 この OID メソッド要求は、PF ミニポート ドライバー シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートする必要があります。

管理オペレーティング システムで実行されている仮想化スタックが OID の OID メソッド要求を発行するなど、\_SRIOV\_読み取り\_VF\_CONFIG\_VF のミニポート ドライバーを呼び出すときのスペース[ **NdisMGetBusData** ](https://msdn.microsoft.com/library/windows/hardware/ff563591)その PCI の VF 構成領域からの読み取り。

OID の OID メソッド要求を処理するときに\_SRIOV\_読み取り\_VF\_CONFIG\_領域、PF ミニポート ドライバーには、次のガイドラインが従う必要があります。

-   ミニポート ドライバーは、VF がで指定されたを確認する必要があります、 **VFId**のメンバー、 [ **NDIS\_SRIOV\_読み取り\_VF\_CONFIG\_領域\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451681)構造体を以前に割り当てられているリソースします。 ミニポート ドライバーは VF の OID メソッドの要求からのリソースの割り当て[OID\_NIC\_スイッチ\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)します。 指定した VF 用のリソースが割り当てられていない場合、ドライバーは OID 要求に失敗する必要があります。

-   ミニポート ドライバーを確認する必要がありますバッファー (によって参照される、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体) は、要求された PCIe 構成領域のデータを返すのに十分な大きさです。 True でない場合、ドライバーは、OID 要求を失敗する必要があります。
-   通常、ミニポート ドライバーを呼び出します[ **NdisMGetVirtualFunctionBusData** ](https://msdn.microsoft.com/library/windows/hardware/hh451484)要求 PCIe 構成領域をクエリします。 ただし、ミニポート ドライバーには VF ドライバーが前のキャッシュの PCIe 構成領域のデータの読み取りや書き込み操作、PCIe 構成領域の取得もできます。

    **注**  独立系ハードウェア ベンダー (IHV) が SR-IOV 対応の一部としてバーチャル バス ドライバー (VBD) を提供する場合[ドライバー パッケージ](https://msdn.microsoft.com/library/windows/hardware/ff544840)、ミニポート ドライバーを呼び出してはならない[ **NdisMGetVirtualFunctionBusData**](https://msdn.microsoft.com/library/windows/hardware/hh451484)します。 代わりに、ドライバーをプライベートな通信チャネルを介して VBD とのインターフェイスし、VBD を呼び出すことを要求する必要があります[ *ReadVfConfigBlock*](https://msdn.microsoft.com/library/windows/hardware/hh439637)します。 この関数がから公開されている、 [GUID\_VPCI\_インターフェイス\_標準](https://msdn.microsoft.com/library/windows/hardware/hh451146)基になる仮想 PCI (VPCI) バス ドライバーによってサポートされているインターフェイス。

     

PF のミニポート ドライバーでは、OID 要求を正常に完了する場合、ドライバーは要求された PCI 構成の領域データをによって参照されるバッファーにコピーする必要があります、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体。 ドライバーで指定されたオフセットからバッファーにデータをコピーする**BufferOffset**のメンバー [ **NDIS\_SRIOV\_読み取り\_VF\_CONFIG\_領域\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451681)構造体。

詳細については、次を参照してください。[仮想関数の PCI 構成データを照会する](https://msdn.microsoft.com/library/windows/hardware/hh440183)します。

### <a name="return-status-codes"></a>リターン状態コード

PF のミニポート ドライバーでは、OID の OID メソッド要求の次のステータス コードのいずれかを返します\_SRIOV\_読み取り\_VF\_CONFIG\_領域。

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
<td><p>ミニポート ドライバーでは、シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートしていませんか、またはインターフェイスを使用して有効になっていません。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p>1 つ以上のメンバーの<a href="https://msdn.microsoft.com/library/windows/hardware/hh451681" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_READ_VF_CONFIG_SPACE_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451681)"> <strong>NDIS_SRIOV_READ_VF_CONFIG_SPACE_PARAMETERS</strong> </a>構造が無効な値を指定します。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーが小さすぎます。 ミニポート ドライバーを設定する必要があります、<strong>データ。METHOD_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
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
[GUID\_VPCI\_インターフェイス\_標準](https://msdn.microsoft.com/library/windows/hardware/hh451146)

[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_SRIOV\_読み取り\_VF\_CONFIG\_領域\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/hh451681)

[**NdisMGetBusData**](https://msdn.microsoft.com/library/windows/hardware/ff563591)

[**NdisMGetVirtualFunctionBusData**](https://msdn.microsoft.com/library/windows/hardware/hh451484)

[OID\_NIC\_スイッチ\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)

[*ReadVfConfigBlock*](https://msdn.microsoft.com/library/windows/hardware/hh439637)

 

 




