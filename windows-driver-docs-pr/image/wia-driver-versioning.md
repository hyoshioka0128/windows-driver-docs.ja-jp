---
title: WIA ドライバーのバージョン管理
description: WIA ドライバーのバージョン管理
ms.assetid: 9ebd79ac-d742-4524-9573-5873f7a8ec37
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d8fec11adbf7377eb5c717f9ae2a3b5a6c160aa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840701"
---
# <a name="wia-driver-versioning"></a>WIA ドライバーのバージョン管理


ドライバーは、 [**iで**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getcapabilities)返されるバージョンフィールドでサポートされている WIA (レガシドライバーの場合は STI) のバージョンを報告します。 ドライバーは、通常、このフィールドを STI\_バージョンに設定します。これは、 *sti*で定義されています。

Windows Vista 用 Windows Driver Kit (WDK) では、以前のオペレーティングシステムで、STI\_バージョンの値が、STI\_バージョンの値を超えています。 ドライバーのバージョンが Windows Vista の場合は、Windows Vista [IStream データ転送](istream-data-transfers.md)がサポートされている必要があります。

新しい Windows Vista WIA モデルに準拠している Windows Vista ドライバーは、 **Istiusd:: GetCapabilities**から返されたバージョンフィールドで、\_バージョン\_3 の STI を返す必要があります。

 

 




