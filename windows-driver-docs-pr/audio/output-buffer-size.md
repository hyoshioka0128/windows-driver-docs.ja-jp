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
ms.openlocfilehash: c36eeb51c46b622df398dc796bdb76ec00f976f0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364331"
---
# <a name="output-buffer-size"></a>出力バッファー サイズ


## <span id="output_buffer_size"></span><span id="OUTPUT_BUFFER_SIZE"></span>


ミニポート ドライバーの[ **IMiniport::DataRangeIntersection** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiport-datarangeintersection)メソッドは、呼び出し元によって割り当てられているバッファーにネゴシエートされたデータ形式を指定する構造をコピーします。 メソッドの*OutputBufferLength*パラメーターは、バッファーのサイズをバイト数を指定します。 選択した形式で形式の構造体のサイズが異なることに注意してください。 バッファーの末尾を越えて書き込みを回避するために、 **DataRangeIntersection**メソッドは、割り当てられたバッファーが小さすぎて、形式が含まれることを検証する必要がありますまずします。

Mono またはステレオの形式で出力バッファーの最小サイズは、いずれかの**sizeof**([**KSDATAFORMAT\_WAVEFORMATEX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdataformat_waveformatex)) または**sizeof**([**KSDATAFORMAT\_DSOUND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdataformat_dsound))、WAVEFORMATEX または DirectSound 形式が選択されているかどうかによって異なります。

Wave 形式は、複数の 2 つのチャネルをサポートしている場合、 [ **WAVEFORMATEX** ](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex)構造体の末尾に埋め込まれている、[**KSDATAFORMAT\_WAVEFORMATEX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdataformat_waveformatex)構造体は、追加のバイト数の相違点に相当するを占有するよう展開

**sizeof**([**WAVEFORMATEXTENSIBLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-waveformatextensible)) - **sizeof**([**WAVEFORMATEX**](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex))

 

 




