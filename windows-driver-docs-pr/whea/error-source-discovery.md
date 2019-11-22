---
title: エラー ソース検出
description: エラー ソース検出
ms.assetid: 58b7501d-b51a-436f-ac29-8d03161d0956
keywords:
- Windows ハードウェアエラーアーキテクチャ WDK、エラーソース検出
- WHEA WDK、エラーソースの検出
- ハードウェアエラー WDK WHEA、エラーソース検出
- エラー WDK WHEA、エラーソース検出
- プラットフォーム固有のハードウェアエラードライバープラグイン WDK WHEA、エラーソース検出
- PSHED プラグイン WDK WHEA、エラーソース検出
- エラーソース検出 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70cd7e1c2cd7fa6865196d83c585d9ac84aa7a46
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844408"
---
# <a name="error-source-discovery"></a>エラー ソース検出


オペレーティングシステムの初期化中に、Windows カーネルは、ハードウェアプラットフォームによって実装されているすべての[エラーソース](hardware-errors-and-error-sources.md)の一覧を照会します。 この手順では、ハードウェアプラットフォームがサポートしている各エラーソースについて説明する、 [**WHEA\_エラー\_ソース\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_source_descriptor)構造体の一覧を返します。 オペレーティングシステムは、この情報を使用して、ハードウェアプラットフォームからのエラー通知を処理するために必要な低レベルのハードウェアエラーハンドラー (LLHEHs) を有効にします。

次に示すのは、PSHED 検出されたエラーソースの最小セットです。

<a href="" id="x86-based-and-x64-based-hardware-platforms"></a>**x86 ベースおよび x64 ベースのハードウェアプラットフォーム**  
-   コンピューターチェックの例外 (MCE)

-   コンピューターチェック (CMC) を修正しました

-   Nonmaskable Interrupt (NMI)

-   ブートエラー

<a href="" id="itanium-based-hardware-platforms"></a>**Itanium ベースのハードウェアプラットフォーム**  
-   コンピューターチェックの中止 (MCA)

-   コンピューターチェック (CMC) を修正しました

-   修正されたプラットフォームエラー (送付状)

-   INIT エラー

PCI Express (PCIe) の高度なエラー報告 (AER) の場合、PCI バスドライバーは、エラーソースを検出せずに検出します。 このため、Windows カーネルに返されるエラーソースの最初の一覧に、PCIe AER エラーソースは含まれません。 代わりに、PCI バスドライバーは、これらのエラーソースをオペレーティングシステムに報告します。 このようなエラーソースがオペレーティングシステムに報告されると、Windows カーネルは、エラーソースに関する追加情報を提供するために、pshed を呼び出します。

また、pshed プラグインは、エラーソースの検出に参加して、PSHED 報告されるエラーソース情報を変更し、pshed 検出されなかった追加のエラーソースを報告することもできます。 エラーソースの検出に関与し、pshed サポートされていない追加のエラーソースをオペレーティングシステムに報告する、pshed プラグインが実装されている場合は、これらの追加のエラーソースに対するエラーソース管理およびエラー情報の取得操作をサポートするために、[エラー](error-source-control.md)ソース管理およびエラー[情報の取得](error-information-retrieval.md)にも参加する必要があります。 エラーソースの検出に参加する PSHED プラグインを実装する方法の詳細については、「[エラーソースの検出に参加](participating-in-error-source-discovery.md)する」を参照してください。

 

 




