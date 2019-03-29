---
title: テープ クラス ドライバーの使用
description: テープ クラス ドライバーの使用
ms.assetid: 72ed3fd9-d46f-400e-9816-f9f48b5a85c0
keywords:
- テープ ドライバー WDK ストレージ、テープ ドライバーについて
- テープ ドライバーに関するテープ ドライバー WDK、ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a992634d000b1b152ce14649d3ba75da51053dc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579712"
---
# <a name="using-the-tape-class-driver"></a>テープ クラス ドライバーの使用


## <span id="ddk_using_the_tape_class_driver_kg"></span><span id="DDK_USING_THE_TAPE_CLASS_DRIVER_KG"></span>


システム提供のテープのクラス ドライバーがデバイスに依存しないを実装して、オペレーティング システムに固有のテープのサポートしデバイスに固有のテープ miniclass ドライバーのサポート ルーチンをエクスポートします。

テープのクラス ドライバー:

-   Miniclass ドライバーのによって提供されるデバイス固有の情報を使用してテープ miniclass ドライバーを初期化します**DriverEntry**の割り当てと初期化 miniclass ドライバーをオペレーティング システムのリソースを含むルーチンとPnP マネージャーからの開始要求の受信時にデバイス オブジェクトを表すデバイスと、デバイス スタックに関連付けるとデバイスを起動 (FDO) を作成する、サポートするデバイス。

-   メモリの割り当てと初期化ルーチンをエクスポートします。

-   分割は、HBA の最大転送サイズに収まるように必要な場合に要求を転送します。

-   IRP の処理\_MJ\_作成、IRP\_MJ\_読み取り、IRP\_MJ\_書き込み、IRP\_MJ\_PNP、および IRP\_MJ\_POWER 要求.

-   デバイス非依存は IRP の前処理を実行します。\_MJ\_デバイス\_コントロール要求、テープ miniclass ドライバーに対応するデバイス固有のルーチンにディスパッチします。

-   される Srb を割り当て、テープ miniclass ドライバー、CDB と要求に適切な SRB メンバーが入力した後は、基になる記憶域ポート ドライバーに送信します。

-   Windows NT ステータス コードとテープの状態コード間の変換をデバイスに依存しないテープ固有のエラー処理、示しテープ miniclass ドライバーのデバイスに固有のエラー処理ルーチンを呼び出します。

-   テープ miniclass ドライバー (minitape 拡張機能とコマンド拡張機能) のドライバーのコンテキストの領域を割り当てます。

参照してください[テープ クラス ドライバー ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff567959)の説明については、**TapeClass * * * Xxx*テープ miniclass ドライバーによって呼び出すことができるルーチン。

 

 




