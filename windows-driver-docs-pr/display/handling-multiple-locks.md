---
title: 複数のロックの処理
description: 複数のロックの処理
ms.assetid: d62b9577-d78f-431d-a5bf-c06c9be345c0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d9a3c2be3abe614cb8b6f8187646bdc84157181
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839660"
---
# <a name="handling-multiple-locks"></a>複数のロックの処理


Direct3D ランタイムを使用すると、頂点バッファーとインデックスバッファーに複数のロックが保留されることを許可できます。 ユーザーモードの表示ドライバーは、 [Windows 2000 Display Driver モデル](windows-2000-display-driver-model-design-guide.md)のランタイムと同じ方法で、複数のロックを処理する必要があります。

ユーザーモードの表示ドライバーは、既にロックされているリソースに対する[**Lockasync**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lockasync)関数の呼び出しに失敗することはできません。 つまり、 *lockasync*関数の最初の呼び出しでそのリソースのロックが成功した後、特定のリソースに対する*lockasync*関数の呼び出しをドライバーが失敗させることはできません。 同様に、ドライバーは、*ロック*関数の最初の呼び出しでそのリソースのロックが成功した後に、特定のリソースに対する[**ロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lock)関数の呼び出しを失敗させることはできません。 ランタイムは、ドライバーの[**UnlockAsync**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_unlockasync)関数を呼び出すことによって、ドライバーの*lockasync*関数に対して行われる各呼び出しに一致します。 また、ランタイムは、ドライバーの[**Unlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_unlock)関数を呼び出すことによって、ドライバーの*ロック*関数に対して行われる各呼び出しに一致します。

[**D3DDDIARG\_UnlockAsync**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_unlockasync)構造体に記述されているリソースが、ドライバーの*lockasync*への前回の呼び出しによって実際にロックされていない場合を除き、ユーザーモードの表示ドライバーは、 [**UnlockAsync**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_unlockasync)関数への呼び出しに失敗することはできません。プロシージャ. 同様に、ドライバーは、 [**D3DDDIARG\_unlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_unlock)構造体に記述されているリソースが、ドライバーの*ロック*関数の前回の呼び出しによって実際にロックされていない限り、 [**unlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_unlock)関数の呼び出しに失敗することはありません。 リソースが以前にロックされていない状況では、 *UnlockAsync*と*Unlock*は E\_invalidarg を返します。

 

 





