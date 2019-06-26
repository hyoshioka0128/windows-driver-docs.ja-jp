---
title: 受信パスでの IPsec タスクのオフロード
description: 受信パスでの IPsec タスクのオフロード
ms.assetid: d1dff4fa-7354-4c8c-8591-223c6b524619
keywords:
- WDK IPsec オフロード、ESP により保護されたパケットの受信パスのオフロード
- WDK IPsec オフロード、AH で保護されたパケットの受信パスのオフロード
- パスをオフロード WDK IPsec オフロードします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b19d31dcc8d61ac2efcc7390b9338f90f7db568
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368504"
---
# <a name="offloading-ipsec-tasks-in-the-receive-path"></a>受信パスでの IPsec タスクのオフロード

\[IPsec タスク オフロード機能は非推奨し、は使用できません。\]




NIC は、インターネット プロトコル セキュリティ (IPsec) の受信パケットの処理を実行するときに復号化パケット パケットは、ESP ペイロードが含まれています、AH または ESP 暗号化チェックサム (あるいはその両方) を計算する場合、パケットの。 示す前に、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list) TCP/IP トランスポート、ミニポート ドライバーの呼び出しまでパケットの構造、 [ **NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-info)マクロが、  *\_Id*の**IPsecOffloadV1NetBufferListInfo**を取得する、 [ **NDIS\_IPSEC\_オフロード\_V1\_NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_ipsec_offload_v1_net_buffer_list_info)パケットに関連付けられている構造体。

ミニポート ドライバーのセット、 **CryptoDone** NDIS フラグ\_IPSEC\_オフロード\_V1\_NET\_バッファー\_一覧\_情報構造体NIC が IPsec 受信パケット内の少なくとも 1 つの IPsec ペイロードのチェックを実行することを示します。 ミニポート ドライバーにも設定 NIC は、IPsec の受信パケットのトンネルおよびトランスポートの両方の部分でチェックを実行している場合、 **NextCryptoDone** NDIS フラグ\_IPSEC\_オフロード\_V1\_NET\_バッファー\_一覧\_情報構造体。 ミニポートのドライバー セット**NextCryptoDone**パケット トンネルおよびトランスポートの両方の IPsec ペイロードがある場合のみです。 それ以外の場合、ミニポート ドライバーの設定**NextCryptoDone**をゼロにします。 IPsec チェックの結果を示すために、ミニポート ドライバーする必要がありますも値を指定、 **CryptoStatus** NDIS でメンバー\_IPSEC\_オフロード\_V1\_NET\_バッファー\_一覧\_情報構造体。 かどうか、NIC には、チェックサム エラーまたは暗号化解除エラーが検出された、ミニポート ドライバーが示す必要があります、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)あらゆる形式の受信パケットの構造適切なを指定して**CryptoStatus**値。

注、ミニポート ドライバーは、着信パケットを復号化しないが場合に、消去される両方、 **CryptoDone**と**NextCryptoDone**フラグ。 ミニポート ドライバーでは、これはすべての受信パケットの復号化ではありませんが、パケットは、AH または ESP で保護されているかどうかに関係なく。 ミニポートのドライバー セット**CryptoStatus** CRYPTO に\_成功パケットの解読されません。

ミニポート後は、ドライバーは、NET を示します\_バッファー\_リスト構造体は、TCP/IP トランスポートを実行するには、NIC が、パケットのシーケンス番号をチェックする IPsec チェックの結果を検査と動作を決定します。パケットに対して行うには、チェックサムまたはシーケンス処理のテストが失敗しました。

 

 





