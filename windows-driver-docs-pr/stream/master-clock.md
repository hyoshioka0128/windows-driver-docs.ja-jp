---
title: マスター クロック
description: マスター クロック
ms.assetid: 87a99371-9c72-4310-bcc7-02af19207b3e
keywords:
- DVD デコーダーミニドライバー WDK、マスタークロック
- デコーダーミニドライバー WDK DVD、マスタークロック
- マスタークロック WDK DVD デコーダー
- 時計 WDK DVD デコーダー
- オンボードクロック WDK DVD デコーダー
- 現在のストリーム時間 WDK DVD デコーダー
- time WDK DVD デコーダー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60f8408021acc3b5b76d6da1230ebdce60fe0607
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838041"
---
# <a name="master-clock"></a>マスター クロック





DVD デコーダーミニドライバーは、特定のストリームがマスタークロック情報を提供できることを示している場合があります。 これは、他のすべてのが同期する必要があるストリームであることを示しています。 SRB 構造体のメンバーは2つだけ必要です。

*HwClockFunction*メンバーは、クロック情報の呼び出しを処理する DVD デコーダーミニドライバールーチンへのポインターに設定されます。 ルーチンが設定されるのは、マスタークロックストリームに対して、SRB\_OPEN\_ストリーム呼び出しを受信したときです。 これは、ストリームがシステムのマスタークロックになることができることを示します。

[**HW\_CLOCK\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_clock_object)構造の*clocksupportflags*メンバーは、次のいずれかの値に設定されます。

<a href="" id="clock-support-can-set-onboard-clock"></a>クロック\_サポート\_\_オンボード\_時計に\_設定できます  
デバイスが、オンボードのクロック時間を任意の値に変更できることを示します。

<a href="" id="clock-support-can-read-onboard-clock"></a>クロック\_サポート\_\_\_オンボード\_時計  
このストリームの現在のクロック時間をハードウェアから読み取ることができることを示します。 このクロックは、現在のストリーム時間に関連付けられている必要はありません。これは、ドライバーが、オンボードクロックの100ナノ秒単位の値を返す機能を示しているだけです。

<a href="" id="clock-support-can-return-stream-time"></a>クロック\_サポート\_は\_ストリーム\_時間を返す\_  
このストリームが、ハードウェアで処理されている現在のストリームの時間を返すことができることを示します。

詳細については、「[マスタークロック](master-clocks.md)」を参照してください。

 

 




