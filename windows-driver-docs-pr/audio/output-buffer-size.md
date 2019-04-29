---
title: 出力バッファー サイズ
description: 出力バッファー サイズ
ms.assetid: 386cc6f7-2fab-474a-b997-9ba2457ada0c
keywords:
- 交差部分のデータ ハンドラーの WDK オーディオ、出力バッファーのサイズ
- 出力バッファーの WDK オーディオ
- バッファー サイズの WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3b2240172bbb759c621d5aa47570007c7f544e4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332251"
---
# <a name="output-buffer-size"></a>出力バッファー サイズ


## <span id="output_buffer_size"></span><span id="OUTPUT_BUFFER_SIZE"></span>


ミニポート ドライバーの[ **IMiniport::DataRangeIntersection** ](https://msdn.microsoft.com/library/windows/hardware/ff536764)メソッドは、呼び出し元によって割り当てられているバッファーにネゴシエートされたデータ形式を指定する構造をコピーします。 メソッドの*OutputBufferLength*パラメーターは、バッファーのサイズをバイト数を指定します。 選択した形式で形式の構造体のサイズが異なることに注意してください。 バッファーの末尾を越えて書き込みを回避するために、 **DataRangeIntersection**メソッドは、割り当てられたバッファーが小さすぎて、形式が含まれることを検証する必要がありますまずします。

Mono またはステレオの形式で出力バッファーの最小サイズは、いずれかの**sizeof**([**KSDATAFORMAT\_WAVEFORMATEX**](https://msdn.microsoft.com/library/windows/hardware/ff537095)) または**sizeof**([**KSDATAFORMAT\_DSOUND**](https://msdn.microsoft.com/library/windows/hardware/ff537094))、WAVEFORMATEX または DirectSound 形式が選択されているかどうかによって異なります。

Wave 形式は、複数の 2 つのチャネルをサポートしている場合、 [ **WAVEFORMATEX** ](https://msdn.microsoft.com/library/windows/hardware/ff538799)構造体の末尾に埋め込まれている、[**KSDATAFORMAT\_WAVEFORMATEX** ](https://msdn.microsoft.com/library/windows/hardware/ff537095)構造体は、追加のバイト数の相違点に相当するを占有するよう展開

**sizeof**([**WAVEFORMATEXTENSIBLE**](https://msdn.microsoft.com/library/windows/hardware/ff538802)) - **sizeof**([**WAVEFORMATEX**](https://msdn.microsoft.com/library/windows/hardware/ff538799))

 

 




