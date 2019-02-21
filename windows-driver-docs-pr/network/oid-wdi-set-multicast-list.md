---
title: OID_WDI_SET_MULTICAST_LIST
description: OID_WDI_SET_MULTICAST_LIST には、特定のポートのマルチキャスト アドレスの一覧を指定します。 このコマンドは、いつでも設定できます。
ms.assetid: dee41a49-2be2-4364-877c-b2b3bf29e78d
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_MULTICAST_LIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: f82501e01636fc6ec5f6be436dbd6abd15a59003
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538656"
---
# <a name="oidwdisetmulticastlist"></a>OID\_WDI\_設定\_マルチキャスト\_一覧


OID\_WDI\_設定\_マルチキャスト\_リスト、特定のポートのマルチキャスト アドレスの一覧を指定します。 このコマンドは、いつでも設定できます。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | 〇                      | 1                               |

 

IHV コンポーネントがリストのサイズがで指定された制限を超えた場合のコマンドは、失敗のみ[ **WDI\_TLV\_インターフェイス\_属性**](https://msdn.microsoft.com/library/windows/hardware/dn897835)します。

マルチキャスト パケットのポートを使用して、フィルタ リングを有効にすた後ホスト[OID\_WDI\_設定\_受信\_パケット\_フィルター](oid-wdi-set-receive-packet-filter.md)デバイスが受信を指定する必要がありますホストにポートのマルチキャスト リスト内のアドレスに一致する宛先アドレスでマルチキャスト フレーム。 デバイスの処理の一環として、マルチキャストの一覧をオフにする必要があります[OID\_WDI\_タスク\_DOT11\_リセット](oid-wdi-task-dot11-reset.md)します。 指定したマルチキャスト リストのコマンドが送信されると、ドライバーは、そのマルチキャストの一覧をクリアする必要があります。 この場合、パケットは示されませんをしない限り、OID\_WDI\_設定\_受信\_パケット\_フィルターには、WDI\_パケット\_フィルター\_すべて\_マルチキャスト ビット セット。

## <a name="set-property-parameters"></a>プロパティ パラメーターの設定


| TLV                                                              | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                  |
|------------------------------------------------------------------|--------------------------------|----------|--------------------------------------------------------------|
| [**WDI\_TLV\_マルチキャスト\_一覧**](https://msdn.microsoft.com/library/windows/hardware/dn897849) |                                | X        | マルチキャスト MAC の一覧に対処します。 一覧は空にできません。 |

 

## <a name="set-property-results"></a>セットのプロパティの結果


追加データがありません。 ヘッダー内のデータで十分です。
要件
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

 

 




