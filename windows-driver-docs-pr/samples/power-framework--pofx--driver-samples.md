---
title: 電源フレームワーク (PoFx) ドライバーのサンプル
description: このディレクトリのドライバーサンプルは、デバイスのカスタム PoFx ドライバーを作成するための開始点となります。
ms.assetid: BA2CC8F0-E337-4A5E-987F-1B40213F5983
ms.date: 11/19/2019
ms.localizationpriority: medium
ms.openlocfilehash: dddb23a78991d09cc098b8ec66dd0e049a8ed5fd
ms.sourcegitcommit: 30fa63ad13fd5e2e883b76a44f0703e01049ffa1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74735232"
---
# <a name="power-framework-pofx-driver-samples"></a>電源フレームワーク (PoFx) ドライバーのサンプル

このディレクトリのドライバーサンプルは、デバイスのカスタム PoFx ドライバーを作成するための開始点となります。

| サンプル | 説明 |
| --- | --- |
| [PEP ACPI サンプル](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/pep-acpi-sample) | 電源エンジンプラグイン (PEP) がファームウェアではなく Windows ドライバーを使用してネイティブに ACPI ランタイムメソッドを実装できるようにするインターフェイスを示します。 |
| [UMDF2 PoFx ドライバー](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/power-framework-pofx-sample-umdf-version-2) | UMDF 2 SingleComp サンプルでは、コンポーネントが1つしかないデバイスに対して、UMDF2 ドライバーが F 状態ベースの電源管理を実装する方法を示します。 |
| [WDF PoFx ドライバー](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/kmdf-power-framework-pofx-sample) | KMDF ドライバーが F 状態ベースの電源管理を実装する方法を示す2つのサンプルが含まれています。 SingleComp サンプルは、1つのコンポーネントのみを持つデバイスに対して、KMDF ドライバーが F 状態ベースの電源管理を実装する方法を示しています。 MultiComp サンプルでは、個別の電源管理が可能な任意の数のコンポーネントを持つデバイスに対して、KMDF ドライバーが F 状態ベースの電源管理を実装する方法を示します。 |
