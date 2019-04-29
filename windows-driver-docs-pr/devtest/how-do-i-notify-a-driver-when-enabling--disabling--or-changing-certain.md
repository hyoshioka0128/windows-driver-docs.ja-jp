---
title: 有効にすると、無効化、または特定のフラグを変更するときにドライバーを通知する方法
description: 有効にすると、無効化、または特定のフラグを変更するときにドライバーを通知する方法
ms.assetid: 1bdf8047-8d3f-4cdf-883b-3544dea06705
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa2f2156dcf1d1917d44fb7abb33af31c08533a5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329737"
---
# <a name="how-do-i-notify-a-driver-when-enabling-disabling-or-changing-certain-flags"></a>特定のフラグの有効化、無効化、変更をドライバーに通知する方法


一部のドライバーは、トレース フラグが有効になっている、無効になっている、または変更されたときに、追加の作業を行う必要があります。 このような変更が発生したときに、ドライバーを通知するには、次のコマンドを使用します。

```
#define WPP_PRIVATE_ENABLE_CALLBACK 
```

TMH ファイルをインクルードする前に、このシンボリック定数を定義する必要があります。 記述する必要があります関数のシグネチャは次のとおりです。

```
typedef
VOID
(*PFN_WPP_PRIVATE_ENABLE_CALLBACK)(
__in LPCGUID Guid,
__in __int64 Logger,
__in BOOLEAN Enable,
__in ULONG Flags,
__in UCHAR Level);
```

特定のフラグが有効にすると、ドライバーに通知する方法の例を次に示します。

```
#define WPP_PRIVATE_ENABLE_CALLBACK MyOwnCallback
#include "tracedrv.tmh" // this is the file that will be auto-generated 
VOID MyOwnCallback (
                 __in LPCGUID Guid,
                 __in __int64 Logger,
                 __in BOOLEAN Enable,
                 __in ULONG Flags,
                 __in UCHAR Level) 
{
//                
//                  This callback function will be called with the current values of : GUID, Logger, Enable, Flags, and Level
//                 

                  if (Enable) {
                        .
                        .
                   }
} 
```









