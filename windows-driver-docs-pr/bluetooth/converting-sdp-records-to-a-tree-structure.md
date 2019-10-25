---
title: SDP レコードのツリー構造への変換
description: SDP レコードのツリー構造への変換
ms.assetid: 762cf68b-0082-4b9e-8f24-ff19ecf6f8bd
keywords:
- Bluetooth WDK、SDP サーバー通信
- SDP WDK Bluetooth
- サービス検出プロトコル WDK Bluetooth
- サービスの参照 (WDK) Bluetooth
- サービスの検索 WDK Bluetooth
- サービス閲覧 WDK Bluetooth
- SDP レコードの変換
- SDP レコードからのツリー構造 WDK Bluetooth
- SdpConvertStreamToTree
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfea61df8d5f8561f42b9411176528326331df9e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833871"
---
# <a name="converting-sdp-records-to-a-tree-structure"></a>SDP レコードのツリー構造への変換


サービス検出プロトコル (SDP) レコードは、複雑なバイナリストリームでエンコードされます。 プロファイルドライバーが SDP レコードをより簡単に解析できるようにするために、Bluetooth ドライバースタックには、プロファイルドライバーが SDP レコードストリームを階層ツリー構造に変換して戻すために使用できる多数の関数が用意されています。

クライアントプロファイルドライバーは、 [**Sdpconvertstreamtotree**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthsdpddi/nc-bthsdpddi-pconvertstreamtotree)関数を使用して、SDP レコードをツリー構造に変換できます。 **Sdpconvertstreamtotree**関数を呼び出した結果として得られる sdp レコードのツリー表現は、SDP [ **\_ツリー\_ルートによって定義される、sdp レコードに関連付けられているすべての情報を含むルートノードで構成され\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdpnode/ns-sdpnode-_sdp_tree_root_node)構造。 ルートノードには、一連の相互接続された[**sdp\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdpnode/ns-sdpnode-_sdp_node)構造が含まれており、それぞれに1つの sdp 属性に関する情報が含まれています。

各 SDP\_ノード構造には、 [**sdp\_ノード\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdpnode/ns-sdpnode-_sdp_node_header)構造と、 [**sdp\_ノード\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdpnode/ns-sdpnode-_sdp_node_data)共用体が含まれています。 ヘッダー構造は、ノードに格納されているデータの型を指定します。 プロファイルドライバーは、 [**LIST\_ENTRY**](https://docs.microsoft.com/windows/desktop/api/ntdef/ns-ntdef-_list_entry)構造体を使用して、ピア SDP\_ノード構造へのリンクにアクセスします。 SDP\_ノード構造の hdr を使用し**ます。Flink**と hdr をリンクします。 **リンク. 点滅**するメンバー、プロファイルドライバーは、ツリー内のピアノードのアドレスを取得できます。 \_エントリポインターは、他のリスト\_エントリの構造体のアドレスを保持します。また、プロファイルドライバーは、含んでいる[ **\_レコード**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)マクロを使用して、ノードレコードを含むアドレスを抽出する必要があることに注意してください。 詳細については、 [**Sdpconvertstreamtotree**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthsdpddi/nc-bthsdpddi-pconvertstreamtotree)のトピックを参照してください。

SDP レコードストリームがツリー表現に変換された後、プロファイルドライバーは[**SdpFindAttributeInTree**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpfindattributeintree)関数を呼び出して、ツリー内の指定したノードのアドレスを取得できます。

プロファイルドライバーは、このトピックで説明されているすべての関数へのポインターを取得できます。そのためには、 [**bthddi\_sdp\_PARSE\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthsdpddi/ns-bthsdpddi-_bthddi_sdp_parse_interface)と[**bthddi\_SDP\_NODE\_INTERFACE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthsdpddi/ns-bthsdpddi-_bthddi_sdp_node_interface)インターフェイスを照会します。 これらのインターフェイスのクエリを実行する方法の詳細については、「 [Bluetooth インターフェイスの](querying-for-bluetooth-interfaces.md)クエリ」を参照してください。

 

 





