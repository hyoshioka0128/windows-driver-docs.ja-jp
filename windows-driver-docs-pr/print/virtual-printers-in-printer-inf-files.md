---
title: プリンターの INF ファイルでの仮想プリンター
description: プリンターの INF ファイルでの仮想プリンター
ms.assetid: a7308b0f-61b8-4b4d-a116-ce940787882b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28140db763668d9bc01fb9cedb1f004f9739590a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538922"
---
# <a name="virtual-printers-in-printer-inf-files"></a>プリンターの INF ファイルでの仮想プリンター


仮想プリンターは、fax サーバーの物理プリンターではない、電子ドキュメントなどの出力先です。 仮想プリンターは、ハードウェア ID があるないため、表す必要がある、プリンターの INF ファイルで null ハードウェア id

INF ファイルで、null のハードウェア ID を挿入するには、インストール セクション名と、互換性のある ID 間 INF のモデル セクションに 2 つ目のコンマを追加します。 次の例では、指定された fax プリンターの null のハードウェア ID を作成する方法を示します。

```cpp
"Objectworld Fax Printer"=OWFAX,,Objectworld_Fax_Printer
```

INF ファイルでの仮想プリンターの詳細については、次を参照してください。 **DriverCategory**で[プリンター INF ファイルのエントリ](printer-inf-file-entries.md)します。

 

 




