---
title: KMDF ドライバーからのバグ チェック
description: KMDF ドライバーからのバグ チェック
ms.assetid: 4fde9586-3455-4692-8eeb-bbf64c0a437e
keywords:
- ドライバーのデバッグ WDK KMDF、バグチェック
- WDK KMDF のバグチェック
- KMDF コードを検証しています
- KMDF バグチェック WDK
- WDF_VIOLATION
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fb20e1e13db1882fb3d9e85290b887541d49045
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845507"
---
# <a name="bug-checks-from-kmdf-drivers"></a>KMDF ドライバーからのバグ チェック


フレームワークは、フレームワークベースのドライバーから複数の種類のエラーをチェックします。 これらのエラーのいずれかが発生すると、フレームワークによって WDF\_違反のバグチェックが作成されます。

フレームワークがチェックするドライバーエラーの種類の詳細については、「 [**WDF\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x10d---wdf-violation)」を参照してください。

ドライバーは、 [**WdfVerifierKeBugCheck**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfverifier/nf-wdfverifier-wdfverifierkebugcheck)を呼び出すことによってバグチェックを作成できます。

 

 





