---
title: NET_ROOT 構造
description: NET_ROOT 構造
ms.assetid: f7846343-9af6-4b7f-9c8d-190abb524946
keywords:
- net ルート構造 WDK RDBSS
- ネットワーク サーバー共有の接続データ WDK RDBSS
- NET_ROOT 構造体
- サーバー共有の接続データ WDK RDBSS
- ルート構造 WDK RDBSS
- データ構造体の WDK ファイル システム
- RDBSS WDK ファイル システム、接続およびファイル構造
- リダイレクトされたサブシステムの WDK のバッファリングをドライブのファイル システム、接続およびファイル構造
- 接続が WDK RDBSS 構造体します。
- ファイル構造 WDK RDBSS
- WDK RDBSS 構造体
- WDK RDBSS の接続情報
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 982e668d07bc6965847a001cce73b72857c4648b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575125"
---
# <a name="the-netroot-structure"></a>NET_ROOT 構造


## <span id="ddk_the_net_root_structure_if"></span><span id="DDK_THE_NET_ROOT_STRUCTURE_IF"></span>


NET_ROOT、net ルート構造体には、特定のネットワークの各サーバーの情報が含まれています。\\ネットワーク ミニリダイレクターによって維持されている接続を共有します。

NET_ROOT はどのような RDBSS とを扱うネットワーク ミニ リダイレクター ドライバーするサーバーではありません。 したがって、RDBSS 通常作成し NET_ROOT 構造が開き、呼び出しますネットワーク ミニ リダイレクター ドライバー、サーバーを開く責任を負います。 ネットワークのミニ リダイレクター ドライバーは、渡される適切なフィールドに入力が必要です。 NET_ROOT 構造にします。

NET_ROOT 構造体のリストは、各 SRV_CALL の RDBSS によって維持されます。 各 NET_ROOT 構造体には、NET_ROOT 構造体に固有の要素と共に、他の RDBSS 構造と一般的ないくつかの要素があります。 NET_ROOT 構造を管理する RDBSS ルーチンは、次の要素のみを変更します。

-   署名と参照カウント

-   テーブルの名前と関連付けられている情報

-   関連付けられている SRV_CALL 構造へのポインターを戻します

-   各種のサブ構造体のサイズ情報

-   関連付けられている FCB の構造体のルックアップ テーブル

-   どのような追加のストレージは、ネットワークのミニ リダイレクター (や NET_ROOT データ構造体の作成者) からの要求

NET_ROOT 構造体には、NET_ROOT 遷移 IRP の処理の再開する前に完了するを待機している RX_CONTEXT 構造の一覧も含まれています。 これは通常、同時実行の要求は、サーバーに転送するときに発生します。 これらの要求の 1 つは、他の要求がキューに置かれたときに開始されます。 ネットワークのミニ リダイレクターはインクルード ファイルからコンテキストのフィールドを使用してこの余分なスペースを単に参照できるように既知 NET_ROOT データ構造体の末尾に余分なスペースがネットワーク ミニリダイレクター用に予約を開始します。

NET_ROOT 構造の最終処理では、2 つの部分で構成されます。

1.  すべての V_NET_ROOTS との関連付けを破棄します。

2.  メモリの解放

これら 2 つのアクション間で遅延が発生できるし、NET_ROOT 構造内のフィールドから重複する最初の手順をできないようにします。

 

 




