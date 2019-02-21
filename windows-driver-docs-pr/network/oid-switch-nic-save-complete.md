---
title: OID_SWITCH_NIC_SAVE_COMPLETE
description: HYPER-V 拡張可能スイッチのプロトコルのエッジは、HYPER-V 拡張可能スイッチの拡張機能については、実行時データを保存する操作の完了を通知する OID_SWITCH_NIC_SAVE_COMPLETE のオブジェクト識別子 (OID) セット要求を発行します。
ms.assetid: 75D4C0D5-B4B2-493D-8D1D-400F60613FCA
ms.date: 08/08/2017
keywords: -OID_SWITCH_NIC_SAVE_COMPLETE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: f13707aebec432109302c8293574e7b94aaa21ae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552193"
---
# <a name="oidswitchnicsavecomplete"></a>OID\_スイッチ\_NIC\_保存\_完了


HYPER-V 拡張可能スイッチのプロトコルのエッジの OID オブジェクト識別子 (OID) セット要求を発行する\_切り替える\_NIC\_保存\_HYPER-V 拡張可能スイッチの拡張機能が完了したことを通知する完了実行時のデータを保存する操作です。 この操作では、拡張機能は、ポートと関連付けられているネットワーク アダプター接続の実行時データを保存します。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_スイッチ\_NIC\_保存\_状態**](https://msdn.microsoft.com/library/windows/hardware/hh598216)構造体。

<a name="remarks"></a>注釈
-------

OID の OID のセット要求を受け取ったとき\_スイッチ\_NIC\_保存\_完了、拡張機能には、次のガイドラインが従う必要があります。

-   拡張機能は変更しないで、 [ **NDIS\_スイッチ\_NIC\_保存\_状態**](https://msdn.microsoft.com/library/windows/hardware/hh598216) OID 要求に関連付けられている構造体。

-   拡張機能を呼び出す必要があります[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)この OID を転送するには、基になる拡張機能は拡張可能スイッチ ドライバー スタックの要求を設定します。 拡張機能では、OID 要求が失敗しない必要があります。

OID の要求を設定しました OID\_スイッチ\_NIC\_保存\_完了は拡張可能スイッチの基になるミニポート edge によって最終的に処理されます。 NDIS に OID 要求が完了するミニポート edge によってこの OID メソッド要求を受信すると後、\_状態\_成功します。 拡張可能スイッチのプロトコルの端に通知、拡張可能スイッチ ドライバー スタック内のすべての拡張機能が、保存を完了している操作。

拡張可能スイッチ ポートの実行時データを保存する方法の詳細については、次を参照してください。[保存 Hyper-v 拡張可能なスイッチ実行時データ](https://msdn.microsoft.com/library/windows/hardware/hh598299)します。

### <a name="return-status-codes"></a>リターン状態コード

拡張可能スイッチの基になるミニポート edge OID の OID のクエリ要求が完了すると\_切り替える\_NIC\_保存\_完了し、次のステータス コードの 1 つを返します。

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

 

 




