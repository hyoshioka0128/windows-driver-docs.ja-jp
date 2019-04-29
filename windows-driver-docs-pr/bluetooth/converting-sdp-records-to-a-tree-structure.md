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
ms.openlocfilehash: 4eb42793abbcef08fe932bf48b9632cb886243e5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328235"
---
# <a name="converting-sdp-records-to-a-tree-structure"></a>SDP レコードのツリー構造への変換


サービス探索プロトコル (SDP) レコードは、複雑なバイナリ ストリームにエンコードされます。 SDP レコードの詳細についてを解析するプロファイルのドライバーを有効にするには、Bluetooth ドライバー スタックの実現も簡単プロファイル ドライバーが、SDP のレコードのストリームを階層ツリー構造に変換し、再び使用できる関数の数。

プロファイルのクライアント ドライバーを使用できる、 [ **SdpConvertStreamToTree** ](https://msdn.microsoft.com/library/windows/hardware/ff536794)ツリー構造、SDP のレコードに変換する関数。 呼び出し元に起因する SDP レコードのツリー表現、 **SdpConvertStreamToTree** SDP のレコードに関連付けられているすべての情報が含まれるルート ノードで構成される関数によって定義された、 [ **SDP\_ツリー\_ルート\_ノード**](https://msdn.microsoft.com/library/windows/hardware/ff536851)構造体。 ルート ノードには一連の相互接続された[ **SDP\_ノード**](https://msdn.microsoft.com/library/windows/hardware/ff536848) SDP の 1 つの属性に関する情報を含む構造体。

各 SDP\_ノード構造に含まれる、 [ **SDP\_ノード\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff536850)構造と[ **SDP\_ノード\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff536849)共用体。 ヘッダーの構造は、ノードに含まれるデータの種類を指定します。 プロファイルのドライバーの使用、 [**一覧\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/ff554296) SDP をピアへのリンクにアクセスする構造体\_ノード構造体。 SDP を使用して\_ノード構造体の**hdr します。Link.Flink**と**hdr します。Link.Blink** 、メンバー プロファイル ドライバーは、ツリー内のピア ノードのアドレスを取得できます。 一覧に注意してください\_エントリのポインターをその他の一覧にアドレスを保持する\_エントリの構造体、およびプロファイルのドライバーを使用する必要があります、 [**含まれている\_レコード**](https://msdn.microsoft.com/library/windows/hardware/ff542043)ノードのレコードが含まれるアドレスを抽出するマクロ。 詳細については、次を参照してください。、 [ **SdpConvertStreamToTree** ](https://msdn.microsoft.com/library/windows/hardware/ff536794)トピック。

SDP レコードのストリームをツリー表現に変換すると、プロファイルのドライバーを呼び出すことが、 [ **SdpFindAttributeInTree** ](https://msdn.microsoft.com/library/windows/hardware/ff536838)ツリー内の指定したノードのアドレスを取得します。

プロファイルのドライバーは、すべてのクエリを実行して、このトピックで説明した関数のポインターを取得できます、 [ **BTHDDI\_SDP\_解析\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff536636)と[**BTHDDI\_SDP\_ノード\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff536635)インターフェイス。 これらのインターフェイスを照会する方法の詳細については、次を参照してください。 [Bluetooth インターフェイスの照会](querying-for-bluetooth-interfaces.md)します。

 

 





