---
title: 圧縮画像のデコード
description: 圧縮画像のデコード
ms.assetid: 61633a15-72e4-49a4-9a42-684bde21df9e
keywords:
- WDK DirectX VA をデコードする圧縮画像
- 画像デコード WDK DirectX VA、圧縮
- ビデオデコード WDK DirectX VA、圧縮された画像
- ビデオをデコードする WDK DirectX VA、圧縮された画像
- WDK DirectX VA をデコードする圧縮画像、圧縮画像デコードについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20dd82a811b90a1b7a9d7a25577bf0db1fd6dea6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839047"
---
# <a name="compressed-picture-decoding"></a>圧縮画像のデコード


## <span id="ddk_compressed_picture_decoding_gg"></span><span id="DDK_COMPRESSED_PICTURE_DECODING_GG"></span>


[BDXVA\_Func 変数](bdxva-func-variable.md)が1の場合、指定された操作は圧縮された画像デコードです。 [**DXVA\_configpicture デコード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)構造体には、圧縮された画像デコード用の DirectX VA 接続構成データが含まれています。

### <a name="span-idcompressed_picture_parametersspanspan-idcompressed_picture_parametersspanspan-idcompressed_picture_parametersspancompressed-picture-parameters"></a><span id="Compressed_Picture_Parameters"></span><span id="compressed_picture_parameters"></span><span id="COMPRESSED_PICTURE_PARAMETERS"></span>圧縮された画像のパラメーター

デコードする各画像につき1回送信する必要があるパラメーターは、 [**DXVA\_ピクチャパラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)構造体で指定されます。

 

 





