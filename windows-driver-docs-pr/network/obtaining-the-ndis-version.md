---
title: NDIS バージョンの取得
description: NDIS バージョンの取得
ms.assetid: f7bbd11c-b6ec-4adb-8c42-ec438d518ed8
keywords:
- オペレーティングシステムのバージョンと比較して、NDIS バージョン情報 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec744da14872d49b7d6ac80592ff3cd02fd02209
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842168"
---
# <a name="obtaining-the-ndis-version"></a>NDIS バージョンの取得





NDIS バージョンは、オペレーティングシステムのバージョンと同じであるとは限りません。 たとえば、 [**Rtlgetversion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlgetversion)および[**RtlVerifyVersionInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlverifyversioninfo)ルーチンを使用してオペレーティングシステムのバージョンを取得した場合、特定の NDIS バージョンとの関連付けは保証されません。 そのため、NDIS ドライバーは、NDIS バージョンとオペレーティングシステムのバージョンを個別に取得する必要があります。 NDIS ドライバーは、 [**NdisGetVersion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetversion)関数を使用して ndis バージョンを取得できます。

## <a name="related-topics"></a>関連トピック


[NDIS バージョンの概要](overview-of-ndis-versions.md)

[NDIS バージョン情報の指定](specifying-ndis-version-information.md)

 

 






