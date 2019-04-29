---
title: OID_WDI_ABORT_TASK
description: OID_WDI_ABORT_TASK は、特定の保留中のタスクをキャンセルするダウン送信されるプロパティです。
ms.assetid: 0E454DC9-1CED-497F-90A8-7065883BB945
ms.date: 07/18/2017
keywords:
- OID_WDI_ABORT_TASK ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: e72ddd10a06ce1e40583d7dd25fa9af9ef5e4760
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384627"
---
# <a name="oidwdiaborttask"></a>OID\_WDI\_中止\_タスク


OID\_WDI\_中止\_タスクは、特定の保留中のタスクをキャンセルするダウン送信されるプロパティ。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | X                       | 1                               |

 

このコマンドでは、プロパティのセマンティクスに従います。 シグナルとして扱う必要がある、できるだけ早く処理する必要がありますおよびタスクの完了とは無関係に完了する必要があります。 IHV コンポーネントは、保留中のタスクをできるだけ早く完了する必要があります試みます。

## <a name="command-parameters"></a>コマンドのパラメーター


| TLV                                                                    | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                          |
|------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------|
| [**WDI\_TLV\_CANCEL\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/dn926163) |                                |          | 取り消されているコマンドの情報です。 |

 

## <a name="command-result"></a>コマンドの結果


NDIS の状態を含む\_状態\_成功します。 追加のペイロードはありません。
## <a name="examples"></a>例


元の入力タスク コマンド:

フィールドのサブフィールド型の値の NDIS\_OID\_要求 Oid NDIS\_OID OID(WDI\_TASK\_SCAN) InputBufferLength UINT32 0x210 (例) InformationBuffer PVOID ポインター WDI を格納しているメモリ ブロックへ\_メッセージ\_ヘッダー + TLV ペイロード WDI\_メッセージ\_ヘッダー PortId UINT16 0x0001 (例) 予約済み UINT16 N/A WiFiStatus NDIS\_状態 N/A TransactionId UINT32 0x1111 (例) IhvSpecificId UINT32 N/A TLV ペイロード TLV ペイロードさまざまなペイロード データ
 

タスクで入力コマンド (とメッセージ ヘッダー) を中止します。

フィールドのサブフィールド型の値の NDIS\_OID\_要求 Oid NDIS\_OID OID(WDI\_ABORT\_TASK) InputBufferLength UINT32 sizeof (WDI\_メッセージ\_ヘッダー) + sizeof (WDI\_TLV\_キャンセル\_パラメーター) WDI を含むメモリ ブロックへの InformationBuffer PVOID ポインター\_メッセージ\_ヘッダー + TLV ペイロード WDI\_メッセージ\_ヘッダー PortId UINT16 0x0001 (例) 予約済み UINT16 N/A WiFiStatus NDIS\_状態 N/A TransactionId UINT32 0x2222 (例) IhvSpecificId UINT32 0 WDI\_TLV\_キャンセル\_パラメーターOriginalTaskOid NDIS\_OID OID(WDI\_TASK\_SCAN) OriginalPortId UINT16 0x0001 (例) OriginalTransactionId UINT32 0x1111 (例)
 

タスクのコマンドの結果を中止します。

フィールドのサブフィールド型の値の NDIS\_OID\_要求 Oid NDIS\_OID OID(WDI\_TASK\_SCAN) OutputBufferLength UINT32 sizeof (WDI\_メッセージ\_ヘッダー)WDI を含むメモリ ブロックへの InformationBuffer PVOID ポインター\_メッセージ\_ヘッダー WDI\_メッセージ\_ヘッダー PortId UINT16 0x0001 (例) 予約済み UINT16 N/A WiFiStatus NDIS\_状態 NDIS\_状態\_成功 TransactionId UINT32 0x2222 (例) IhvSpecificId UINT32 該当なし
 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




