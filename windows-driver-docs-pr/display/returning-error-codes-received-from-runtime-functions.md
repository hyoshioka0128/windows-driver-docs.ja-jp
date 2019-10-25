---
title: ランタイム関数から受信したエラー コードを返す
description: ランタイム関数から受信したエラー コードを返す
ms.assetid: 4a2384e8-407f-4248-8b31-7c4e836b15dc
keywords:
- ユーザーモード表示ドライバー WDK Windows Vista、ランタイム関数のエラーコード
- ランタイム関数エラーコード WDK 表示
- エラーコード WDK 表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 951b29698a54d65b6ebd4e1d67b76d88b80d9b34
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825822"
---
# <a name="returning-error-codes-received-from-runtime-functions"></a>ランタイム関数から受信したエラー コードを返す


[Direct3d version 9 ユーザーモード表示ドライバーが提供する関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/index)を呼び出すと、[関数にアクセスする direct3d ランタイムが提供するカーネルサービス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を呼び出すと、その関数が受け取ったエラーコードを返す必要があります。 たとえば、ランタイムは、 [**Createresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)関数などのユーザーモードの表示ドライバー関数を呼び出す場合があります。 次に、これは、特定の操作 (この場合はリソースにメモリを割り当てるため) を実行するために、 [**Pfnallocatecb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)関数などのランタイム提供の関数を呼び出します。 ユーザーモードの表示ドライバーが、ランタイムによって指定された関数の呼び出しからエラーコードを受け取った場合、そのエラーコードをランタイムに返す必要があります。

**ただし**、このルールには、ドライバーがランタイムエラーコードをランタイムに渡す必要があるという例外が1つ   あります。 ドライバーが[**Pfnallocatecb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)ランタイムによって提供される関数を呼び出したときに、ビデオメモリが既に割り当てられている場合、オプションリソースにビデオメモリを割り当てるには、規則は適用されません。 **Pfnallocatecb**が、パフォーマンスの最適化に必要なオプションリソースに対してこのビデオメモリの割り当てに失敗した場合、ドライバーはメモリ不足エラー (E\_OUTOFMEMORY) をランタイムに報告しないようにする必要があります。

 

 

 





