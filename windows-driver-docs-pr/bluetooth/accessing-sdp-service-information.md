---
title: SDP サービス情報へのアクセス
description: SDP サービス情報へのアクセス
ms.assetid: 0b327fbd-1101-4566-ac2f-3d039eed6835
keywords:
- Bluetooth の WDK、SDP サーバー間の通信
- SDP WDK Bluetooth
- サービス探索プロトコルの WDK Bluetooth
- WDK Bluetooth サービスを参照
- WDK Bluetooth サービスを検索
- WDK の Bluetooth の参照サービス
- IOCTL_BTH_SDP_CONNECT
- レコード WDK Bluetooth を SDP を検索
- IOCTL_BTH_SDP_SERVICE_SEARCH
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc4e5ad7cffd8493468853e7e6bd0f0ba6b6fe97
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581994"
---
# <a name="accessing-sdp-service-information"></a>SDP サービス情報へのアクセス


プロファイルのドライバーが SDP でそのサービスを提供するサービスの探索プロトコル (SDP) レコードを送信した後、他のデバイスは、具体的には、レコードのいずれかを検索して、または検索を参照してこれらのサービスを検出できます。

SDP レコードを検索するクライアント プロファイルのドライバーを使用する必要がありますまず[ **IOCTL\_両方\_SDP\_CONNECT** ](https://msdn.microsoft.com/library/windows/hardware/ff536688)リモート デバイスの SDP サービスに接続します。

実際の SDP レコードの検索を実行するのに Ioctl を次のいずれかのプロファイル ドライバーを使用し、ことができます。

-   [**IOCTL\_両方\_SDP\_属性\_検索**](https://msdn.microsoft.com/library/windows/hardware/ff536687) SDP 属性の指定した範囲に分類されるリモート SDP レコードのすべてのコンポーネントを取得します。

-   [**IOCTL\_両方\_SDP\_サービス\_検索**](https://msdn.microsoft.com/library/windows/hardware/ff536692) SDP レコードの特定のサービス クラスまたはクラスへのハンドルを要求して、リモート デバイスに、SDP の要求を発行します。

-   [**IOCTL\_両方\_SDP\_サービス\_属性\_検索**](https://msdn.microsoft.com/library/windows/hardware/ff536691) IOCTL を組み合わせた\_両方\_SDP\_属性\_検索と IOCTL\_両方\_SDP\_サービス\_属性\_検索と使用可能な SDP レコードが 1 回の操作でストリームを返します。

プロファイルのドライバーは、IOCTL を使用できます\_両方\_SDP\_サービス\_検索と IOCTL\_両方\_SDP\_属性\_SDP トラフィックの量を減らす検索Bluetooth のリンクを経由して送信され、最大転送単位 (Mtu) の数が少ないを使用して、必要な情報を抽出することができます。 大きな懸念のこれらの問題のどちらでもない場合は、プロファイルのドライバーを IOCTL を呼び出す方が便利できます\_両方\_SDP\_サービス\_属性\_検索します。

ドライバーは取得した後、プロファイル、*動的*プロトコル/サービスの目的のサービスのマルチプレクサー (PSM) を使用して、リモート サービスに接続できる、 **BRB\_L2CA\_を開く\_チャネル**BRB します。

**注**  場合は、サービスがあるどの多には、固定 2.1.X L2CAP クライアント プロファイルのドライバーが、SDP を使用して、PSM を取得する必要はありません。 ただし、L2CAP クライアント プロファイルのドライバーが、SDP のサーバー属性を取得するのに SDP を引き続き使用することができます。

 

使用するプロファイルのドライバーでは、検索が完了したら、 [ **IOCTL\_両方\_SDP\_切断**](https://msdn.microsoft.com/library/windows/hardware/ff536689) SDP のリモート サーバーから切断します。

 

 





