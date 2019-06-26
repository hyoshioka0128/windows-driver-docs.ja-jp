---
title: ストリーム クラスとミニドライバーのインターフェイス
description: ストリーム クラスとミニドライバーのインターフェイス
ms.assetid: d85510e6-1fd7-442a-bd88-f32b6c13ff75
keywords:
- Stream.sys クラス ドライバー WDK Windows 2000 のカーネル、ストリーム クラスのインターフェイス
- ミニドライバー WDK Windows 2000 のカーネル、ストリーム クラスのインターフェイスのストリーミング
- ミニドライバー WDK Windows 2000 のストリーム、ストリーム クラスのインターフェイス
- stream クラス インターフェイスの WDK ストリーミング ミニドライバー
- される Srb WDK ストリーミング ミニドライバー
- Isr WDK ストリーミング ミニドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa43a1ac64b22cbe5270fba512aef7b4f7bdd5c1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377822"
---
# <a name="stream-class-and-minidriver-interface"></a>ストリーム クラスとミニドライバーのインターフェイス





ストリーム クラスのインターフェイスは、クラス ドライバーと、ミニドライバーの関数呼び出しのセットでは主にします。 クラス ドライバーは、アダプターのハードウェアへのアクセスが必要なアダプター ミニドライバーを呼び出すことの要求フローを制御します。 クラス ドライバーは、マルチプロセッサおよび割り込みの同期を担当します。 クラスのドライバーと、ミニドライバーの両方を初期化すると後、ミニドライバーはパッシブであり、クラス ドライバーによってのみ呼び出されます。 クラスのドライバーに、ミニドライバーから関数呼び出しのほとんどは、低レベルのサービス要求です。

コマンドとミニドライバーに情報を制御する基本的なメカニズムは、*ストリーム要求のブロック*(SRB)。 される Srb のセットは、ドライバーの特定の機能にアクセスするには、各ミニドライバーは提供されており、デバイスでサポートされている各データ ストリームは、通常固有します。 この情報は、大規模な循環バッファー内のオペレーティング システム管理の DMA 経由のデバイスに渡されます。

コマンドとそのコマンドに関連付けられているデータを SRB で構成されます。 A [ **HW\_ストリーム\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_request_block)構造体には、特定の SRB に関連するすべての情報が含まれています。 単に、SRB とも呼ばこの構造体には、コマンドを補足する追加のパラメーターが含まれています。

次の図は、初期化中に、ストリーム クラスと、ミニドライバー間のやり取りを示します。

![初期化中に、ストリーム クラスと、ミニドライバーの間の相互作用を示す図](images/stclassi.png)

ストリーミング ミニドライバー関数をすべて必要に応じて、ミニドライバーを nonreentrant ようにミニドライバーの割り込みサービス ルーチン (ISR) と同期されます。 つまり、ミニドライバーでスレッドを実行しているときに呼び出しになりますありません ISR を含む、ミニドライバー内の他のすべての関数 この nonreentrant 条件は、ミニドライバーを記述しやすく、Windows NT または Windows 2000 のマルチプロセッサ システムであっても、true を保持します。 ストリーム クラス ドライバーを使用して、ストリーミングのミニドライバー (とすべて優先度の低い Irq) の IRQ オフ マスクにより、この nonreentrant 条件を実現**KeSynchronizeExecution**ミニドライバーのルーチンのいずれかでコードを実行するとします。 同期の詳細については、次を参照してください。[ミニドライバー同期](minidriver-synchronization.md)します。

ストリーミングのミニドライバーは、必要に応じて WDM システム サービスを呼び出すことができます。 ただし、ミニドライバーは、デバイス オブジェクトを割り当てられませんが、システムの呼び出しを行うクラス ドライバーのデバイス オブジェクトを使用します。 ほとんどのミニドライバーは、クラス ドライバーから使用可能なすべての必要な機能 WDM システムの呼び出しを実行する必要はありません。

ミニドライバーは、すべてのミニドライバーのエントリ ポイントが IRQL でと呼ばれることに注意してくださいである必要があります&gt;ディスパッチ\_レベル以外の WDM システム サービスの呼び出しを行うときに、 [ **StreamClassCallAtNewPriority** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclasscallatnewpriority)ルーチン。 この関数は IRQL でサービスの呼び出しを許可 = ディスパッチ\_レベルまたはパッシブ\_によって指定された優先度のレベル。 IRQL でこの制限を設定して上書きできます、 **TurnOffSynchronization**でブール値、 [ **HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_initialization_data)構造体を**TRUE**します。

 

 




