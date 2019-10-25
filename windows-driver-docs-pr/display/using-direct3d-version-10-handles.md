---
title: Direct3D バージョン 10 ハンドルの使用
description: Direct3D バージョン 10 ハンドルの使用
ms.assetid: 98cde374-0267-44bc-b285-acf4a6d17ff4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0a82524cbe227250ae80a363153a9099c2781c5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829262"
---
# <a name="using-direct3d-version-10-handles"></a>Direct3D バージョン 10 ハンドルの使用


Direct3D バージョン10のハンドルは、不適切な使用を防ぐために厳密に型指定されています。また、コンパイラが一致しないハンドルの種類を検出できるようにします。 Direct3D バージョン10のハンドルには、作成型関数 ( [**CreateGeometryShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_creategeometryshader)など) への呼び出しで始まり、破棄型関数 ( [**destroyshader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyshader)など) への呼び出しで終了する有効期間があります。 Direct3D バージョン10のハンドルのカテゴリは3つあります。 ハンドルの最初の2つのカテゴリはドライバーハンドルで、Direct3D ランタイムはドライバーとの通信に使用します。ランタイムハンドルは、ドライバーがランタイムとの通信に使用します。 ハンドルの3番目のカテゴリはカーネルハンドルです。 以下のセクションでは、Direct3D バージョン10のハンドルについて説明します。

[Direct3D バージョン10ランタイムとドライバーハンドル](direct3d-version-10-runtime-and-driver-handles.md)

[Direct3D バージョン10カーネルハンドル](direct3d-version-10-kernel-handles.md)

 

 





