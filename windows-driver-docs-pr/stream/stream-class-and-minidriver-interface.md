---
title: Stream クラスとミニドライバーインターフェイス
description: Stream クラスとミニドライバーインターフェイス
ms.assetid: d85510e6-1fd7-442a-bd88-f32b6c13ff75
keywords:
- .Sys クラスドライバー WDK Windows 2000 カーネル、ストリームクラスインターフェイス
- streaming ミニドライバー WDK Windows 2000 カーネル、stream クラスインターフェイス
- ミニドライバー WDK Windows 2000 カーネルストリーミング、stream クラスインターフェイス
- stream クラスインターフェイス WDK streaming ミニドライバー
- SRBs WDK streaming ミニドライバー
- Isr WDK streaming ミニドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44aaf8add9a36e99462f792ca90312425a439447
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837691"
---
# <a name="stream-class-and-minidriver-interface"></a>Stream クラスとミニドライバーインターフェイス





Stream クラスインターフェイスは、主にクラスドライバーとミニドライバー間の関数呼び出しのセットです。 クラスドライバーは、アダプターのハードウェアへのアクセスが必要な場合にアダプターミニドライバーを呼び出すことで、要求フローを制御します。 クラスドライバーは、マルチプロセッサと割り込み同期を担当します。 クラスドライバーとミニドライバーの両方が初期化されると、ミニドライバーはパッシブになり、クラスドライバーによってのみ呼び出されます。 ミニドライバーからクラスドライバーへの関数呼び出しのほとんどは、低レベルのサービス要求です。

コマンドと情報をミニドライバーに制御する基本的なメカニズムは、*ストリーム要求ブロック*(SRB) です。 SRBs のセットは、各ミニドライバーがドライバーの特定の機能にアクセスするために用意されており、通常はデバイスでサポートされている各データストリームに固有です。 この情報は、オペレーティングシステムによって制御される DMA を介して、大きな循環バッファーでデバイスに渡されます。

SRB は、コマンドと、そのコマンドに関連付けられたデータで構成されます。 [**ハードウェア\_ストリーム\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)構造には、特定の SRB に関連するすべての情報が含まれます。 この構造体 (多くの場合、単に単に SRB と呼ばれます) には、コマンドを補完するための追加のパラメーターが含まれています。

次の図は、初期化時のストリームクラスとミニドライバーの相互作用を示しています。

![初期化中にストリームクラスとミニドライバーの間の相互作用を示す図](images/stclassi.png)

必要に応じて、すべての streaming ミニドライバー関数をミニドライバーの interrupt service ルーチン (ISR) と同期して、ミニドライバー nonreentrant にします。 つまり、ミニドライバーでスレッドが実行されている場合、ミニドライバー内の他の関数 (ISR を含む) に対する呼び出しは行われません。 この非再入可能な条件は、マルチプロセッサの Windows NT/Windows 2000 システムであっても、ミニドライバーを簡単に記述できるようにするためのものです。 Stream クラスドライバーは、ミニドライバーのルーチンでコードを実行するときに、 **KeSynchronizeExecution**を使用してストリーミングミニドライバー (およびすべての優先度の低い irq) の IRQ をマスクすることによって、この非再入条件を実現します。 同期の詳細については、「[ミニドライバー synchronization](minidriver-synchronization.md)」を参照してください。

Streaming ミニドライバーは、必要に応じて WDM システムサービスを呼び出すことができます。 ただし、ミニドライバーはデバイスオブジェクトを割り当てませんが、クラスドライバーの device オブジェクトを使用してシステム呼び出しを行います。 すべての必要な機能はクラスドライバーから使用できるため、ほとんどのミニドライバーでは、WDM システム呼び出しを行う必要はありません。

ミニドライバーは、WDM システムサービスの呼び出しを行うときに、 [**Streamclasscallatnewpriority**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclasscallatnewpriority)ルーチンを除き、すべてのミニドライバーエントリポイントが IRQL &gt; ディスパッチ\_レベルを呼び出すことに注意する必要があります。 この関数は、指定された優先度に応じて、IRQL = ディスパッチ\_レベルまたはパッシブ\_レベルでのサービス呼び出しを許可します。 この IRQL に対する制限は、 [**HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_initialization_data)構造体の**TurnOffSynchronization**ブール値を**TRUE**に設定することによってオーバーライドできます。

 

 




