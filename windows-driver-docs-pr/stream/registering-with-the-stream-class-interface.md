---
title: ストリーム クラス インターフェイスへの登録
description: ストリーム クラス インターフェイスへの登録
ms.assetid: dfc94f8d-0c0a-44ed-a4f8-791ce49aba2d
keywords:
- video capture WDK AVStream、Stream クラスインターフェイスの登録
- キャプチャビデオ WDK AVStream、ストリームクラスインターフェイスの登録
- ストリームクラスインターフェイスの WDK AVStream を登録しています
- stream data WDK AVStream を初期化しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bb39891ddc1811f8e3da31303b25092cf0cb2aa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843401"
---
# <a name="registering-with-the-stream-class-interface"></a>ストリーム クラス インターフェイスへの登録


Stream クラスミニドライバー次の手順に従って、データを初期化してストリーム配信する準備をします。

1.  ミニドライバーによってサポートされるハードウェアアダプターは、プラグアンドプレイマネージャーによって検出されます。

2.  プラグアンドプレイマネージャーは、ミニドライバーを読み込み、ミニドライバーの[*Driverentry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンを呼び出します。 **Driverentry**ルーチンの情報からファイルオブジェクトが作成されます。

3.  ミニドライバーは、 **Driverentry**ルーチンからストリームクラスインターフェイスの[**StreamClassRegisterMinidriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassregisteradapter)関数を呼び出し、適切に初期化された[**HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_initialization_data)構造体をパラメーターとして渡します。 HW\_初期化\_データ構造には、ストリーム要求ブロック (SRB) コマンドコードを処理するミニドライバー関数のアドレスが含まれます。 これにより、ミニドライバーは、ストリームクラスインターフェイスによって送信された SRB コードに応答できるようになります。 Stream クラスでサポートされている SRB コマンドコードの完全な一覧については、「 [Stream クラス SRB Reference](https://docs.microsoft.com/windows-hardware/drivers/stream/stream-class-srb-reference)」を参照してください。

 

 




