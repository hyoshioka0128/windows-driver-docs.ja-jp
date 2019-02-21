---
title: C28131
description: C28131、DriverEntry ルーチンの警告と、I/O マネージャー バッファーを解放するため、ポインターではなく、引数のコピーを保存する必要があります。
ms.assetid: 9661f17e-a19a-4230-a848-8233f635db09
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28131
ms.openlocfilehash: e6933b3a4c67a0ad71f2f4b372b4331944678e24
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550661"
---
# <a name="c28131"></a>C28131


C28131 を警告します。DriverEntry ルーチンは I/O マネージャー バッファーを解放するため、ポインターではなく、引数のコピーを保存する必要があります。

ドライバーの*DriverEntry*ルーチンが、バッファー、バッファーのコピーを保存せずに、ポインターのコピーを保存しています。 バッファーが解放されるため、ときに、 *DriverEntry*ルーチンを返します、バッファーへのポインターは、すぐに無効になります。

 

 





