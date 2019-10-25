---
title: マクロブロック制御コマンド バッファー
description: マクロブロック制御コマンド バッファー
ms.assetid: ed6905f6-7e7c-47d2-8f6e-95cfa03e21cb
keywords:
- マクロが WDK DirectX VA、コマンドバッファーをブロックする
- コマンドバッファーの WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1ba990931c31097bfe935dafdbdb9c2dea8645f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840590"
---
# <a name="macroblock-control-command-buffers"></a>マクロブロック制御コマンド バッファー


## <span id="ddk_macroblock_control_command_buffers_gg"></span><span id="DDK_MACROBLOCK_CONTROL_COMMAND_BUFFERS_GG"></span>


デコードされた画像には、1つ以上のマクロブロックコントロールコマンドバッファーが含まれています (ビットストリームバッファーが含まれていない場合)。 すべてのマクロブロックのデコードプロセスは、マクロブロックコントロールのコマンドバッファーに指定されています (1 回だけ)。

すべてのマクロブロックコントロールのコマンドバッファーには、同じマクロブロックのセットのデータを格納する残存差ブロックデータバッファーがあります。 1つ以上の[deblocking フィルターコントロール](deblocking-filter-commands.md)バッファーが送信された場合、各 deblocking フィルターコントロールバッファーのマクロブロックのセットは、対応するマクロブロックコントロールと残留差ブロックデータバッファー内のマクロブロックのセットと同じになります。

画像を処理するには、各マクロブロックのモーション予測を残存差データの追加の前に行う必要があります。 画像のデコードは、次の2つの方法のいずれかで行うことができます。

-   残存差データバッファーを処理しながら、まず、マクロブロックコントロールのコマンドバッファーでモーション予測コマンドを処理してから、圧縮されていないターゲット画面からモーション補正予測データを読み取ります。

-   マクロブロックコントロールのコマンドバッファーと残留差のデータバッファーを調整された方法で処理します。 残差データバッファーに指定された残存データを予測に追加してから、圧縮されていないターゲットサーフェイスに結果を書き込みます。

マクロブロックコントロールコマンドと各マクロブロックの残存差データは、そのマクロブロック内の四角形の領域にのみ影響します。

マクロブロックコントロールコマンドバッファー内のマクロブロックコントロールコマンドの合計数は、対応する[**DXVA\_BufferDescription**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_bufferdescription)構造体の**Dwnummbsinbuffer**メンバーによって指定されます。

残存差データバッファー内のデータの数量と種類は、対応するマクロブロックコントロールコマンドの**Wpattern コード**、 **Wpc\_Overflow**、 **bnumcoef**の各メンバーによって決定されます。

次の図は、マクロブロックコントロールのコマンドバッファーと残差のデータバッファーとの関係を示しています。

![マクロブロックコントロールのコマンドバッファーと残差のデータバッファーとの関係を示す図](images/residdiffdata.png)

[**DXVA\_Configピクチャデコード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)構造体の**bConfigMBcontrolRasterOrder**メンバーが1と等しい場合、次の式は前の図に適用されます。ここで、 *i*は、のマクロブロックのインデックスです。マクロブロックコントロールコマンドバッファー。

![mb 制御コマンドバッファーと残差データバッファーの関係を示す図](images/formula3.png)

 

 





