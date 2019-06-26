---
title: ストリーム クラス インターフェイスへの登録
description: ストリーム クラス インターフェイスへの登録
ms.assetid: dfc94f8d-0c0a-44ed-a4f8-791ce49aba2d
keywords:
- ビデオ キャプチャ WDK AVStream、Stream クラス インターフェイスを登録します。
- Stream クラス インターフェイスを登録するビデオの WDK AVStream のキャプチャ
- Stream クラス インターフェイス WDK AVStream を登録します。
- WDK AVStream のストリーム データを初期化しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4c800078a53599ff69e2fc5a26b11837066d912
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385693"
---
# <a name="registering-with-the-stream-class-interface"></a>ストリーム クラス インターフェイスへの登録


Stream クラス ミニドライバーでは、次の手順を使用して初期化し、データをストリーミングする準備します。

1.  ミニドライバーでサポートされているハードウェア アダプターは、プラグ アンド プレイ manager によって検出されます。

2.  プラグ アンド プレイ マネージャーが、ミニドライバーを読み込みを呼び出すようにミニドライバーの[ *DriverEntry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチン。 情報は、ファイル オブジェクトが作成された、 **DriverEntry**ルーチン。

3.  Stream クラス インターフェイスの呼び出し、ミニドライバー [ **StreamClassRegisterMinidriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclassregisteradapter)関数からその**DriverEntry**ルーチンを適切に初期化された渡します[ **HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_initialization_data)をパラメーターとして構造体。 ハードウェア ベース\_初期化\_データ構造にストリーム要求のブロック (SRB) コマンドのコードを処理するミニドライバー関数のアドレスが含まれています。 これにより、Stream クラスのインターフェイスで送信される SRB のコードに応答するミニドライバーができます。 ストリーム クラスでサポートされる SRB コマンド コードの完全な一覧については、 [Stream クラス SRB 参照](https://docs.microsoft.com/windows-hardware/drivers/stream/stream-class-srb-reference)します。

 

 




