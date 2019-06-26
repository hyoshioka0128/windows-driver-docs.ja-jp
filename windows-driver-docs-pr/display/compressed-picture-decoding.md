---
title: 圧縮画像のデコード
description: 圧縮画像のデコード
ms.assetid: 61633a15-72e4-49a4-9a42-684bde21df9e
keywords:
- WDK DirectX VA をデコードする圧縮の画像
- デコード WDK DirectX va なので、圧縮の画像します。
- ビデオのデコード WDK DirectX va なので、画像の圧縮
- 画像を圧縮されたビデオの WDK DirectX VA をデコードするには、
- WDK DirectX va なのでをデコードについて圧縮の画像は、画像をデコードすることを圧縮します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3eef9b36d575a36b76e6d74c60f83cd92f56a363
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370665"
---
# <a name="compressed-picture-decoding"></a>圧縮画像のデコード


## <span id="ddk_compressed_picture_decoding_gg"></span><span id="DDK_COMPRESSED_PICTURE_DECODING_GG"></span>


ときに、 [bDXVA\_Func 変数](bdxva-func-variable.md)1 には、データが圧縮された画像をデコード操作で指定します。 [ **DXVA\_ConfigPictureDecode** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_configpicturedecode)構造体には、圧縮された画像をデコードの DirectX VA 接続の構成データが含まれています。

### <a name="span-idcompressedpictureparametersspanspan-idcompressedpictureparametersspanspan-idcompressedpictureparametersspancompressed-picture-parameters"></a><span id="Compressed_Picture_Parameters"></span><span id="compressed_picture_parameters"></span><span id="COMPRESSED_PICTURE_PARAMETERS"></span>圧縮された画像のパラメーター

デコードするには、各画像を 1 回送信する必要がありますパラメーターがで指定された、 [ **DXVA\_PictureParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_pictureparameters)構造体。

 

 





