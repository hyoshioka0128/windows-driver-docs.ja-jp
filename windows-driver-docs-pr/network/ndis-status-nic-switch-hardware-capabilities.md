---
title: NDIS_STATUS_NIC_SWITCH_HARDWARE_CAPABILITIES
description: NDIS_STATUS_NIC_SWITCH_HARDWARE_CAPABILITIES 状態は、NDIS とのネットワーク アダプターで NIC スイッチ ハードウェア機能が変更されたドライバーの上にあることを示します。
ms.assetid: 21B326EC-22CC-4E41-895F-457971202C0B
ms.date: 08/08/2017
keywords: -NDIS_STATUS_NIC_SWITCH_HARDWARE_CAPABILITIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 49b911a31a2b9df397db61c1e3462f67a11bd1bb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343267"
---
# <a name="ndisstatusnicswitchhardwarecapabilities"></a>NDIS\_状態\_NIC\_スイッチ\_ハードウェア\_機能


**NDIS\_状態\_NIC\_スイッチ\_ハードウェア\_機能**NDIS と関連付けたドライバーに状態を示します NIC のハードウェア機能ネットワーク アダプターのスイッチが変更されました。 これらの機能には、INF ファイルの設定、または、現在無効になっているハードウェア機能が含まれる、**詳細**プロパティ ページ。

状態の表示が、ミニポート ドライバーのネットワーク アダプターの PCI Express (PCIe) 物理機能 (PF) によって行われます。 PF のミニポート ドライバーは、HYPER-V 親パーティションの管理オペレーティング システムで実行されます。

<a name="remarks"></a>コメント
-------

PF のミニポート ドライバーを発行する必要があります、 **NDIS\_状態\_NIC\_スイッチ\_ハードウェア\_機能**状態を示す値に変更を検出するたびに、NIC のハードウェア機能は、ネットワーク アダプターに切り替えます。 次の条件のいずれかが true の場合、これらの機能を変更できます。

-   NIC スイッチ ハードウェアの機能では、有効または独立系ハードウェア ベンダー (IHV) によって開発された管理アプリケーションで無効にします。

-   負荷分散マルチプレクサー中間ドライバーによって管理されているフェールオーバー (LBFO) のチームに属している 1 つまたは複数のネットワーク アダプターの NIC スイッチ ハードウェアの機能を変更します。 詳細については、次を参照してください。 [NDIS MUX 中間ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff566498)します。

PF のミニポート ドライバーを発行したとき、 **NDIS\_状態\_NIC\_スイッチ\_ハードウェア\_機能**状態を示す値、次の手順に従う必要があります。

1.  ミニポート ドライバーを初期化します、 [ **NDIS\_NIC\_切り替える\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566583)ネットワーク アダプターの NIC のスイッチのハードウェア機能を含む構造体.
2.  ミニポート ドライバーを初期化します、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)次のように構造体。

    -   **StatusCode**にメンバーを設定する必要があります**NDIS\_状態\_NIC\_スイッチ\_ハードウェア\_機能**します。

    -   **StatusBuffer**へのポインターにメンバーを設定する必要があります、 [ **NDIS\_NIC\_スイッチ\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566583)構造体。 この構造体には、NIC のスイッチのハードウェア機能が含まれています。

    -   **StatusBufferSize** sizeof にメンバーを設定する必要があります ([**NDIS\_NIC\_スイッチ\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566583))。

3.  PF のミニポート ドライバーが呼び出すことで状態の通知を発行[ **NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600)します。 ドライバーへのポインターを渡す必要があります、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)構造体を*StatusIndication*パラメーター。

後続のドライバーを使用できます、 **NDIS\_状態\_NIC\_切り替える\_ハードウェア\_機能**状態を示す値を現在有効な NIC スイッチの確認ネットワーク アダプターに機能します。 または、これらのドライバーにはの OID クエリ要求が発行できますも[OID\_NIC\_スイッチ\_ハードウェア\_機能](oid-nic-switch-hardware-capabilities.md)をいつでもこれらの機能を取得します。

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
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


****
[**NDIS\_NIC\_スイッチ\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566583)

[**NDIS\_状態\_を示す値**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[OID\_NIC\_スイッチ\_ハードウェア\_機能](oid-nic-switch-hardware-capabilities.md)

 

 




