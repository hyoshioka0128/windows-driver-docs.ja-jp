---
title: SDP レコードのツリー構造への変換
description: SDP レコードのツリー構造への変換
ms.assetid: 762cf68b-0082-4b9e-8f24-ff19ecf6f8bd
keywords:
- Bluetooth の WDK、SDP サーバー間の通信
- SDP WDK Bluetooth
- サービス探索プロトコルの WDK Bluetooth
- WDK Bluetooth サービスを参照
- WDK Bluetooth サービスを検索
- WDK の Bluetooth の参照サービス
- SDP レコードの変換
- SDP レコード WDK Bluetooth からツリー構造
- SdpConvertStreamToTree
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f0d7e6ffd12a1b3fdfdd5ab07c295d384e77f65
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354017"
---
# <a name="converting-sdp-records-to-a-tree-structure"></a>SDP レコードのツリー構造への変換


サービス探索プロトコル (SDP) レコードは、複雑なバイナリ ストリームにエンコードされます。 SDP レコードの詳細についてを解析するプロファイルのドライバーを有効にするには、Bluetooth ドライバー スタックの実現も簡単プロファイル ドライバーが、SDP のレコードのストリームを階層ツリー構造に変換し、再び使用できる関数の数。

プロファイルのクライアント ドライバーを使用できる、 [ **SdpConvertStreamToTree** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthsdpddi/nc-bthsdpddi-pconvertstreamtotree)ツリー構造、SDP のレコードに変換する関数。 呼び出し元に起因する SDP レコードのツリー表現、 **SdpConvertStreamToTree** SDP のレコードに関連付けられているすべての情報が含まれるルート ノードで構成される関数によって定義された、 [ **SDP\_ツリー\_ルート\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdpnode/ns-sdpnode-_sdp_tree_root_node)構造体。 ルート ノードには一連の相互接続された[ **SDP\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdpnode/ns-sdpnode-_sdp_node) SDP の 1 つの属性に関する情報を含む構造体。

各 SDP\_ノード構造に含まれる、 [ **SDP\_ノード\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdpnode/ns-sdpnode-_sdp_node_header)構造と[ **SDP\_ノード\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdpnode/ns-sdpnode-_sdp_node_data)共用体。 ヘッダーの構造は、ノードに含まれるデータの種類を指定します。 プロファイルのドライバーの使用、 [**一覧\_エントリ**](https://docs.microsoft.com/windows/desktop/api/ntdef/ns-ntdef-_list_entry) SDP をピアへのリンクにアクセスする構造体\_ノード構造体。 SDP を使用して\_ノード構造体の**hdr します。Link.Flink**と**hdr します。Link.Blink** 、メンバー プロファイル ドライバーは、ツリー内のピア ノードのアドレスを取得できます。 一覧に注意してください\_エントリのポインターをその他の一覧にアドレスを保持する\_エントリの構造体、およびプロファイルのドライバーを使用する必要があります、 [**含まれている\_レコード**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)ノードのレコードが含まれるアドレスを抽出するマクロ。 詳細については、次を参照してください。、 [ **SdpConvertStreamToTree** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthsdpddi/nc-bthsdpddi-pconvertstreamtotree)トピック。

SDP レコードのストリームをツリー表現に変換すると、プロファイルのドライバーを呼び出すことが、 [ **SdpFindAttributeInTree** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpfindattributeintree)ツリー内の指定したノードのアドレスを取得します。

プロファイルのドライバーは、すべてのクエリを実行して、このトピックで説明した関数のポインターを取得できます、 [ **BTHDDI\_SDP\_解析\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthsdpddi/ns-bthsdpddi-_bthddi_sdp_parse_interface)と[**BTHDDI\_SDP\_ノード\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthsdpddi/ns-bthsdpddi-_bthddi_sdp_node_interface)インターフェイス。 これらのインターフェイスを照会する方法の詳細については、次を参照してください。 [Bluetooth インターフェイスの照会](querying-for-bluetooth-interfaces.md)します。

 

 





