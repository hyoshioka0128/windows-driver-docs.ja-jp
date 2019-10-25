---
title: Macrovision
description: Macrovision
ms.assetid: 62bd8d8a-3e58-4bca-a32d-ff792180afbe
keywords:
- DVD デコーダーミニドライバー WDK、著作権保護
- デコーダーミニドライバー WDK DVD、著作権保護
- 著作権保護 WDK DVD デコーダー
- Macrovision WDK DVD デコーダー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d997179f2af42c7896037d775cbf73cc3dc3461
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842138"
---
# <a name="macrovision"></a>Macrovision





Macrovision は、コンピューターから離れる前にビデオデータを処理する最後のデバイスでサポートされています。 ビデオカードへのビデオポート接続の場合、ビデオカードと DVD ナビゲーター/スプリッターは、すべての Macrovision 処理を処理します。 デコーダーは関係していません。

デコーダーに NTSC 出力がある場合、Macrovision encoding と Macrovision 準拠はデコーダーカードの役割です。 [**KS\_COPY\_MACROVISION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_copy_macrovision)プロパティは、メディアの MACROVISION encoding のレベル (レベル 0 ~ 3) を示します。 デコーダーは、この情報を使用して、NTSC 出力の Macrovision エンコードを有効または無効にすることができます。

 

 




