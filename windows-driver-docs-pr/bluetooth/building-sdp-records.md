---
title: SDP レコードの構築
description: SDP レコードの構築
ms.assetid: ca3c0483-6193-4683-94bb-15466a8f332e
keywords:
- Bluetooth WDK、SDP サーバー通信
- SDP WDK Bluetooth
- サービス検出プロトコル WDK Bluetooth
- サービスの参照 (WDK) Bluetooth
- サービスの検索 WDK Bluetooth
- サービス閲覧 WDK Bluetooth
- アドバタイズサービス WDK Bluetooth
- WDK Bluetooth を提供するサービス
- SdpCreateNodeTree
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 217e63ec512fe88797b4794cdffa83b759998774
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832125"
---
# <a name="building-sdp-records"></a>SDP レコードの構築


サービスを提供するプロファイルドライバーは、サービス検出プロトコル (SDP) ツリー階層をゼロから構築し、それを SDP レコードストリームに変換できます。 プロファイルドライバーは、まず[**SdpCreateNodeTree**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodetree)関数を呼び出す必要があります。 **SdpCreateNodeTree**関数は、プロファイルドライバーが次の関数を使用して設定できる、割り当てられた空の[**SDP\_ツリー\_ルート\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdpnode/ns-sdpnode-_sdp_tree_root_node)構造を返します。

[**SdpAddAttributeToTree**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpaddattributetotree)

[**SdpAppendNodeToContainerNode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpappendnodetocontainernode)

[**Sdpcreatの代替**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodealternative)

[**Sdpcreat/Boolean**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeboolean)

[**SdpCreateNodeInt128**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeint128)

[**SdpCreateNodeInt16**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeint16)

[**SdpCreateNodeInt32**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeint32)

[**SdpCreateNodeInt64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeint64)

[**SdpCreateNodeInt8**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeint8)

[**Sdpcreat"Il"** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodenil)

[**Sdpcreatの手順**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodesequence)

[**Sdpcreatの文字列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodestring)

[**SdpCreateNodeUInt128**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeuint128)

[**SdpCreateNodeUInt16**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeuint16)

[**SdpCreateNodeUInt32**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeuint32)

[**SdpCreateNodeUInt64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeuint64)

[**SdpCreateNodeUInt8**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeuint8)

[**Sdpcreatの Url**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeurl)

[**SdpCreateNodeUUID128**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeuuid128)

[**SdpCreateNodeUUID16**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeuuid16)

[**SdpCreateNodeUUID32**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpcreatenodeuuid32)

プロファイルドライバーは、ツリーベースの SDP レコードの構築を完了した後、 [**Sdpconverttreetostream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthsdpddi/nc-bthsdpddi-pconverttreetostream)関数を呼び出して、sdp レコードの未加工のバイトストリームバージョンを生成します。 この形式では、SDP レコードはプロファイルドライバーがローカル SDP サーバーに発行する準備ができています。 このプロセスは、ストリームとして SDP レコードを構築するよりも、プロファイルドライバーが使用する方が便利です。

**Sdpconverttreetostream**関数は、SDP レコードのストリームバージョンを格納するために必要なメモリを割り当てます。 プロファイルドライバーが SDP レコードを必要としなくなった場合は、 [**Exfreepool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)を使用してメモリを解放する必要があります。

また、プロファイルドライバーが、ツリーベースの SDP レコードのバージョンを必要としなくなった場合は、 [**Sdpfreetree**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sdplib/nf-sdplib-sdpfreetree)を呼び出して、関連付けられている SDP\_ツリー\_ルート\_ノード構造で割り当てられたメモリを解放する必要があります。

プロファイルドライバーは、このトピックで説明されているすべての関数へのポインターを取得できます。そのためには、 [**bthddi\_sdp\_PARSE\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthsdpddi/ns-bthsdpddi-_bthddi_sdp_parse_interface)と[**bthddi\_SDP\_NODE\_INTERFACE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthsdpddi/ns-bthsdpddi-_bthddi_sdp_node_interface)インターフェイスを照会します。 これらのインターフェイスのクエリを実行する方法の詳細については、「 [Bluetooth インターフェイスの](querying-for-bluetooth-interfaces.md)クエリ」を参照してください。

 

 





