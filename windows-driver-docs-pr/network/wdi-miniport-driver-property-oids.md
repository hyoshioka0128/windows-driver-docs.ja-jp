---
title: WDI プロパティ OID
description: このセクションには、WDI プロパティ Oid にはが含まれています。
ms.assetid: 1B1B54B8-6CE4-4C17-AAF8-7394210B09E8
ms.date: 07/18/2017
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 4165572608ab4c6ca2b722b9d3f17017b22b35a8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385368"
---
# <a name="wdi-property-oids"></a>WDI プロパティ OID


このセクションには、WDI プロパティ Oid にはが含まれています。

Wi-fi ドライバー インターフェイス (WDI) のオブジェクト識別子 (Oid) は、WDI を実装するミニポート ドライバーにのみ適用されます。

次の表とを指定するかどうか WDI OID クエリ (Q)、セット (S) NDIS 6.0 メソッド (M) 要求必須またはオプションを実装します。

<a href="" id="r"></a>**R**  
オブジェクトが必要です。 サポートすることを示します。 ミニポート ドライバー NDIS 状態コードを返すことによって、オブジェクトのセットまたはクエリの要求を失敗する必要がありますしない\_状態\_いない\_からサポートされているその[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)関数。

<a href="" id="o"></a>**O**  
オブジェクトは省略可能なサポートすることを示します。 NDIS を返すことによって、要求は失敗は、ドライバーまたはミニポート ドライバーのクエリをサポートまたは、オブジェクトの要求を設定できます\_状態\_いない\_からサポートされているその[ *MiniportOidRequest*](https://msdn.microsoft.com/library/windows/hardware/ff559416)関数。

| 名前                                                                                                | Q   | S   | M   |
|-----------------------------------------------------------------------------------------------------|-----|-----|-----|
| [OID\_WDI\_中止\_タスク](oid-wdi-abort-task.md)                                                     |     |     | R   |
| [OID\_WDI\_取得\_アダプター\_機能](oid-wdi-get-adapter-capabilities.md)                        |     |     | R   |
| [OID\_WDI\_取得\_自動\_POWER\_保存](oid-wdi-get-auto-power-save.md)                                 |     |     | R   |
| [OID\_WDI\_取得\_BSS\_エントリ\_一覧](oid-wdi-get-bss-entry-list.md)                                   |     |     | O   |
| [OID\_WDI\_GET\_NEXT\_ACTION\_FRAME\_DIALOG\_TOKEN](oid-wdi-get-next-action-frame-dialog-token.md) |     |     | O   |
| [OID\_WDI\_取得\_PM\_プロトコル\_オフロード](oid-wdi-get-pm-protocol-offload.md)                         |     |     | O   |
| [OID\_WDI\_取得\_受信\_COALESCING\_一致\_数](oid-wdi-get-receive-coalescing-match-count.md)  |     |     | O   |
| [OID\_WDI\_取得\_統計情報](oid-wdi-get-statistics.md)                                             |     |     | R   |
| [OID\_WDI\_IHV\_要求](oid-wdi-ihv-request.md)                                                   |     |     | O   |
| [OID\_WDI\_SET\_ADAPTER\_CONFIGURATION](oid-wdi-set-adapter-configuration.md)                      |     |     | R   |
| [OID\_WDI\_設定\_追加\_暗号\_キー](oid-wdi-set-add-cipher-keys.md)                                 |     |     | R   |
| [OID\_WDI\_設定\_追加\_PM\_プロトコル\_オフロード](oid-wdi-set-add-pm-protocol-offload.md)                |     |     | O   |
| [OID\_WDI\_設定\_追加\_WOL\_パターン](oid-wdi-set-add-wol-pattern.md)                                 |     |     | O   |
| [OID\_WDI\_設定\_広告\_情報](oid-wdi-set-advertisement-information.md)              |     |     | O   |
| [OID\_WDI\_設定\_アソシエーション\_パラメーター](oid-wdi-set-association-parameters.md)                    |     |     | R   |
| [OID\_WDI\_設定\_クリア\_受信\_COALESCING](oid-wdi-set-clear-receive-coalescing.md)               |     |     | O   |
| [OID\_WDI\_設定\_接続\_品質](oid-wdi-set-connection-quality.md)                            |     |     | R   |
| [OID\_WDI\_設定\_既定\_キー\_ID](oid-wdi-set-default-key-id.md)                                   |     |     | R   |
| [OID\_WDI\_設定\_削除\_暗号\_キー](oid-wdi-set-delete-cipher-keys.md)                           |     |     | R   |
| [OID\_WDI\_設定\_カプセル化\_オフロード](oid-wdi-set-encapsulation-offload.md)                      |     |     | O   |
| [OID\_WDI\_設定\_フラッシュ\_BSS\_エントリ](oid-wdi-set-flush-bss-entry.md)                                 |     |     | O   |
| [OID\_WDI\_設定\_マルチキャスト\_一覧](oid-wdi-set-multicast-list.md)                                    |     |     | R   |
| [OID\_WDI\_SET\_NETWORK\_LIST\_OFFLOAD](oid-wdi-set-network-list-offload.md)                       |     |     | O   |
| [OID\_WDI\_SET\_P2P\_LISTEN\_STATE](oid-wdi-set-p2p-listen-state.md)                               |     |     | O   |
| [OID\_WDI\_設定\_P2P\_開始\_バック グラウンド\_検出](oid-wdi-set-p2p-start-background-discovery.md)  |     |     | O   |
| [OID\_WDI\_設定\_P2P\_停止\_バック グラウンド\_検出](oid-wdi-set-p2p-stop-background-discovery.md)    |     |     | O   |
| [OID\_WDI\_SET\_P2P\_WPS\_ENABLED](oid-wdi-set-p2p-wps-enabled.md)                                 |     |     | O   |
| [OID\_WDI\_設定\_POWER\_状態](oid-wdi-set-power-state.md)                                          |     |     | R   |
| [OID\_WDI\_SET\_PRIVACY\_EXEMPTION\_LIST](oid-wdi-set-privacy-exemption-list.md)                   |     |     | R   |
| [OID\_WDI\_設定\_受信\_COALESCING](oid-wdi-set-receive-coalescing.md)                            |     |     | O   |
| [OID\_WDI\_設定\_受信\_パケット\_フィルター](oid-wdi-set-receive-packet-filter.md)                     |     |     | R   |
| [OID\_WDI\_設定\_削除\_PM\_プロトコル\_オフロード](oid-wdi-set-remove-pm-protocol-offload.md)          |     |     | O   |
| [OID\_WDI\_設定\_削除\_WOL\_パターン](oid-wdi-set-remove-wol-pattern.md)                           |     |     | O   |
| [OID_WDI_SET_SAE_AUTH_PARAMS](oid-wdi-set-sae-auth-params.md)                                      |     |     | O   |
| [OID\_WDI\_設定\_TCP\_オフロード\_パラメーター](oid-wdi-set-tcp-offload-parameters.md)                   |     |     | O   |
| [OID\_WDI\_TCP\_RSC\_STATISTICS](oid-wdi-tcp-rsc-statistics.md)                                    |     |     | O   |

 

 

 




