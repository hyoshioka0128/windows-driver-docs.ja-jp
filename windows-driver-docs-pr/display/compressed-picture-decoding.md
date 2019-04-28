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
ms.openlocfilehash: dca118023d2e0cd49c5d0f23d4db0979d56a8a88
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361256"
---
# <a name="compressed-picture-decoding"></a>圧縮画像のデコード


## <span id="ddk_compressed_picture_decoding_gg"></span><span id="DDK_COMPRESSED_PICTURE_DECODING_GG"></span>


ときに、 [bDXVA\_Func 変数](bdxva-func-variable.md)1 には、データが圧縮された画像をデコード操作で指定します。 [ **DXVA\_ConfigPictureDecode** ](https://msdn.microsoft.com/library/windows/hardware/ff563133)構造体には、圧縮された画像をデコードの DirectX VA 接続の構成データが含まれています。

### <a name="span-idcompressedpictureparametersspanspan-idcompressedpictureparametersspanspan-idcompressedpictureparametersspancompressed-picture-parameters"></a><span id="Compressed_Picture_Parameters"></span><span id="compressed_picture_parameters"></span><span id="COMPRESSED_PICTURE_PARAMETERS"></span>圧縮された画像のパラメーター

デコードするには、各画像を 1 回送信する必要がありますパラメーターがで指定された、 [ **DXVA\_PictureParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff564012)構造体。

 

 





