---
title: マスター クロック
description: マスター クロック
ms.assetid: 87a99371-9c72-4310-bcc7-02af19207b3e
keywords:
- DVD デコーダー ミニドライバー WDK、マスターのクロック
- デコーダー ミニドライバー WDK DVD、マスターのクロック
- マスターのクロックの WDK DVD デコーダー
- WDK DVD デコーダーをクロックします。
- オンボードのクロックの WDK DVD デコーダー
- 現在のストリームに WDK DVD デコーダー
- 時間の WDK DVD デコーダー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d46beaa0a86bab16a8cce854408dc1ea6af18fb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386638"
---
# <a name="master-clock"></a>マスター クロック





DVD デコーダーのミニドライバーは、指定したストリームがマスターの時計の情報を提供することのできる可能性があります。 これは、ストリームは、1 つの他のすべてのユーザーが同期化する必要がありますを示します。 SRB 構造体のメンバーを 2 つだけが必要です。

*HwClockFunction*メンバー時計の情報への呼び出しを処理する DVD デコーダー ミニドライバー ルーチンへのポインターに設定されます。 ときに、ルーチンが設定、SRB\_オープン\_マスター クロック ストリームのストリームの呼び出しを受信します。 これは、ストリームがシステムのマスター クロックをすることのできることを示します。

*ClockSupportFlags*のメンバー、 [ **HW\_クロック\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_clock_object)構造体は、次の値のいずれかに設定します。

<a href="" id="clock-support-can-set-onboard-clock"></a>クロック\_サポート\_できます\_設定\_オペレーション インサイト理解\_クロック  
デバイスは任意の値をオンボードのクロック時間を変更することができますを示します。

<a href="" id="clock-support-can-read-onboard-clock"></a>クロック\_サポート\_できます\_読み取り\_オペレーション インサイト理解\_クロック  
ハードウェアからこのストリームの現在の時刻を読み取ることができることを示します。 このクロックがストリームの現在の時刻に関連付けるために、オンボードのクロックの 100 ナノ秒単位で値を返すには、ドライバーの機能だけを示します。

<a href="" id="clock-support-can-return-stream-time"></a>クロック\_サポート\_できます\_返す\_ストリーム\_時間  
このストリームは、ハードウェアで処理されている現在のストリームの時刻を返すことができますを示します。

詳細については、次を参照してください。[マスター クロック](master-clocks.md)します。

 

 




