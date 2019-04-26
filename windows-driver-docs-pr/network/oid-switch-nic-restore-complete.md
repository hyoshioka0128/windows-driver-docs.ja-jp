---
title: OID_SWITCH_NIC_RESTORE_COMPLETE
description: HYPER-V 拡張可能スイッチのプロトコルのエッジは、HYPER-V 拡張可能スイッチの拡張機能については、実行時データを復元する操作の完了を通知する OID_SWITCH_NIC_RESTORE_COMPLETE のオブジェクト識別子 (OID) セット要求を発行します。
ms.assetid: E47EBA55-FF35-4366-AF9C-A714C2E6F8FE
ms.date: 08/08/2017
keywords: -OID_SWITCH_NIC_RESTORE_COMPLETE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: cff184050292a50e18f0ab0593c1e556918a1ac8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353235"
---
# <a name="oidswitchnicrestorecomplete"></a>OID\_スイッチ\_NIC\_復元\_完了


HYPER-V 拡張可能スイッチのプロトコルのエッジの OID オブジェクト識別子 (OID) セット要求を発行する\_切り替える\_NIC\_復元\_HYPER-V 拡張可能スイッチの拡張機能を通知する完了、実行時データを復元する操作を完了します。 、この操作では、拡張機能は、ポートと関連付けられているネットワーク アダプター接続の場合は、その実行時データを復元します。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_スイッチ\_NIC\_保存\_状態**](https://msdn.microsoft.com/library/windows/hardware/hh598216)構造体。 この構造体は、拡張可能スイッチのプロトコル edge によって割り当てられます。

<a name="remarks"></a>注釈
-------

OID の OID のセット要求を受け取ったとき\_スイッチ\_NIC\_復元\_完了、拡張機能には、次のガイドラインが従う必要があります。

-   拡張機能は変更しないで、 [ **NDIS\_スイッチ\_NIC\_保存\_状態**](https://msdn.microsoft.com/library/windows/hardware/hh598216) OID 要求に関連付けられている構造体。
-   拡張機能を呼び出す必要があります[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)この OID を転送するには、基になる拡張機能は拡張可能スイッチ ドライバー スタックの要求を設定します。 拡張機能では、OID 要求が失敗しない必要があります。

OID の要求を設定しました OID\_スイッチ\_NIC\_復元\_完了は拡張可能スイッチの基になるミニポート edge によって最終的に処理されます。 NDIS に OID 要求が完了するミニポート edge によってこの OID メソッド要求を受信すると後、\_状態\_成功します。 拡張可能スイッチのプロトコルの端に通知、拡張可能スイッチ ドライバー スタック内のすべての拡張機能が、保存を完了している操作。

拡張可能スイッチ ポートの実行時データを保存する方法の詳細については、次を参照してください。[保存 Hyper-v 拡張可能なスイッチ実行時データ](https://msdn.microsoft.com/library/windows/hardware/hh598299)します。

### <a name="return-status-codes"></a>リターン状態コード

拡張機能の OID のセットの要求が完了すると[OID\_スイッチ\_NIC\_復元\_完了](oid-switch-nic-restore.md)、次のステータス コードの 1 つを返します。

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

[**NDIS\_スイッチ\_NIC\_保存\_状態**](https://msdn.microsoft.com/library/windows/hardware/hh598216)

 

 




