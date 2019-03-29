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
ms.openlocfilehash: 39b49ae2fa41719fd0195dce0f5f5320d5d52c4a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582554"
---
# <a name="building-sdp-records"></a>SDP レコードの構築


自社のサービスをアドバタイズするプロファイルのドライバーでは、Service Discovery Protocol (SDP) ツリー階層をゼロから構築でき、SDP のレコードのストリームに変換することができます。 まず、プロファイルのドライバーを呼び出す必要があります、 [ **SdpCreateNodeTree** ](https://msdn.microsoft.com/library/windows/hardware/ff536818)関数。 **SdpCreateNodeTree**関数の戻り値を割り当てられた空[ **SDP\_ツリー\_ルート\_ノード**](https://msdn.microsoft.com/library/windows/hardware/ff536851)構造体、プロファイルのドライバーは、次の関数を使用して設定できます。

[**SdpAddAttributeToTree**](https://msdn.microsoft.com/library/windows/hardware/ff536784)

[**SdpAppendNodeToContainerNode**](https://msdn.microsoft.com/library/windows/hardware/ff536786)

[**SdpCreateNodeAlternative**](https://msdn.microsoft.com/library/windows/hardware/ff536798)

[**SdpCreateNodeBoolean**](https://msdn.microsoft.com/library/windows/hardware/ff536801)

[**SdpCreateNodeInt128**](https://msdn.microsoft.com/library/windows/hardware/ff536802)

[**SdpCreateNodeInt16**](https://msdn.microsoft.com/library/windows/hardware/ff536804)

[**SdpCreateNodeInt32**](https://msdn.microsoft.com/library/windows/hardware/ff536806)

[**SdpCreateNodeInt64**](https://msdn.microsoft.com/library/windows/hardware/ff536808)

[**SdpCreateNodeInt8**](https://msdn.microsoft.com/library/windows/hardware/ff536811)

[**SdpCreateNodeNil**](https://msdn.microsoft.com/library/windows/hardware/ff536812)

[**SdpCreateNodeSequence**](https://msdn.microsoft.com/library/windows/hardware/ff536814)

[**SdpCreateNodeString**](https://msdn.microsoft.com/library/windows/hardware/ff536816)

[**SdpCreateNodeUInt128**](https://msdn.microsoft.com/library/windows/hardware/ff536819)

[**SdpCreateNodeUInt16**](https://msdn.microsoft.com/library/windows/hardware/ff536822)

[**SdpCreateNodeUInt32**](https://msdn.microsoft.com/library/windows/hardware/ff536824)

[**SdpCreateNodeUInt64**](https://msdn.microsoft.com/library/windows/hardware/ff536827)

[**SdpCreateNodeUInt8**](https://msdn.microsoft.com/library/windows/hardware/ff536828)

[**SdpCreateNodeUrl**](https://msdn.microsoft.com/library/windows/hardware/ff536831)

[**SdpCreateNodeUUID128**](https://msdn.microsoft.com/library/windows/hardware/ff536833)

[**SdpCreateNodeUUID16**](https://msdn.microsoft.com/library/windows/hardware/ff536835)

[**SdpCreateNodeUUID32**](https://msdn.microsoft.com/library/windows/hardware/ff536836)

プロファイルのドライバーでは、SDP のツリーに基づくレコードの作成が完了すると、呼び出し、 [ **SdpConvertTreeToStream** ](https://msdn.microsoft.com/library/windows/hardware/ff536796) SDP レコードの生のバイト ストリーム バージョンを生成する関数。 このフォームで、SDP レコードがプロファイル ドライバーがローカル SDP サーバーにパブリッシュするために準備します。 このプロセスはストリームとして、SDP のレコードを構築するよりも使用するプロファイルのドライバーの方が便利にすることはできます。

**SdpConvertTreeToStream**関数は、SDP のレコードのストリームのバージョンを格納するために必要なメモリを割り当てます。 使用して、メモリが解放する必要がありますプロファイル ドライバーでは、SDP レコードが必要なくなる、 [ **ExFreePool**](https://msdn.microsoft.com/library/windows/hardware/ff544590)します。

さらに、不要になった、プロファイル ドライバーには、SDP のレコードのツリー ベースのバージョンが必要とするときに呼び出す必要があります[ **SdpFreeTree** ](https://msdn.microsoft.com/library/windows/hardware/ff536839)関連付けられている SDP で割り当てられたメモリを解放する\_ツリー\_ルート\_ノード構造体。

プロファイルのドライバーは、すべてのクエリを実行して、このトピックで説明した関数のポインターを取得できます、 [ **BTHDDI\_SDP\_解析\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff536636)と[**BTHDDI\_SDP\_ノード\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff536635)インターフェイス。 これらのインターフェイスを照会する方法の詳細については、次を参照してください。 [Bluetooth インターフェイスの照会](querying-for-bluetooth-interfaces.md)します。

 

 





