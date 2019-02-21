---
title: C28625
description: 使用して機密データをクリア警告 C28625 関数の呼び出しは最適化されます。
ms.assetid: 9ae44fbc-9a56-41e4-9972-d76d9b62033c
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28625
ms.openlocfilehash: 49384914d5f3f3f3f834d5eba57ace3743e0cfd1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548602"
---
# <a name="c28625"></a>C28625


C28625 を警告します。機密データをクリアするために使用する関数呼び出しは最適化します。

現在の関数呼び出しは、メモリ内で機密データが常になることが、コンパイル時に最適化された可能性があります。 使用して、 **SecureZeroMemory**または**RtlSecureZeroMemory**代わりに機能します。 ヒューリスティックは、「キー」やこの警告をトリガーするには、"pass"などの項目を含む識別子の名前を検索します。

 

 





