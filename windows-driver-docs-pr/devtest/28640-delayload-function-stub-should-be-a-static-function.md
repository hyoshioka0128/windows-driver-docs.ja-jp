---
title: C28640
description: 警告 C28640 関数遅延読み込みスタブ静的関数である必要があります。
ms.assetid: 7e4c675b-5f5c-461a-bf80-cd7ba0d8832c
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28640
ms.openlocfilehash: bda1348cb0f840a010fd006c427f1d894f8a93be
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559982"
---
# <a name="c28640"></a>C28640


警告 C28640: 関数遅延読み込みスタブは静的関数である必要があります

遅延読み込みのすべてのライブラリが静的には必要ありませんシンボリック エクスポートをします。 これにより、遅延読み込みスタブ関数にリンクできます予期しないソフトウェアがありません。 このガイドラインに準拠していない場合、バイナリは可能性のある不適切な使用可能性のあるエクスポートを公開します。

 

 





