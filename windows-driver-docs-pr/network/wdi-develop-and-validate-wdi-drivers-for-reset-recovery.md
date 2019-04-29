---
title: リセット回復用の WDI ドライバーの開発と検証
description: UE がファームウェアのハングをシミュレートすることでリセットと回復を生じての組み込みのフックです。
ms.assetid: 5C669F22-2C82-4072-8010-1DDC918C064F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed2fc1b25c031378fefa96be457ffb159e7f5c37
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330509"
---
# <a name="develop-and-validate-wdi-drivers-for-reset-recovery"></a>リセット回復用の WDI ドライバーの開発と検証


UE がファームウェアのハングをシミュレートすることでリセットと回復を生じての組み込みのフックです。 UE と LE がない、実際のファームウェア可能性がありますが、シミュレーションの機能を実行します。 コードは、M1 UE でです。 IHV ファームウェア ハングを挿入するためのメカニズムがある場合に最適です。 LE、以下のモジュールの復旧のリセットを実行このバス、ACPI、および UEFI 具体的には。 あった問題をデバッグ ハードこれらの下位レイヤーのリセットの回復が実際には、ファームウェアのリセットに失敗する下位の層に関連します。

 

 





