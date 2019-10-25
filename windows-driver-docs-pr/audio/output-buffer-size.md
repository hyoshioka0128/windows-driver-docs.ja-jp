---
title: 出力バッファー サイズ
description: 出力バッファー サイズ
ms.assetid: 386cc6f7-2fab-474a-b997-9ba2457ada0c
keywords:
- データ交差ハンドラー WDK オーディオ、出力バッファーサイズ
- 出力バッファー WDK オーディオ
- バッファーサイズ WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50a62ecf80dc891555c0261378ec321809783346
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832547"
---
# <a name="output-buffer-size"></a>出力バッファー サイズ


## <span id="output_buffer_size"></span><span id="OUTPUT_BUFFER_SIZE"></span>


ミニポートドライバーの[**IMiniport::D ataRangeIntersection 部分**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiport-datarangeintersection)メソッドは、ネゴシエートされたデータ形式を指定する構造体を、呼び出し元によって割り当てられたバッファーにコピーします。 メソッドの*Outputbufferlength*パラメーターは、バッファーのサイズをバイト単位で指定します。 フォーマット構造のサイズは、選択した形式によって異なります。 バッファーの末尾を越えた書き込みを回避するために、 **Datarangeintersection**メソッドは、割り当てられたバッファーが、形式を格納するのに十分な大きさであることを最初に確認する必要があります。

Mono またはステレオ形式の場合、出力バッファーの最小サイズは、WAVEFORMATEX と DirectSound のどちらであるかに応じて、 **sizeof**([**KSDATAFORMAT\_WAVEFORMATEX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_waveformatex)) または**sizeof**([**KSDATAFORMAT\_DSOUND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_dsound)) のいずれかになります。形式が選択されました。

Wave 形式が2つ以上のチャネルをサポートしている場合は、[**KSDATAFORMAT\_WAVEFORMATEX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_waveformatex)構造体の末尾に埋め込まれている[**WAVEFORMATEX**](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex)構造体を拡張して、その差と同じ数のバイトを占有します。

**sizeof**([**WAVEFORMATEXTENSIBLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible))- **sizeof**([**WAVEFORMATEX**](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex))

 

 




