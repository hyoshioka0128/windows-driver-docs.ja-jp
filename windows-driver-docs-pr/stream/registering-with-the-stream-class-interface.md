---
title: Stream クラスのインターフェイスに登録します。
description: Stream クラスのインターフェイスに登録します。
ms.assetid: dfc94f8d-0c0a-44ed-a4f8-791ce49aba2d
keywords:
- ビデオ キャプチャ WDK AVStream、Stream クラス インターフェイスを登録します。
- Stream クラス インターフェイスを登録するビデオの WDK AVStream のキャプチャ
- Stream クラス インターフェイス WDK AVStream を登録します。
- WDK AVStream のストリーム データを初期化しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df66766eebcaa06a8d0636c1fd4d9c4c3f9c1c15
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530678"
---
# <a name="registering-with-the-stream-class-interface"></a>Stream クラスのインターフェイスに登録します。


Stream クラス ミニドライバーでは、次の手順を使用して初期化し、データをストリーミングする準備します。

1.  ミニドライバーでサポートされているハードウェア アダプターは、プラグ アンド プレイ manager によって検出されます。

2.  プラグ アンド プレイ マネージャーが、ミニドライバーを読み込みを呼び出すようにミニドライバーの[ *DriverEntry* ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチン。 情報は、ファイル オブジェクトが作成された、 **DriverEntry**ルーチン。

3.  Stream クラス インターフェイスの呼び出し、ミニドライバー [ **StreamClassRegisterMinidriver** ](https://msdn.microsoft.com/library/windows/hardware/ff568263)関数からその**DriverEntry**ルーチンを適切に初期化された渡します[ **HW\_初期化\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff559682)をパラメーターとして構造体。 ハードウェア ベース\_初期化\_データ構造にストリーム要求のブロック (SRB) コマンドのコードを処理するミニドライバー関数のアドレスが含まれています。 これにより、Stream クラスのインターフェイスで送信される SRB のコードに応答するミニドライバーができます。 ストリーム クラスでサポートされる SRB コマンド コードの完全な一覧については、 [Stream クラス SRB 参照](https://msdn.microsoft.com/library/windows/hardware/ff568295)します。

 

 




