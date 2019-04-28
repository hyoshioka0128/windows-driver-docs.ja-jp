---
title: パラレル ポートに関する情報の取得
description: パラレル ポートに関する情報の取得
ms.assetid: d8ae2296-05b6-419a-93cc-00fcb12d41fe
keywords:
- パラレル ポート WDK、情報を取得します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7754095795119f3061223b0fb0f1bf2c1c03831c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373538"
---
# <a name="obtaining-information-about-a-parallel-port"></a>パラレル ポートに関する情報の取得





クライアントは、パラレル ポートを使用する前に、次の情報を取得できます。

-   パラレル ポートによって使用されるリソース

-   パラレル ポートのハードウェア機能

-   [パラレル ポート コールバック ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff544307)カーネル モード ドライバーを使用します。

クライアントは、上記の情報を取得するのに次の内部デバイス制御要求を使用します。

[**IOCTL\_内部\_取得\_並列\_ポート\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff544002)

[**IOCTL\_内部\_取得\_詳細\_並列\_ポート\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff543996)

[**IOCTL\_内部\_取得\_並列\_PNP\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff543997)

クライアントでは、パラレル ポート情報をリリースを使用して、 [ **IOCTL\_内部\_リリース\_並列\_ポート\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff544047)要求。

 

 




