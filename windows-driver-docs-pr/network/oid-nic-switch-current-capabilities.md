---
title: OID_NIC_SWITCH_CURRENT_CAPABILITIES
description: 上にある、ドライバーは、ネットワーク アダプターで NIC スイッチの現在有効になっているハードウェア機能を取得する OID_NIC_SWITCH_CURRENT_CAPABILITIES のオブジェクト識別子 (OID) クエリ要求を発行します。
ms.assetid: 529dc5d5-9b84-4891-9e7a-1f9f7850c6d7
ms.date: 08/08/2017
keywords: -OID_NIC_SWITCH_CURRENT_CAPABILITIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 40ab6ed6883de567f7cd58856ddebe143a461e9a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330580"
---
# <a name="oidnicswitchcurrentcapabilities"></a>OID\_NIC\_スイッチ\_現在\_機能


上にある、ドライバーの OID オブジェクト識別子 (OID) のクエリ要求を発行する\_NIC\_切り替える\_現在\_ネットワーク アダプターでの NIC を現在有効になっているハードウェア機能を取得する機能の切り替え.

OID のクエリ要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体ポインターが含まれています、 [ **NDIS\_NIC\_スイッチ\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566583)構造体。

<a name="remarks"></a>注釈
-------

ミニポート ドライバー以降 NDIS 6.20 が動作では、ネットワーク アダプターで現在有効な NIC スイッチ ハードウェア機能を提供時にその[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数が呼び出されます。 ドライバーの初期化、 [ **NDIS\_NIC\_スイッチ\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566583)構造体の NIC にハードウェアの機能およびセットのスイッチ、 **CurrentNicSwitchCapabilities**のメンバー、 [ **NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)構造体へのポインターを**NDIS\_NIC\_スイッチ\_機能**構造体。 ミニポート ドライバーを呼び出して、 [ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)関数とセット、 *MiniportAttributes*パラメーターへのポインターを**NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**構造体。

**注**  NDIS 6.30 以降、シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートするミニポート ドライバーは NIC スイッチを有効になっているハードウェア機能を登録する必要があります。 ドライバーは、呼び出すことによってこれらの機能を登録[ **NdisMSetMiniportAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff563672)します。

 

OID の OID クエリ要求を発行する上位のプロトコルとフィルター ドライバーがいない\_NIC\_スイッチ\_現在\_機能します。 NDIS は、次のように、これらのドライバーをネットワーク アダプターの現在有効な NIC スイッチ ハードウェア機能を提供します。

-   NDIS 報告、現在有効な NIC スイッチ ハードウェアを基になるネットワーク アダプターの機能でプロトコル ドライバーに関連する、 **NicSwitchCapabilities**のメンバー、 [ **NDIS\_バインド\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff564832)バインド操作中に構造体。

-   NDIS 報告、現在有効な NIC スイッチ ハードウェアを基になるネットワーク アダプターの機能のフィルター ドライバーに関連する、 **NicSwitchCapabilities**のメンバー、 [ **NDIS\_フィルター\_アタッチ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff565481) attach 操作中に構造体。

### <a name="return-status-codes"></a>リターン状態コード

OID の OID のクエリ要求を処理する NDIS\_NIC\_スイッチ\_現在\_ミニポート ドライバーの機能要求。 ドライバーにはこの OID 要求が発行するされません。

NDIS が、OID を処理するときに\_NIC\_スイッチ\_現在\_機能要求と、次のステータス コードの 1 つを返します。

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
<td><p>要求は正常に完了しました。 <strong>InformationBuffer</strong>を指す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566583" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_CAPABILITIES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566583)"> <strong>NDIS_NIC_SWITCH_CAPABILITIES</strong> </a>構造体。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>ミニポート ドライバーでは、シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートしていませんか、またはインターフェイスを使用して有効になっていません。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーの長さが sizeof より小さい (<a href="https://msdn.microsoft.com/library/windows/hardware/ff566583" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_CAPABILITIES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566583)"><strong>NDIS_NIC_SWITCH_CAPABILITIES</strong></a>)。 ミニポート ドライバーを設定する必要があります、<strong>データ。QUERY_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
</tr>
<tr class="even">
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
<td><p>以降では、NDIS 6.20 が動作をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_バインド\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff564832)

[**NDIS\_フィルター\_アタッチ\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff565481)

[**NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)

[**NDIS\_NIC\_スイッチ\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566583)

[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

 

 




