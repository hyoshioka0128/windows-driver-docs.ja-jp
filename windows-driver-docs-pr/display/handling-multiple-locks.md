---
title: 複数ロックの処理
description: 複数ロックの処理
ms.assetid: d62b9577-d78f-431d-a5bf-c06c9be345c0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 622e57e519251ab48c8546f2f75beffe40e0ef44
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579232"
---
# <a name="handling-multiple-locks"></a>複数ロックの処理


Direct3D、ランタイムでは、頂点バッファーとインデックス バッファーが未処理の 1 つ以上のロックを許可できます。 ユーザー モードのディスプレイ ドライバーがでランタイムと同じ方法には複数のロックの処理する必要があります、 [Windows 2000 Display Driver Model](windows-2000-display-driver-model-design-guide.md)します。

ユーザー モードのディスプレイ ドライバーはへの呼び出しに失敗することはできません、 [ **LockAsync** ](https://msdn.microsoft.com/library/windows/hardware/ff568214)既にロックされているリソース用の関数。 ドライバーでへの呼び出しが失敗することはできません、その*LockAsync*関数の最初の呼び出し後に、特定のリソースの*LockAsync*関数は、そのリソースのロックが成功しました。 ドライバーでの呼び出しが失敗することはできません同様に、その[**ロック**](https://msdn.microsoft.com/library/windows/hardware/ff568213)関数の最初の呼び出し後に、特定のリソースの*ロック*関数が正常にロックします。リソースです。 ランタイムが各呼び出しは、ドライバーを送信すると一致する*LockAsync*ドライバーへの呼び出しで関数を[ **UnlockAsync** ](https://msdn.microsoft.com/library/windows/hardware/ff570105)関数。 ランタイムでは、アプリケーションは、ドライバーを各の呼び出しとも一致*ロック*ドライバーへの呼び出しで関数を[ **Unlock** ](https://msdn.microsoft.com/library/windows/hardware/ff570104)関数。

ユーザー モードのディスプレイ ドライバーにへの呼び出しが失敗することはできません、 [ **UnlockAsync** ](https://msdn.microsoft.com/library/windows/hardware/ff570105)しない限り、機能、リソースを[ **D3DDDIARG\_UNLOCKASYNC**](https://msdn.microsoft.com/library/windows/hardware/ff543395)構造について説明します、ドライバーの以前の呼び出しによって実際にはロックされていない*LockAsync*関数。 ドライバーでの呼び出しが失敗することはできません同様に、その[**ロックの解除**](https://msdn.microsoft.com/library/windows/hardware/ff570104)しない限り、機能、リソースを[ **D3DDDIARG\_ロックの解除**](https://msdn.microsoft.com/library/windows/hardware/ff543394)構造について説明します、ドライバーの以前の呼び出しによって実際にはロックされていない*ロック*関数。 リソースが以前ロックされていない状況で*UnlockAsync*と*ロックの解除*戻り\_INVALIDARG します。

 

 





