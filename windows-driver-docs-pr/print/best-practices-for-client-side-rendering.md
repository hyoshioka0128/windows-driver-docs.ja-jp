---
title: クライアント側のレンダリングのためのベスト プラクティス
description: クライアント側のレンダリングのためのベスト プラクティス
ms.assetid: d05086c1-4e0b-4767-bb1d-7b6d73b1b210
keywords:
- クライアント側のレンダリング WDK の印刷、ベスト プラクティス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cca25f0b73b0e12cb770bcb23be33d2f0315af99
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536410"
---
# <a name="best-practices-for-client-side-rendering"></a>クライアント側のレンダリングのためのベスト プラクティス


クライアント側のレンダリングを正常に動作するために、プリンター ドライバーを記述するときに注意してください、次のものをおく必要があります。

-   プリンター ドライバーは、ドライバー パッケージとしてインストールする必要があります。

-   プリンター ドライバーでは、プリンターの構成情報を格納するのに SetPrinterData または SetPrinterDataEx 関数を使用する必要があります。 これらの関数の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

-   カスタムのプリント プロセッサを使用するプリンター ドライバーがドライバー パッケージに、プロセッサを含める必要があります、そのポイントを確認して、印刷は、クライアント コンピューター上に読み込みます。

 

 




