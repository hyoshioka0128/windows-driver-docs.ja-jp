---
title: C28636
description: C28636 呼び出す LocalFree を呼び出しています、グループ、Dacl または Sacl の呼び出しから取得した未割り当てのポインターで警告します。
ms.assetid: cad12c6c-5d65-4c5b-98fa-4e0fa9e75166
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28636
ms.openlocfilehash: df20050c95648d23215b283cd4e7cb22056d0877
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557953"
---
# <a name="c28636"></a>C28636


C28636 を警告します。呼び出しています、グループ、Dacl または Sacl の呼び出しから取得した未割り当てのポインターで LocalFree を呼び出してください。

これらの関数にはメモリの割り当て — で渡されたポインターを設定します。 このためは、そのポインターを使用してメモリを解放が正しくありません。

 

 





