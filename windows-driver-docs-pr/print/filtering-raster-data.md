---
title: ラスター データのフィルター処理
description: ラスター データのフィルター処理
ms.assetid: 179a2dc0-8794-4934-99b9-eb3f7900536c
keywords:
- Unidrv、ラスターデータフィルタリング
- GPD ファイル WDK Unidrv、ラスターデータフィルタリング
- ラスターデータのフィルター処理 WDK 印刷
- ラスターデータフィルター WDK Unidrv
- 後処理スキャンラインデータストリーム WDK Unidrv
- Unidrv WDK 印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c243056b874d0fdb6fc2af9b1885b77dcbf11b6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833833"
---
# <a name="filtering-raster-data"></a>ラスター データのフィルター処理





スプールする前にスキャンラインデータストリームのカスタマイズされた後処理を提供する場合は、[レンダリングプラグイン](rendering-plug-ins.md)で[**Iprintoemuni:: filtergraphics**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-filtergraphics)メソッドを実装します。 この Unidrv 機能に関連付けられている GPD ファイルエントリがありません。

詳細については、「カスタマイズされた[データストリームのフィルター処理](customized-data-stream-filtering.md)」を参照してください。

 

 




