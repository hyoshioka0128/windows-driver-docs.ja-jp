---
title: C28157
description: 警告 C28157、IRQL が復元されたことはありません。
ms.assetid: 3c60253f-5d89-4bb7-9787-9a2aa42bf7fb
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28157
ms.openlocfilehash: 1314dab061dfe7c82dba8a4f7e17c2e5f00fb79e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361348"
---
# <a name="c28157"></a>C28157


C28157 を警告します。IRQL が復元されたことはありません。

現在の関数が、  **\_IRQL\_復元\_** 注釈を完了すると、ドライバーが実行すべき前 IRQL の値から復元された IRQL で必要があります。 ただし、これには、ドライバーを実行しているさまざまな IRQL で関数が完了したときに、少なくとも 1 つのパスがあります。

 

 





