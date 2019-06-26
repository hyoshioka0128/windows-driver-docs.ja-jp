---
title: SDP レコードの構築
description: SDP レコードの構築
ms.assetid: ca3c0483-6193-4683-94bb-15466a8f332e
keywords:
- Bluetooth の WDK、SDP サーバー間の通信
- SDP WDK Bluetooth
- サービス探索プロトコルの WDK Bluetooth
- WDK Bluetooth サービスを参照
- WDK Bluetooth サービスを検索
- WDK の Bluetooth の参照サービス
- WDK の Bluetooth の広告サービス
- WDK の Bluetooth の広告サービス
- SdpCreateNodeTree
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 716ea2d15fbf601a69b4c5de85c69dafcc105854
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354023"
---
# <a name="building-sdp-records"></a>SDP レコードの構築


自社のサービスをアドバタイズするプロファイルのドライバーでは、Service Discovery Protocol (SDP) ツリー階層をゼロから構築でき、SDP のレコードのストリームに変換することができます。 まず、プロファイルのドライバーを呼び出す必要があります、 [ **SdpCreateNodeTree** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodetree)関数。 **SdpCreateNodeTree**関数の戻り値を割り当てられた空[ **SDP\_ツリー\_ルート\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdpnode/ns-sdpnode-_sdp_tree_root_node)構造体、プロファイルのドライバーは、次の関数を使用して設定できます。

[**SdpAddAttributeToTree**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpaddattributetotree)

[**SdpAppendNodeToContainerNode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpappendnodetocontainernode)

[**SdpCreateNodeAlternative**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodealternative)

[**SdpCreateNodeBoolean**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodeboolean)

[**SdpCreateNodeInt128**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodeint128)

[**SdpCreateNodeInt16**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodeint16)

[**SdpCreateNodeInt32**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodeint32)

[**SdpCreateNodeInt64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodeint64)

[**SdpCreateNodeInt8**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodeint8)

[**SdpCreateNodeNil**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodenil)

[**SdpCreateNodeSequence**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodesequence)

[**SdpCreateNodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodestring)

[**SdpCreateNodeUInt128**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodeuint128)

[**SdpCreateNodeUInt16**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodeuint16)

[**SdpCreateNodeUInt32**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodeuint32)

[**SdpCreateNodeUInt64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodeuint64)

[**SdpCreateNodeUInt8**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodeuint8)

[**SdpCreateNodeUrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodeurl)

[**SdpCreateNodeUUID128**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodeuuid128)

[**SdpCreateNodeUUID16**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodeuuid16)

[**SdpCreateNodeUUID32**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpcreatenodeuuid32)

プロファイルのドライバーでは、SDP のツリーに基づくレコードの作成が完了すると、呼び出し、 [ **SdpConvertTreeToStream** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthsdpddi/nc-bthsdpddi-pconverttreetostream) SDP レコードの生のバイト ストリーム バージョンを生成する関数。 このフォームで、SDP レコードがプロファイル ドライバーがローカル SDP サーバーにパブリッシュするために準備します。 このプロセスはストリームとして、SDP のレコードを構築するよりも使用するプロファイルのドライバーの方が便利にすることはできます。

**SdpConvertTreeToStream**関数は、SDP のレコードのストリームのバージョンを格納するために必要なメモリを割り当てます。 使用して、メモリが解放する必要がありますプロファイル ドライバーでは、SDP レコードが必要なくなる、 [ **ExFreePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exfreepool)します。

さらに、不要になった、プロファイル ドライバーには、SDP のレコードのツリー ベースのバージョンが必要とするときに呼び出す必要があります[ **SdpFreeTree** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sdplib/nf-sdplib-sdpfreetree)関連付けられている SDP で割り当てられたメモリを解放する\_ツリー\_ルート\_ノード構造体。

プロファイルのドライバーは、すべてのクエリを実行して、このトピックで説明した関数のポインターを取得できます、 [ **BTHDDI\_SDP\_解析\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthsdpddi/ns-bthsdpddi-_bthddi_sdp_parse_interface)と[**BTHDDI\_SDP\_ノード\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthsdpddi/ns-bthsdpddi-_bthddi_sdp_node_interface)インターフェイス。 これらのインターフェイスを照会する方法の詳細については、次を参照してください。 [Bluetooth インターフェイスの照会](querying-for-bluetooth-interfaces.md)します。

 

 





