---
title: WDI プロパティ OID
description: このセクションには、WDI プロパティ Oid が含まれています。
ms.assetid: 1B1B54B8-6CE4-4C17-AAF8-7394210B09E8
ms.date: 07/18/2017
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: dc215bc96c813c97b372f125d07f0110df6768e7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842917"
---
# <a name="wdi-property-oids"></a>WDI プロパティ OID


このセクションには、WDI プロパティ Oid が含まれています。

Wi-fi Driver Interface (WDI) オブジェクト識別子 (Oid) は、WDI を実装するミニポートドライバーにのみ適用されます。

次の表では、WDI OID query (Q)、set (S)、および NDIS 6.0 method (M) 要求を実装するかどうかを指定します。

<a href="" id="r"></a> **\R\n\r\n**  
オブジェクトのサポートが必要であることを示します。 ミニポートドライバーは、 [*Miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)関数からサポートされて\_いない状態コード NDIS\_status\_返すことによって、オブジェクトの設定またはクエリ要求に失敗しないようにする必要があります。

<a href="" id="o"></a>**I/o**  
オブジェクトのサポートが省略可能であることを示します。 ミニポートドライバーは、オブジェクトのクエリまたは設定要求をサポートすることができます。または、ドライバーが、[*ミニ Portoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)関数からサポートされて\_いない NDIS\_ステータス\_を返すことによって要求を失敗させることができます。

| 名前                                                                                                | Q   | S   | [M]   |
|-----------------------------------------------------------------------------------------------------|-----|-----|-----|
| [OID\_WDI\_ABORT\_タスク](oid-wdi-abort-task.md)                                                     |     |     | R   |
| [OID\_WDI\_\_アダプターの\_機能を取得する](oid-wdi-get-adapter-capabilities.md)                        |     |     | R   |
| [OID\_WDI\_\_自動\_POWER\_保存](oid-wdi-get-auto-power-save.md)                                 |     |     | R   |
| [OID\_WDI\_\_BSS\_エントリ\_リストを取得します。](oid-wdi-get-bss-entry-list.md)                                   |     |     | O   |
| [OID\_WDI\_GET\_NEXT\_ACTION\_FRAME\_DIALOG\_TOKEN](oid-wdi-get-next-action-frame-dialog-token.md) |     |     | O   |
| [OID\_WDI\_取得\_PM\_プロトコル\_オフロード](oid-wdi-get-pm-protocol-offload.md)                         |     |     | O   |
| [OID\_WDI\_取得\_受信\_結合\_カウント\_照合](oid-wdi-get-receive-coalescing-match-count.md)  |     |     | O   |
| [OID\_WDI\_\_統計情報の取得](oid-wdi-get-statistics.md)                                             |     |     | R   |
| [OID\_WDI\_IHV\_要求](oid-wdi-ihv-request.md)                                                   |     |     | O   |
| [OID\_WDI\_設定\_アダプター\_構成](oid-wdi-set-adapter-configuration.md)                      |     |     | R   |
| [OID\_WDI\_設定\_\_暗号\_キーの追加](oid-wdi-set-add-cipher-keys.md)                                 |     |     | R   |
| [OID\_WDI\_設定\_\_PM\_プロトコル\_オフロード](oid-wdi-set-add-pm-protocol-offload.md)                |     |     | O   |
| [OID\_WDI\_設定\_\_WOL\_パターンの追加](oid-wdi-set-add-wol-pattern.md)                                 |     |     | O   |
| [OID\_WDI\_設定\_開示通知\_情報](oid-wdi-set-advertisement-information.md)              |     |     | O   |
| [OID\_WDI\_SET\_ASSOCIATION\_パラメーター](oid-wdi-set-association-parameters.md)                    |     |     | R   |
| [OID\_WDI\_SET\_CLEAR\_RECEIVE\_合体](oid-wdi-set-clear-receive-coalescing.md)               |     |     | O   |
| [OID\_WDI\_設定\_接続\_品質](oid-wdi-set-connection-quality.md)                            |     |     | R   |
| [OID\_WDI\_設定\_既定の\_キー\_ID](oid-wdi-set-default-key-id.md)                                   |     |     | R   |
| [OID\_WDI\_設定\_\_暗号\_キーの削除](oid-wdi-set-delete-cipher-keys.md)                           |     |     | R   |
| [OID\_WDI\_SET\_のカプセル化\_オフロード](oid-wdi-set-encapsulation-offload.md)                      |     |     | O   |
| [OID\_WDI\_SET\_FLUSH\_BSS\_ENTRY](oid-wdi-set-flush-bss-entry.md)                                 |     |     | O   |
| [OID\_WDI\_設定\_マルチキャスト\_リスト](oid-wdi-set-multicast-list.md)                                    |     |     | R   |
| [OID\_WDI\_設定\_ネットワーク\_リスト\_オフロード](oid-wdi-set-network-list-offload.md)                       |     |     | O   |
| [OID\_WDI\_設定\_P2P\_リッスン\_状態](oid-wdi-set-p2p-listen-state.md)                               |     |     | O   |
| [OID\_WDI\_設定\_P2P\_開始\_バックグラウンド\_検出](oid-wdi-set-p2p-start-background-discovery.md)  |     |     | O   |
| [OID\_WDI\_SET\_P2P\_STOP\_バックグラウンド\_検出](oid-wdi-set-p2p-stop-background-discovery.md)    |     |     | O   |
| [OID\_WDI\_設定\_P2P\_WPS\_有効](oid-wdi-set-p2p-wps-enabled.md)                                 |     |     | O   |
| [OID\_WDI\_設定\_電源\_状態](oid-wdi-set-power-state.md)                                          |     |     | R   |
| [OID\_WDI\_設定\_プライバシー\_除外対象\_一覧](oid-wdi-set-privacy-exemption-list.md)                   |     |     | R   |
| [OID\_WDI\_SET\_受信\_合体](oid-wdi-set-receive-coalescing.md)                            |     |     | O   |
| [OID\_WDI\_SET\_受信\_パケット\_フィルター](oid-wdi-set-receive-packet-filter.md)                     |     |     | R   |
| [OID\_WDI\_設定\_削除\_PM\_プロトコル\_オフロード](oid-wdi-set-remove-pm-protocol-offload.md)          |     |     | O   |
| [OID\_WDI\_設定\_\_WOL\_パターンの削除](oid-wdi-set-remove-wol-pattern.md)                           |     |     | O   |
| [OID_WDI_SET_SAE_AUTH_PARAMS](oid-wdi-set-sae-auth-params.md)                                      |     |     | O   |
| [OID\_WDI\_設定\_TCP\_オフロード\_パラメーター](oid-wdi-set-tcp-offload-parameters.md)                   |     |     | O   |
| [OID\_WDI\_TCP\_RSC\_の統計情報](oid-wdi-tcp-rsc-statistics.md)                                    |     |     | O   |

 

 

 




