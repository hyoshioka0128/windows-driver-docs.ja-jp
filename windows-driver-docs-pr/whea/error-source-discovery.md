---
title: エラー ソースの検出
description: エラー ソースの検出
ms.assetid: 58b7501d-b51a-436f-ac29-8d03161d0956
keywords:
- Windows ハードウェア アーキテクチャ WDK のエラー、エラー ソースの検出
- WHEA WDK、エラー ソースの検出
- ハードウェア エラー WDK WHEA、エラー ソースの検出
- エラー WDK WHEA、エラー ソースの検出
- プラットフォーム固有のハードウェア エラー ドライバー プラグインを WDK WHEA、エラー ソースの検出
- PSHED プラグイン WDK WHEA、エラー ソースの検出
- WDK WHEA エラー ソースの検出
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e3bc3c4e90efb599b74768a0df920c874141239
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553268"
---
# <a name="error-source-discovery"></a>エラー ソースの検出


オペレーティング システムの初期化中に、Windows カーネルのクエリのすべての一覧については PSHED、[エラー ソース](hardware-errors-and-error-sources.md)ハードウェア プラットフォームにより実装されます。 一覧を返します、PSHED [ **WHEA\_エラー\_ソース\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff560505)の各ハードウェア プラットフォームをサポートするエラーのソースを記述する構造体. オペレーティング システムでは、この情報を使用して、、ハードウェア プラットフォームからのエラー通知を処理するために必要な低レベル ハードウェア エラー ハンドラー (LLHEHs) を有効にします。

次は、PSHED で検出されたエラーのソースの最小セットです。

<a href="" id="x86-based-and-x64-based-hardware-platforms"></a>**x86 ベースおよび x64 ベースのハードウェア プラットフォーム**  
-   マシン チェック例外 (MCE)

-   マシン チェック (CMC) を修正しました

-   マスク不可能割り込み (NMI)

-   起動エラー

<a href="" id="itanium-based-hardware-platforms"></a>**Itanium ベースのハードウェア プラットフォーム**  
-   マシン チェック中止 (MCA)

-   マシン チェック (CMC) を修正しました

-   修正されたプラットフォーム エラー (CPE)

-   初期化エラー

PCI express 詳細エラー報告 (AER) (PCIe) の場合は、PCI バス ドライバーは、PSHED ではなく、エラーのソースを検出します。 そのため、PSHED は、Windows カーネルに返されるエラー ソースの初期リストに、PCIe AER エラーのソースを含めない。 代わりに、PCI バス ドライバーは、オペレーティング システムにこれらのエラーのソースを報告します。 ときに、このようなエラーの発生元は、エラーの発生元に関する追加の詳細を提供するよう PSHED を許可する、PSHED には、Windows カーネルの呼び出しで、オペレーティング システムに報告されます。

PSHED のプラグインは、エラー ソースの検出、PSHED で報告されるエラーのソース情報を変更して、レポート、PSHED で検出されなかったその他のエラーのソースにも参加できます。 エラー ソースの検出に参加して、追加のエラーのソースを PSHED をサポートしないオペレーティング システムに報告されたプラグイン PSHED が実装されている場合 PSHED をプラグインする必要がありますにも参加[エラー ソース制御](error-source-control.md)と[エラー情報の取得](error-information-retrieval.md)エラー ソースの管理とこれらの追加のエラーのソースのエラー情報の取得操作をサポートします。 エラー ソースの検出に参加している PSHED プラグインを実装する方法の詳細については、次を参照してください。[エラー ソースの検出に参加している](participating-in-error-source-discovery.md)します。

 

 




