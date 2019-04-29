---
title: C28752
description: 警告の kernel32 または advapi32 API の使用状況を C28752 が禁止されています。
ms.assetid: F887EB9E-FA5A-4139-AF67-7460BB9254B8
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28752
ms.openlocfilehash: fad7a7e4a6751f0f5a485e377686727935a8cbc3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330994"
---
# <a name="c28752"></a>C28752


C28752 を警告します。Kernel32 または advapi32 の API の使用を禁止されています。

この警告は、関数が使用されていることを非推奨とされましたがコア システムの一部である優先置換を示します。

コア システム バイナリが kernel32 と advapi32 には、機能の多くを提供しますが、多くの場合は、別の API 呼び出しが必要です。 コア システム Api を呼び出すことは高速であり、レガシ kernel32 または advapi32 Api を呼び出すよりも小さいメモリ フット プリントが必要です。

 

 





