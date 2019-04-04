---
title: OID_SWITCH_NIC_RESTORE
description: オブジェクト識別子 (OID) に、拡張可能スイッチ ポートとそのネットワーク アダプターの復元は実行時データの拡張可能スイッチ拡張機能を通知する OID_SWITCH_NIC_RESTORE の要求を設定する HYPER-V 拡張可能スイッチに関する問題のプロトコルの端接続します。
ms.assetid: 252FB1D2-932F-4FB8-83D6-2690171D746D
ms.date: 08/08/2017
keywords: -OID_SWITCH_NIC_RESTORE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: c199635a6daf6c8130e599c37bd2de301f119b9e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559965"
---
# <a name="oidswitchnicrestore"></a>OID\_スイッチ\_NIC\_復元


HYPER-V 拡張可能スイッチのプロトコルのエッジの OID オブジェクト識別子 (OID) セット要求を発行する\_切り替える\_NIC\_復元については、実行時のデータを復元できる拡張可能スイッチ拡張機能を通知する、拡張可能スイッチのポートと、そのネットワーク アダプター接続します。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_スイッチ\_NIC\_保存\_状態**](https://msdn.microsoft.com/library/windows/hardware/hh598216)構造体。 この構造体は、拡張可能スイッチのプロトコル edge によって割り当てられます。

<a name="remarks"></a>注釈
-------

OID の OID のセット要求を受け取ったとき\_切り替える\_NIC\_復元、拡張可能スイッチ拡張機能を最初に確認、実行時データが所有しているかどうか。 値を比較することでこの拡張機能の実行、 **ExtensionId**のメンバー、 [ **NDIS\_スイッチ\_NIC\_保存\_状態**](https://msdn.microsoft.com/library/windows/hardware/hh598216)構造体を拡張機能を使用して自身を識別する GUID 値。

拡張機能が拡張可能スイッチ ポートの実行時のデータを所有している場合は、次のようにこのデータが復元されます。

1.  拡張機能の実行時データのコピー、 **SaveData**拡張機能に割り当てられたストレージへのメンバー。

    **注**  の値、 **PortId**のメンバー、 [ **NDIS\_スイッチ\_NIC\_保存\_状態**](https://msdn.microsoft.com/library/windows/hardware/hh598216)構造体が異なる可能性があります、 **PortId**実行時データの保存時の値。 これは、実行時のデータが別のホストへのライブ マイグレーションを実行中に保存された場合に発生することができます。 ただし、ライブ マイグレーション中に、拡張可能スイッチ ポートの構成が保持されます。 これにより、拡張可能スイッチ ポートに新しいを使用して、実行時データを復元する拡張機能**PortId**値。

     

2.  拡張機能は、NDIS を使用して、OID のセット要求を完了\_状態\_成功します。

拡張機能が指定された実行時データを所有していない場合、拡張機能を呼び出す[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)この OID を転送するには、基になる拡張機能は拡張可能スイッチ ドライバー スタックの要求を設定します。 この場合、拡張機能は変更しないで、 [ **NDIS\_スイッチ\_NIC\_保存\_状態**](https://msdn.microsoft.com/library/windows/hardware/hh598216) OID 要求に関連付けられている構造体。

場合、OID\_切り替える\_NIC\_拡張可能スイッチのミニポート edge によって復元セットの要求が受信されると、NDIS に OID 要求が完了すると、\_状態\_成功します。 これによって、拡張機能に、実行時データが所有していないことに拡張可能スイッチのプロトコルの端に通知します。

実行時のデータを復元する方法の詳細については、[Hyper-v 拡張可能スイッチ実行時データを復元](https://msdn.microsoft.com/library/windows/hardware/hh598298)を参照してください。

**注**  拡張機能には、OID セットの要求が失敗した場合、拡張可能スイッチによって、全体の復元操作は失敗します。 結果として、拡張機能では、可能な場合は、OID 要求を失敗を避ける必要があります。 など、拡張機能は、実行時データを復元するために必要なリソースを割り当てることができない場合、その実行時データを復元しない適切に機能しない場合は OID 要求が失敗にする必要があります。 ただし、「拡張機能は、エラーの状態から回復できる、OID のセット要求しないは失敗します。

 

### <a name="return-status-codes"></a>リターン状態コード

拡張機能の OID OID セットの要求が完了すると\_スイッチ\_NIC\_リストアでは、1 つを返しますの次のステータス コード。

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
<td><p>NDIS_STATUS_<em>Xxx</em></p></td>
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

[**NDIS\_スイッチ\_NIC\_保存\_状態**](https://msdn.microsoft.com/library/windows/hardware/hh598216)

[**NdisFOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff561830)

 

 




