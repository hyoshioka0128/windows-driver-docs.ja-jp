---
title: ユーザー モードの静止画像ミニドライバーを作成します。
description: ユーザー モードの静止画像ミニドライバーを作成します。
ms.assetid: 94fdbeba-5b4a-4b66-b381-ec362b6d38c9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 068de4dc8ed2378faa264b569d8f39e5714a5455
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535901"
---
# <a name="creating-a-user-mode-still-image-minidriver"></a>ユーザー モードの静止画像ミニドライバーを作成します。





すべてのユーザー モード静止画像ミニドライバーがによって定義されたインターフェイスのメソッドを実装する必要があります[IStiUSD COM インターフェイス](istiusd-com-interface.md)します。 この実装は、次の手順を使用して、比較的簡単です。

**IStiUSD COM インターフェイスで定義されたメソッドを実装するには。**

1.  、インターフェイスの GUID を取得し、ヘッダー ファイルとセットアップ情報 (INF) ファイルに含めます。

2.  実装ファイル (.cpp) などを作成します。

3.  作成、カスタマイズしたクラス定義を使用して**IStiUSD**継承クラスとして。

4.  すべての定義されているメソッドの実装、 [IStiUSD COM インターフェイス](istiusd-com-interface.md)します。 STIERR を返す必要があります、メソッドが必要でない場合\_サポートされていません。

このセクションでは、次のトピックについての情報を提供します。

[デバイスのイベントを静止画像します。](still-image-device-events.md)

[転送モード](transfer-modes.md)

[セキュリティの問題は、ドライバーを静止画像します。](security-issues-for-still-image-drivers.md)

 

 




