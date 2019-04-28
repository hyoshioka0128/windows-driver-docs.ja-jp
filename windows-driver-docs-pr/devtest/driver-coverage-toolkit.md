---
title: Driver Coverage Toolkit
description: Toolkit モニターのドライバの対応とレポートは、さまざまな I/O 要求パケット (Irp) を入力するかのドライバー スタックのままにするには、デバイスを指定します。
ms.assetid: b35ca87e-9ec7-4e25-89ce-0e7c121f6445
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5facc6b1d8962aad294e99983f4a6372bfd407ca
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380614"
---
# <a name="driver-coverage-toolkit"></a>Driver Coverage Toolkit


Toolkit モニターのドライバの対応とレポートは、さまざまな I/O 要求パケット (Irp) を入力するかのドライバー スタックのままにするには、デバイスを指定します。 ドライバの対応ツールキットからのデータは、ドライバーのテストおよび検証中にカバレッジの弱点を識別できます。

**注**  ドライバーのカバレッジ Toolkit は Windows 10 で不要になったと、インストーラーが WDK に含まれていません。 ここで説明されている Windows 10 でタスクを実行する代わりに使用[Driver Verifier](driver-verifier.md)と[IRP のログ記録](irp-logging.md)します。

 

ドライバの対応 toolkit は Windows Driver Kit (WDK) で含まれているし、の一部として Visual Studio から実行、[デバイス基礎テスト](device-fundamentals-tests.md)します。

ドライバの対応 toolkit は、次のツールで構成されます。

-   [ドライバー カバレッジ フィルター ドライバー](driver-coverage-filter-driver.md) (Drvcov.sys) IRP の要求を監視するには、1 つまたは複数の指定したデバイスのドライバー スタックの出入りします。

-   ドライバーのカバレッジ ツールとして使用できますの一部、[デバイス基礎テスト](device-fundamentals-tests.md)を参照してください[カバレッジのテスト (デバイスの基本)](coverage-tests--device-fundamentals-.md)します。 これらのツールを使用して、有効にするか、指定したデバイスは、IRP のカバレッジを無効にするだけでなくカバレッジ データからレポートを作成することができます。

インストールして、大きな影響を与えることがなく、テスト コンピューターでドライバーのカバレッジ ツールキットを実行することができます。 これらのツールがない IRP の要求を変更またはデバイスのドライバー スタックに追加の Irp を挿入しないでください。 これらのツールは、単に入るか出るデバイス ドライバーをすべての IRP でデータを収集します。

ドライバの対応 toolkit は、Windows Vista 以降のバージョンの Windows を実行するシステムでサポートされます。

このセクションでは、次のトピックについて説明します。

[ドライバーのカバレッジ Toolkit の概要](overview-of-the-driver-coverage-toolkit.md)

[カバレッジ フィルター ドライバーのドライバー](driver-coverage-filter-driver.md)

[IRP カバレッジ データを収集する方法](how-to-collect-irp-coverage-data.md)

[IRP カバレッジ データを分析する方法](how-to-analyze-irp-coverage-data.md)

 

 





