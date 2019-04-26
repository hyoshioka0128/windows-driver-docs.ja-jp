---
title: I/O の一般的なプログラミング手法
description: I/O の一般的なプログラミング手法
ms.assetid: c310829f-e102-4a96-aa3e-39136b8a641b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d0441ff7e12e6ada42b5d46d8836a22f929bf517
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359942"
---
# <a name="general-io-programming-techniques"></a>I/O の一般的なプログラミング手法


入出力のプログラミングで最も重要な手法の 1 つは避ける必要のある 1 つ: オペレーティング システムのデバイスの待機を強制します。 ほとんどすべてのユーザーを「固定」表示の Microsoft Windows のエクスペリエンスとしました。 Freeze はにより、クラッシュが他にもデバイスが応答するために、システムが待機していますがあります。

デバイスの待機を処理するため 2 つの基本的な方法でプログラミングに方法があります:*同期*と*非同期*します。 同期プログラミングでは、デバイスを待機し、避ける必要があります。 非同期プログラミング (割り込み要求を待機中) などの他の手法を使用します。 同期および非同期プログラミングの詳細については、次のトピックを参照してください。

[同期 I/O のプログラミング](synchronous-i-o-programming.md)

[I/O の非同期プログラミング](asynchronous-i-o-programming.md)

Microsoft Vista では、同期プログラミングの問題に対処するための新しいポリシーを持ちます。 この新しいポリシーの詳細については、次を参照してください。 [Windows Vista での待機を制限する](restricting-waits-in-vista.md)詳細についてはします。

プログラミング以前のデバイス ドライバー、ドライバーは、回答が提供されるまで、ドライバーから情報を繰り返し要求する必要があります。 この手法では、ポーリングは呼び出され、ほとんどないを使用する必要があります。 ポーリングの問題に対処する最善の方法では、ハードウェアの割り込みを使用します。 ハードウェアの割り込みの詳細については、次を参照してください。[サービス割り込み](servicing-interrupts.md)します。 ポーリングといないを使用する理由の詳細については、次を参照してください。[デバイスのポーリングを回避](avoid-polling-devices.md)します。

 

 




