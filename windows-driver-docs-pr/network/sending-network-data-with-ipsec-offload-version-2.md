---
title: IPsec Offload Version 2 によるネットワーク データの送信
description: IPsec Offload Version 2 によるネットワーク データの送信
ms.assetid: d3580313-a98b-4150-b344-e3e395ce68e9
keywords:
- IPsecOV2 WDK TCP/IP トランスポートは、データを送信します。
- WDK ネットワークのデータを送信します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb98bbf7cab9961e7d5c2361a763a4ec9ed91234
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346747"
---
# <a name="sending-network-data-with-ipsec-offload-version-2"></a>IPsec Offload Version 2 によるネットワーク データの送信

\[IPsec タスク オフロード機能は非推奨し、は使用できません。\]




TCP/IP トランスポートは、1 つ以上の SAs を IPsec オフロード バージョン 2 (IPsecOV2) 情報を提供します、 [OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_の追加。\_SA](https://msdn.microsoft.com/library/windows/hardware/ff569812) OID。 ミニポートする前にドライバーは OID の成功した結果を返します\_TCP\_タスク\_IPSEC\_オフロード\_V2\_追加\_SA、ミニポート ドライバー、オフロードを初期化します処理します。 TCP/IP トランスポートは要求の処理をオフロードするミニポート ドライバー、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388) でIPsecOV2情報を指定することによって構造[ **NDIS\_IPSEC\_オフロード\_V2\_NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff565818)と[ **NDIS\_IPSEC\_オフロード\_V2\_ヘッダー\_NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff565812)に含まれる構造体の**NET\_バッファー\_一覧**アウト オブ バンド (OOB) の情報。

TCP/IP トランスポートは、オフロードのハンドルを提供、 **OffloadHandle**のメンバー [ **NDIS\_IPSEC\_オフロード\_V2\_NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff565818)トランスポート (エンド ツー エンド接続) 部分では、送信パケットの送信のセキュリティ アソシエーション (SA) を識別するハンドルを指定します。

TCP/IP トランスポートでは、次のヘッダー情報を提供する、 [ **NDIS\_IPSEC\_オフロード\_V2\_ヘッダー\_NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff565812)構造体。

-   ヘッダーは、AH ヘッダー、ESP ヘッダー、またはその両方のオフセットします。

-   [次へ] プロトコルの値 (ESP トレーラーが含まれているのと同じです)。

-   結合の大量送信オフロード (LSO) と IPsec オフロードを使用する埋め込み長さです。

また、送信パケットが、トンネルを通じて送信される、TCP/IP トランスポートは提供、 [ **NDIS\_IPSEC\_オフロード\_V2\_トンネル\_NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff565843)構造体。 この構造体には、トンネル部分では、送信パケットの送信、SA のオフロード ハンドルを指定します。 OOB の情報にアクセスする方法の詳細については、次を参照してください。[にアクセスする NET\_バッファー\_一覧については、IPsec オフロード バージョン 2 で](accessing-net-buffer-list-information-in-ipsec-offload-version-2.md)します。

ミニポート ドライバー提供の OID セット要求への応答でオフロード ハンドル[OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_追加\_SA](https://msdn.microsoft.com/library/windows/hardware/ff569812). SAs の詳細については、次を参照してください。 [IPsec オフロード バージョン 2 のセキュリティ アソシエーションを管理する](managing-security-associations-in-ipsec-offload-version-2.md)します。

ミニポート ドライバーでの送信要求を処理するときに、 [ *MiniportSendNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff559440)関数では、ミニポート ドライバー。

-   IPsec オフロード サービスを処理するために、ハードウェアが構成されていることを確認します。 IPsec オフロード サービスを処理するために、ハードウェアが構成されていない場合、ミニポート ドライバーは、オフロード サービスを提供することがなく送信要求を処理する必要があります。

-   検証でハンドル、 [ **NDIS\_IPSEC\_オフロード\_V2\_NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff565818)と[ **NDIS\_IPSEC\_オフロード\_V2\_トンネル\_NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff565843) IPsec の暗号化処理が必要なかどうかを判断する構造体。 ゼロのオフロード ハンドル値を示しますの IPsec タスク オフロードを実行しない必要があります、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)します。 送信パケットが失敗し、ミニポート ドライバーが指定したオフロード ハンドルに対応する、オフロードされた SA を見つけられない場合、 **NDIS\_状態\_エラー**値。

-   検証でハンドル、 [ **NDIS\_TCP\_LARGE\_送信\_オフロード\_NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff567882)のセグメント化オフロードを実行するかどうかを決定する構造体、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)します。

-   送信パケットのすべての必要な AH と ESP の処理が完了すると、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)します。 NIC は、IPsec の送信パケットの処理を実行するときは、パケット データの暗号操作を実行します。 TCP/IP トランスポートをパケットのフレームは既にし (必要に応じて)、パディングし、シーケンス番号とセキュリティ パラメーター インデックス (SPI) が割り当てられては。 結合された LSO と IPsec オフロード用、 [ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376) NIC セグメントの大きなパケット、破棄は余白があります。 余白が指定された、 **PadLength**のメンバー、 [ **NDIS\_IPSEC\_オフロード\_V2\_ヘッダー\_NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff565812)構造体。 セグメント化されたパケットには、IPsec の操作をサポートするためにパディングが必要です。

プロトコル ドライバーは、LSO と IPsecOV2 の両方を要求するパケットを送信する、ときに、ESP トレーラーを土台されません。 これは、ESP トレーラー、パディングの長さなどの情報は NIC によって生成された最後のセグメントの正確なされないためです。

 

 





