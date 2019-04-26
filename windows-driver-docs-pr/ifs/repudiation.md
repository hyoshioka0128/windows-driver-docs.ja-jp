---
title: 否認
description: 否認
ms.assetid: ccb50b6c-9e7d-4a90-a049-6c62b1b57376
keywords:
- 脅威モデルの WDK ファイル システム、否認不可
- セキュリティの脅威は、WDK のファイル システム、否認不可をモデル化します。
- 否認不可 WDK ファイル システム
- 所有権の WDK ファイル システム
- WDK ファイル システムの操作を実行を拒否します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6bfcea232582eb22b2e158eef38bb085df1994b1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344574"
---
# <a name="repudiation"></a>否認


## <span id="ddk_repudiation_if"></span><span id="DDK_REPUDIATION_IF"></span>


否認不可の概念は、ユーザーが特定の操作を実行してし、その後を拒否することを実行可能性があります。 ほとんどのドライバーの問題の異常の種類になります。 ファイル システムでは、ただし、ログ記録に使用されます (たとえば、重要なファイルの削除) 操作を追跡し、操作の明確な痕跡があることを確認します。 これは、に対してこのような否認不可を確保するためのメカニズムを提供します。

さらに、オペレーティング システムでは、特定のセキュリティ識別子にオブジェクトの所有権を割り当てることができます。 適切な権限を持たない所有権情報を変更ことはできません (**SeTakeOwnershipPrivilege**) 特定のオブジェクトの所有権を追跡できるようにします。 オブジェクトの所有権を別の形式の否認不可に対する保護を提供します。

 

 




