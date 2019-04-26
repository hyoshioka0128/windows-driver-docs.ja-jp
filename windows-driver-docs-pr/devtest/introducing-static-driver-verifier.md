---
title: 静的ドライバー検証ツールとは
description: 静的ドライバー検証ツールとは
ms.assetid: fa6e8b0f-0d0f-4293-87ec-e67decd6acb7
keywords:
- Static Driver Verifier WDK、Static Driver Verifier について
- StaticDV WDK、Static Driver Verifier について
- SDV の WDK、Static Driver Verifier について
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6bb44e32f323c409d8f0d8930d2e289ad0210d2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356534"
---
# <a name="introducing-static-driver-verifier"></a>静的ドライバー検証ツールとは


Static Driver Verifier (SDV) は、コンパイル時に実行する静的検証ツールです。 オペレーティング システムの状態と、ドライバーの初期状態について最小限の可能な推測すること、ソース コードをシンボリックに実行をドライバー コード内のパスがについて説明します。 その結果、SDV は、パスで従来のテストが欠落しているコードを実行することができます。

SDV には、ドライバーとオペレーティング システム カーネルの間の適切な相互作用を定義するルールが含まれています。 検証の際は、SDV は、ドライバーのコードと、ドライバー、規則に違反していることを証明するためにしようとして、使用するライブラリ コードの該当する各分岐を調べます。 SDV は、違反を証明するために失敗した場合、ドライバーが、ルールに準拠しており、検証を渡すことを報告します。

このセクションの内容:

[Static Driver Verifier をについてください。](understanding-static-driver-verifier.md)

[Static Driver Verifier の概念](static-driver-verifier-concepts.md)

[サポートされているドライバー](supported-drivers.md)

[Static Driver Verifier の制限事項](static-driver-verifier-limitations.md)

 

 





