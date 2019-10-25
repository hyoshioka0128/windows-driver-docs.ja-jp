---
title: テープ クラス ドライバーの使用
description: テープ クラス ドライバーの使用
ms.assetid: 72ed3fd9-d46f-400e-9816-f9f48b5a85c0
keywords:
- テープドライバー WDK 記憶域、テープドライバーについて
- 記憶域テープドライバー WDK、テープドライバーについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4f26a5b0a0141be66737fb97ef759fcec38340b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845371"
---
# <a name="using-the-tape-class-driver"></a>テープ クラス ドライバーの使用


## <span id="ddk_using_the_tape_class_driver_kg"></span><span id="DDK_USING_THE_TAPE_CLASS_DRIVER_KG"></span>


システム提供のテープクラスドライバーは、デバイスに依存しないオペレーティングシステム固有のテープサポートを実装し、デバイス固有の tape miniclass ドライバーのサポートルーチンをエクスポートします。

テープクラスドライバー:

-   Miniclass ドライバーの**Driverentry**ルーチンによって提供されるデバイス固有の情報を使用して、tape miniclass driver を初期化します。これには、miniclass ドライバーとそれがサポートするデバイスのオペレーティングシステムリソースの割り当てと初期化が含まれます。デバイスを表すデバイスオブジェクト (FDO) を作成し、デバイススタックにアタッチし、PnP マネージャーから開始要求の受信時にデバイスを起動します。

-   メモリの割り当ておよび初期化ルーチンをエクスポートします。

-   必要に応じて転送要求を分割し、HBA の最大転送サイズ内に収まるようにします。

-   IRP\_MJ\_CREATE、IRP\_MJ\_READ、IRP\_MJ\_WRITE、IRP\_MJ\_PNP、および IRP\_MJ\_の電源要求を処理します。

-   IRP\_MJ\_\_デバイスのデバイスに依存しないプリプロセスを実行して、要求を制御し、tape miniclass ドライバー内の対応するデバイス固有のルーチンにディスパッチします。

-   SRBs を割り当て、テープ miniclass ドライバーが要求に適した CDB およびその他の SRB メンバーを入力した後に、基になるストレージポートドライバーに送信します。

-   Windows NT 状態コードとテープの状態コードを変換し、デバイスに依存しないテープ固有のエラー処理を提供し、tape miniclass ドライバーのデバイス固有のエラー処理ルーチンを呼び出します。

-   Tape miniclass ドライバー (minitape 拡張機能とコマンド拡張機能) のドライバーコンテキスト領域を割り当てます。

Tape miniclass ドライバーから呼び出すことができる **TapeClass * * * Xxx*ルーチンの説明については、「 [Tape Class Driver ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

 

 




