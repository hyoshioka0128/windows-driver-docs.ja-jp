---
title: セキュリティの脅威を最小限に抑える、ファイル システムを実装します。
description: セキュリティの脅威を最小限に抑える、ファイル システムを実装します。
ms.assetid: a7c974ee-9f0b-4a51-aa56-5c67ee2d1180
keywords:
- 脅威を最小限に抑え、セキュリティ WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a21f793875cebe4e8c393186550760bc36702a92
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532662"
---
# <a name="implementing-file-systems-to-minimize-security-threats"></a>セキュリティの脅威を最小限に抑える、ファイル システムを実装します。


## <span id="ddk_implementing_to_minimize_security_threats_if"></span><span id="DDK_IMPLEMENTING_TO_MINIMIZE_SECURITY_THREATS_IF"></span>


セキュリティの脅威となる実装の問題は、一連の一般的な問題に分類されます。

-   バッファー処理します。

-   認証と識別します。

-   アクセス制御。

-   管理を処理します。

特に、これらの問題の小説します。 これらの問題はよく知られていない、ドライバーでこれらの問題が再び発生します。 問題の一部は、既存のほとんどの開発ツールのユーザーに警告またはこの種の問題を緩和するためはありません。 ただし、賢く防御的な開発手法を使用して、これらの問題のほとんど削除できます。

ここでは、次のトピックについて説明します。

[バッファー処理](buffer-handling.md)

[認証と Id](authentication-and-identification.md)

[アクセス制御](access-control.md)

[ハンドルの管理](handle-management.md)

 

 




