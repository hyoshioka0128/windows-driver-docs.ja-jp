---
title: OID_NIC_SWITCH_CREATE_SWITCH
description: NDIS は、ネットワーク アダプターで NIC スイッチを作成する OID_NIC_SWITCH_CREATE_SWITCH のオブジェクト識別子 (OID) メソッド要求を発行します。
ms.assetid: 16FFC6A4-11A6-45A1-ABCF-8C1EBE3FD953
ms.date: 08/08/2017
keywords: -OID_NIC_SWITCH_CREATE_SWITCH ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 939517cb5a6517e793cbe924ebb6fb7a246386e5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578135"
---
# <a name="oidnicswitchcreateswitch"></a>OID\_NIC\_スイッチ\_作成\_スイッチ


NDIS OID のオブジェクト識別子 (OID) メソッド要求の発行\_NIC\_切り替える\_作成\_NIC を作成するスイッチがネットワーク アダプターに切り替えます。 この OID 要求を処理する場合、ミニポート ドライバーは、アダプターで NIC スイッチのリソースを割り当てます。

NDIS は、ミニポート ドライバーのネットワーク アダプターの PCI Express (PCIe) 物理機能 (PF) にこの OID メソッド要求を発行します。 この OID メソッド要求は、PF ミニポート ドライバー シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートする必要があります。

**注**  OID の OID メソッドの要求を発行できないなど、プロトコルまたはフィルター ドライバー、ドライバー、スライド\_NIC\_スイッチ\_作成\_PF ミニポート ドライバーに切り替えます。

 

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_NIC\_スイッチ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451587)構造体。

<a name="remarks"></a>コメント
-------

OID の OID メソッド要求を受け取ったとき\_NIC\_スイッチ\_作成\_スイッチ、PF ミニポート ドライバーでは、次を実行する必要があります。

1.  NDIS を呼び出すときは、NIC スイッチを作成しますが、PF ミニポート ドライバーでは、静的スイッチの作成と構成をサポートする場合[ *MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)します。 構成パラメーターを確認する必要があります、ドライバーは、この OID 要求を処理する場合、 [ **NDIS\_NIC\_スイッチ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451587)構造体。 パラメーターが呼び出し中に、スイッチを作成する、ドライバーによって使用されるものと同じにする必要があります*MiniportInitializeEx*します。 True でない場合、ドライバーは、OID 要求を失敗する必要があります。

    詳細については、[NIC スイッチの作成を静的](https://msdn.microsoft.com/library/windows/hardware/hh440256)を参照してください。

2.  ドライバーの構成値を検証する必要があります、PF ミニポート ドライバーでは、動的なスイッチの作成と構成をサポートする場合、 [ **NDIS\_NIC\_切り替える\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/hh451587)構造体し、これらの値に基づいて、NIC のスイッチを作成します。

    詳細については、[NIC スイッチの動的な作成](https://msdn.microsoft.com/library/windows/hardware/hh406694)を参照してください。

3.  PF ミニポート ドライバーでは、NIC のスイッチの既定 VPort のために必要なハードウェアおよびソフトウェア リソースを割り当てる必要があります。

    **注**  VPort が OID の OID 要求を使って作成された常に既定\_NIC\_スイッチ\_作成\_スイッチを介して、OID 要求の削除と[OID\_NIC\_スイッチ\_削除\_スイッチ](oid-nic-switch-delete-switch.md)します。 OID 要求[OID\_NIC\_スイッチ\_作成\_VPORT](oid-nic-switch-create-vport.md)と[OID\_NIC\_スイッチ\_DELETE\_VPORT](oid-nic-switch-delete-vport.md)作成と NIC のスイッチの拡張を既定以外の削除に使用されます。

     

4.  呼び出して、スイッチの SR-IOV 仮想化を有効にする必要があります動的スイッチの作成と構成をサポートしている PF ミニポート ドライバー [ **NdisMEnableVirtualization**](https://msdn.microsoft.com/library/windows/hardware/hh451481)します。 この呼び出しを構成、 **NumVFs**メンバーと**VF 有効**アダプターの構成領域の PCI Express (PCIe) の SR-IOV 拡張機能の構造内のビットします。

    SR-IOV 構成領域の詳細については、PCI SIG を参照してください。[シングル ルート I/O 仮想化および共有 1.1](https://go.microsoft.com/fwlink/p/?linkid=221742)仕様。

    **注**  スイッチを作成した後は、SR-IOV 仮想化を有効に、PF ミニポート ドライバーでは、静的スイッチの作成をサポートする場合と[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)が呼び出されます.

     

PF のミニポート ドライバーが OID の OID メソッド要求が正常に完了かどうか\_NIC\_スイッチ\_作成\_スイッチでは、次のようできます。

-   VFs を割り当てることができますの OID メソッド要求を通じて NIC スイッチ[OID\_NIC\_切り替える\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)します。

-   既定以外の拡張を作成することができますの OID メソッド要求を通じて NIC スイッチ[OID\_NIC\_切り替える\_作成\_VPORT](oid-nic-switch-create-vport.md)します。

この OID 要求を処理する方法の詳細については、[処理 OID\_NIC\_スイッチ\_作成\_切り替え要求を](https://msdn.microsoft.com/library/windows/hardware/hh451370)を参照してください。

### <a name="return-status-codes"></a>リターン状態コード

PF のミニポート ドライバーでは、OID の OID メソッド要求の次のステータス コードのいずれかを返します\_NIC\_スイッチ\_作成\_スイッチ。

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
<td><p>PF のミニポート ドライバーが SR-IOV インターフェイスをサポートしないか、またはインターフェイスを使用して有効になっていません。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p>1 つ以上のメンバーの<a href="https://msdn.microsoft.com/library/windows/hardware/hh451587" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451587)"> <strong>NDIS_NIC_SWITCH_PARAMETERS</strong> </a>構造が無効な値を指定します。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーの長さが sizeof より小さい (<a href="https://msdn.microsoft.com/library/windows/hardware/hh451587" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451587)"><strong>NDIS_NIC_SWITCH_PARAMETERS</strong></a>)。 PF のミニポート ドライバーを設定する必要があります、<strong>データ。METHOD_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_FAILURE</p></td>
<td><p>他の理由から、要求が失敗しました。</p></td>
</tr>
</tbody>
</table>

 

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
[*MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)

[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_NIC\_SWITCH\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh451587)

[**NdisMEnableVirtualization**](https://msdn.microsoft.com/library/windows/hardware/hh451481)

[OID\_NIC\_スイッチ\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)

[OID\_NIC\_スイッチ\_作成\_VPORT](oid-nic-switch-create-vport.md)

 

 




