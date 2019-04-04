---
title: KMDF ドライバーからのバグ チェック
description: KMDF ドライバーからのバグ チェック
ms.assetid: 4fde9586-3455-4692-8eeb-bbf64c0a437e
keywords:
- WDK KMDF ドライバーをデバッグするには、バグを確認します
- WDK KMDF のバグ チェック
- KMDF コードの検証
- KMDF バグは、WDK を確認します。
- WDF_VIOLATION
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 776ea4eb7b2135b7599e0a657a8084c8447236f0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573005"
---
# <a name="bug-checks-from-kmdf-drivers"></a>KMDF ドライバーからのバグ チェック


フレームワークはフレームワーク ベースのドライバーからのエラーのいくつかの型をチェックします。 これらのエラーが発生した場合、フレームワークを作成、WDF\_違反のバグ チェックします。

フレームワークをチェックするドライバー エラーの種類については、[ **WDF\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff557235)を参照してください。

ドライバーは、呼び出すことによってバグ チェックを作成できます[ **WdfVerifierKeBugCheck**](https://msdn.microsoft.com/library/windows/hardware/ff551166)します。

 

 





