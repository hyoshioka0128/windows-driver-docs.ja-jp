---
title: Direct3D バージョン 10 ハンドルの使用
description: Direct3D バージョン 10 ハンドルの使用
ms.assetid: 98cde374-0267-44bc-b285-acf4a6d17ff4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04f98cb90cacd05c75dc14c0043a08da16dc9f62
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389080"
---
# <a name="using-direct3d-version-10-handles"></a>Direct3D バージョン 10 ハンドルの使用


Misusage を防ぐために一致しないハンドルの型を検出するためにコンパイラを有効にして、Direct3D のバージョン 10 ハンドルが厳密に型指定します。 Direct3D のバージョンの 10 のハンドルを作成する型の関数の呼び出しで開始するには有効期限 (たとえば、 [ **CreateGeometryShader**](https://msdn.microsoft.com/library/windows/hardware/ff540648)) 破棄型関数の呼び出しで終了 (たとえば、 [ **DestroyShader**](https://msdn.microsoft.com/library/windows/hardware/ff552805))。 ハンドルの 3 つのカテゴリでは、Direct3D のバージョン 10 が存在します。 ハンドルの最初の 2 つのカテゴリは、ドライバーのハンドルは、Direct3D ランタイムは、ドライバーとの通信に使用して、ドライバーは、ランタイムとの通信を使用して、ランタイムのハンドル。 ハンドルの 3 つのカテゴリは、カーネル ハンドルです。 次のセクションでは、Direct3D のバージョン 10 ハンドルについて説明します。

[Direct3D のバージョン 10 ランタイムとドライバーのハンドル](direct3d-version-10-runtime-and-driver-handles.md)

[Direct3D のバージョン 10 カーネル ハンドル](direct3d-version-10-kernel-handles.md)

 

 





