---
title: マクロブロック制御コマンド バッファー
description: マクロブロック制御コマンド バッファー
ms.assetid: ed6905f6-7e7c-47d2-8f6e-95cfa03e21cb
keywords:
- マクロ ブロック WDK DirectX va なので、コマンド バッファー
- コマンド バッファー WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8674be88550a4d13cc8559e44f9f2137634410a8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375394"
---
# <a name="macroblock-control-command-buffers"></a>マクロブロック制御コマンド バッファー


## <span id="ddk_macroblock_control_command_buffers_gg"></span><span id="DDK_MACROBLOCK_CONTROL_COMMAND_BUFFERS_GG"></span>


デコードされた画像には、(ビット ストリーム バッファーは含まれません) 場合の 1 つまたは複数のマクロ ブロック コントロール コマンド バッファーが含まれています。 すべてのマクロ ブロックのデコード処理は、マクロ ブロック コントロール コマンド バッファーで (1 回だけ) 指定されます。

各マクロ ブロック コントロール コマンド バッファーには、マクロ ブロックの同じセットのデータを含む対応する残存違いブロック データ バッファーです。 1 つまたは複数[フィルター コントロールのバッファーを非ブロック化](deblocking-filter-commands.md)送信されると、各 deblocking フィルター コントロール バッファー内のマクロ ブロックのセットは、対応するマクロ ブロック コントロールおよび残余違いブロックでのマクロ ブロックのセットと同じです。データ バッファー。

画像の処理では、各マクロ ブロックのモーション予測残存違いデータの追加の前にする必要があります。 画像をデコードすることは、次の 2 つの方法のいずれかで実行できます。

-   モーションの予測コマンド マクロ ブロック コントロールのコマンドは、最初のバッファーします。 その後、動き補償予測データを戻して、圧縮されていない宛先表面から残存の違いのデータ バッファーの処理中にするプロセス。

-   マクロ ブロック コントロール コマンド バッファーと連携的に残留違いデータ バッファーを処理します。 圧縮されていない宛先表面に、結果を書き込む前に、予測に残存違いデータ バッファーで指定された残留データを追加します。

マクロ ブロック コントロール コマンドおよびデータは、各マクロ ブロックの残存の相違は、そのマクロ ブロック内で四角形の領域のみに影響します。

マクロ ブロック コントロール コマンド バッファーで管理コマンドをマクロ ブロックの合計数がで指定された、 **dwNumMBsInBuffer**の対応するメンバー [ **DXVA\_BufferDescription** ](https://msdn.microsoft.com/library/windows/hardware/ff563122)構造体。

量と残存違いデータ バッファー内のデータの種類によって決まりますが、 **wPatternCode**、 **wPC\_Overflow**、および**bNumCoef**のメンバー対応するマクロ ブロック コントロール コマンド。

次の図は、マクロ ブロック コントロールのコマンド バッファーと残存違いデータ バッファー間の関係を示します。

![マクロ ブロック コントロール コマンド バッファーと残存の違いのデータ バッファーの間の関係を示す図](images/residdiffdata.png)

場合、 **bConfigMBcontrolRasterOrder**のメンバー、 [ **DXVA\_ConfigPictureDecode** ](https://msdn.microsoft.com/library/windows/hardware/ff563133)構造体が 1 に、その後に次の式が適用されます前の図で*は*マクロ ブロック コントロール コマンド バッファー内のマクロ ブロックのインデックスです。

![mb コントロール コマンド バッファーと残存違いデータ バッファーの間の関係を示す図](images/formula3.png)

 

 





