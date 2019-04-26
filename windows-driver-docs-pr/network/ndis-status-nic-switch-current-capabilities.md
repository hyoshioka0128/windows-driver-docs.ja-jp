---
title: NDIS_STATUS_NIC_SWITCH_CURRENT_CAPABILITIES
description: NDIS_STATUS_NIC_SWITCH_CURRENT_CAPABILITIES 状態は、NDIS およびネットワーク アダプターで NIC スイッチの現在有効になっているハードウェア機能が変更されたドライバーの上にあることを示します。
ms.assetid: 8F5DF045-4993-45E6-A5B9-502B695E3C62
ms.date: 08/08/2017
keywords: -NDIS_STATUS_NIC_SWITCH_CURRENT_CAPABILITIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: ba3f5ca031410c1fd6f4f8176768f604da92be93
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356850"
---
# <a name="ndisstatusnicswitchcurrentcapabilities"></a>NDIS\_状態\_NIC\_スイッチ\_現在\_機能


**NDIS\_状態\_NIC\_スイッチ\_現在\_機能**NDIS と関連付けたドライバーに状態を示しますが、現在有効になっているハードウェアネットワーク アダプターで NIC スイッチの機能が変更されました。

状態の表示が、ミニポート ドライバーのネットワーク アダプターの PCI Express (PCIe) 物理機能 (PF) によって行われます。 PF のミニポート ドライバーは、HYPER-V 親パーティションの管理オペレーティング システムで実行されます。

<a name="remarks"></a>注釈
-------

PF のミニポート ドライバーを発行する必要があります、 **NDIS\_状態\_NIC\_スイッチ\_現在\_機能**状態を示す値に変更を検出するたびに、現在のネットワーク アダプターで NIC スイッチ ハードウェアの機能を有効になります。 次の条件のいずれかが true の場合、これらの機能を変更できます。

-   現在有効な NIC スイッチ ハードウェア機能は、独立系ハードウェア ベンダー (IHV) によって開発された管理アプリケーションを通じて変更されます。

-   負荷分散マルチプレクサー中間ドライバーによって管理されているフェールオーバー (LBFO) のチームに属している 1 つまたは複数のネットワーク アダプターの現在有効な NIC スイッチ ハードウェア機能を変更します。 詳細については、次を参照してください。 [NDIS MUX 中間ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff566498)します。

PF のミニポート ドライバーを発行したとき、 **NDIS\_状態\_NIC\_スイッチ\_現在\_機能**状態を示す値、次の手順に従う必要があります。

1.  ミニポート ドライバーを初期化します、 [ **NDIS\_NIC\_スイッチ\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566583)ネットワークの現在有効になっているハードウェア機能を含む構造体アダプターの NIC のスイッチです。
2.  ミニポート ドライバーを初期化します、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)次のように構造体。

    -   **StatusCode**にメンバーを設定する必要があります**NDIS\_状態\_NIC\_スイッチ\_現在\_機能**します。

    -   **StatusBuffer**へのポインターにメンバーを設定する必要があります、 [ **NDIS\_NIC\_スイッチ\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566583)構造体。 この構造体には、NIC のスイッチの現在有効になっているハードウェア機能が含まれています。

    -   **StatusBufferSize** sizeof にメンバーを設定する必要があります ([**NDIS\_NIC\_スイッチ\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566583))。

3.  PF のミニポート ドライバーが呼び出すことで状態の通知を発行[ **NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600)します。 ドライバーへのポインターを渡す必要があります、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)構造体を*StatusIndication*パラメーター。

後続のドライバーを使用できます、 **NDIS\_状態\_NIC\_切り替える\_現在\_機能**状態を示す値を現在有効な NIC スイッチの確認ネットワーク アダプターに機能します。 または、これらのドライバーにはの OID クエリ要求が発行できますも[OID\_NIC\_スイッチ\_現在\_機能](oid-nic-switch-current-capabilities.md)をいつでもこれらの機能を取得します。

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
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


****
[**NDIS\_NIC\_スイッチ\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566583)

[**NDIS\_状態\_を示す値**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[OID\_NIC\_スイッチ\_現在\_機能](oid-nic-switch-current-capabilities.md)

 

 




