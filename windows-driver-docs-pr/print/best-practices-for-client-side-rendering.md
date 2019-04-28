---
title: クライアント側レンダリングのベスト プラクティス
description: クライアント側レンダリングのベスト プラクティス
ms.assetid: d05086c1-4e0b-4767-bb1d-7b6d73b1b210
keywords:
- クライアント側のレンダリング WDK の印刷、ベスト プラクティス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cca25f0b73b0e12cb770bcb23be33d2f0315af99
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362005"
---
# <a name="best-practices-for-client-side-rendering"></a>クライアント側レンダリングのベスト プラクティス


クライアント側のレンダリングを正常に動作するために、プリンター ドライバーを記述するときに注意してください、次のものをおく必要があります。

-   プリンター ドライバーは、ドライバー パッケージとしてインストールする必要があります。

-   プリンター ドライバーでは、プリンターの構成情報を格納するのに SetPrinterData または SetPrinterDataEx 関数を使用する必要があります。 これらの関数の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

-   カスタムのプリント プロセッサを使用するプリンター ドライバーがドライバー パッケージに、プロセッサを含める必要があります、そのポイントを確認して、印刷は、クライアント コンピューター上に読み込みます。

 

 




