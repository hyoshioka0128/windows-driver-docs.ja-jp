---
title: 複数ロックの処理
description: 複数ロックの処理
ms.assetid: d62b9577-d78f-431d-a5bf-c06c9be345c0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a497b7b1047d99ed757a8cee62b43d852563be02
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359338"
---
# <a name="handling-multiple-locks"></a>複数ロックの処理


Direct3D、ランタイムでは、頂点バッファーとインデックス バッファーが未処理の 1 つ以上のロックを許可できます。 ユーザー モードのディスプレイ ドライバーがでランタイムと同じ方法には複数のロックの処理する必要があります、 [Windows 2000 Display Driver Model](windows-2000-display-driver-model-design-guide.md)します。

ユーザー モードのディスプレイ ドライバーはへの呼び出しに失敗することはできません、 [ **LockAsync** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_lockasync)既にロックされているリソース用の関数。 ドライバーでへの呼び出しが失敗することはできません、その*LockAsync*関数の最初の呼び出し後に、特定のリソースの*LockAsync*関数は、そのリソースのロックが成功しました。 ドライバーでの呼び出しが失敗することはできません同様に、その[**ロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_lock)関数の最初の呼び出し後に、特定のリソースの*ロック*関数が正常にロックします。リソースです。 ランタイムが各呼び出しは、ドライバーを送信すると一致する*LockAsync*ドライバーへの呼び出しで関数を[ **UnlockAsync** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_unlockasync)関数。 ランタイムでは、アプリケーションは、ドライバーを各の呼び出しとも一致*ロック*ドライバーへの呼び出しで関数を[ **Unlock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_unlock)関数。

ユーザー モードのディスプレイ ドライバーにへの呼び出しが失敗することはできません、 [ **UnlockAsync** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_unlockasync)しない限り、機能、リソースを[ **D3DDDIARG\_UNLOCKASYNC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_unlockasync)構造について説明します、ドライバーの以前の呼び出しによって実際にはロックされていない*LockAsync*関数。 ドライバーでの呼び出しが失敗することはできません同様に、その[**ロックの解除**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_unlock)しない限り、機能、リソースを[ **D3DDDIARG\_ロックの解除**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_unlock)構造について説明します、ドライバーの以前の呼び出しによって実際にはロックされていない*ロック*関数。 リソースが以前ロックされていない状況で*UnlockAsync*と*ロックの解除*戻り\_INVALIDARG します。

 

 





