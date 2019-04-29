---
title: プライマリ割り込みとセカンダリ割り込み
description: GPIO 割り込み処理が 2 段階のプロセスでは本質的にします。
ms.assetid: 731B0E36-4480-4B69-931E-1F7B40B18911
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00b906a6232ee9912c58c5c0c819e43f110c5044
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326121"
---
# <a name="primary-and-secondary-interrupts"></a>プライマリ割り込みとセカンダリ割り込み


GPIO 割り込み処理が 2 段階のプロセスでは本質的にします。 GPIO フレームワーク拡張機能 (GpioClx) 割り込みサービス ルーチン (ISR) を実行するとの汎用的な I/O (GPIO) コントローラからの割り込みと呼ばれる、*プライマリ割り込み*します。 この ISR では、グローバル システムの割り込み (GSI) に割り込む GPIO ピンをマップし、ハードウェア アブストラクション レイヤー (HAL) にこの GSI を渡します。 HAL を生成、*セカンダリ割り込み*を通じてこの GSI GPIO ピンに論理的に接続されている 2 つ目の ISR を実行します。 このプロセスはダイアグラムに示した[GPIO ドライバー サポートの概要](https://msdn.microsoft.com/library/windows/hardware/hh439512#gpio-block-diagram)します。

GpioClx では、ISR 割り込みの入力として構成されている GPIO ピンから GPIO コント ローラーを受信するサービスの割り込み要求を実装しています。 周辺機器、GPIO ピンの割り込みをアサートすると、割り込みを有効になっているし、GPIO コント ローラーにマスク解除されて、GPIO コント ローラーのハードウェアは、プロセッサに割り込みをアサートします。 この割り込みに応答して、GpioClx クエリで ISR、割り込みを生成し、どの GSI を決定し、GPIO ピンを識別するために GPIO コント ローラーに代入されますこのピン留めします。 GpioClx ISR パス、HAL および HAL をこの GSI、GSI に論理的に接続されている ISR を呼び出します。

通常、この 2 つ目の ISR は、GPIO ピンの割り込みをアサート周辺機器のデバイスのドライバーに属しています。 周辺機器のデバイス ドライバを論理的に接続する方法の ISR GPIO 割り込み暗証番号 (pin) については、次を参照してください。 [GPIO-Based 割り込みリソース](https://msdn.microsoft.com/library/windows/hardware/hh698246)します。

 

 




