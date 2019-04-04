---
title: 割り込みオブジェクトの作成
description: 割り込みオブジェクトの作成
ms.assetid: 8bea7498-9fee-4d84-9e6b-976102c54876
keywords:
- ハードウェアの割り込み WDK KMDF、オブジェクトの作成
- WDK KMDF、オブジェクトの作成を中断します。
- メッセージ シグナル割り込み WDK KMDF
- Msi WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5466e4b38f4c6ca08318e572eb2b7cb856a33143
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578338"
---
# <a name="creating-an-interrupt-object"></a>割り込みオブジェクトの作成


デバイスのハードウェアの割り込みを処理する Windows Driver Frameworks (WDF) ドライバーは、各デバイスをサポートする各割り込みの framework 割り込みオブジェクトを作成する必要があります。 Framework version 1.11 および Windows 8 の後で実行中または以降のバージョンのオペレーティング システムでは、カーネル モード ドライバー フレームワーク (KMDF) とユーザー モード ドライバー フレームワーク (UMDF) ドライバーが必要とする割り込みオブジェクトを作成できます[パッシブ レベルの処理](supporting-passive-level-interrupts.md). チップ (SoC) プラットフォームで、システムのドライバーを作成する場合を除き、ただし、ドライバーは、DIRQL 割り込みオブジェクトを使用する必要があります。

ドライバーを通常オブジェクトを作成します framework 割り込みでその[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)コールバック関数。 ドライバーからの割り込みのオブジェクトを作成できますもその[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)コールバック関数。

フレームワークは、ドライバーの[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)プラグ アンド プレイ (PnP) マネージャーがデバイスにベクトルの割り込みなどのシステム リソースを割り当てられる前に、コールバック関数。 後 PnP マネージャーでは、リソースを割り当てる、フレームワークには、割り込みのリソースがデバイスの割り込みのオブジェクトに格納します。 (ドライバーを[プラグ アンド プレイをサポートしない](using-kernel-mode-driver-framework-with-non-pnp-drivers.md)割り込みオブジェクトを使用することはできません)。

フレームワークの割り込みオブジェクトを作成するには、ドライバーを初期化する必要があります、 [ **WDF\_割り込み\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff552347)構造体に渡すと、 [ **WdfInterruptCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547345)メソッド。

UMDF には、割り込みの次の種類がサポートされています。

-   トリガーされたレベル (共有または排他)
-   Edge によってトリガーされる (排他のみ)
-   MSI (定義によって排他)

**注**  UMDF はサポートしていません*共有*edge によってトリガーされる割り込みです。

 

UMDF は、UMDF 2.15 バージョン以降、ハードウェア プッシュ ボタン、通常して GPIO ピンの場合は、バックアップを有効にするかハードウェア レジスタを使用して明示的に無効にすることはできませんのような単純なデバイスの割り込みをサポートしています。 このようなデバイスをサポートするには、UMDF ドライバーは、排他的 edge によってトリガーされる割り込みを使用する必要があります。

KMDF バージョン 1.15 以降、KMDF も割り込みをサポートして、このようなデバイスで説明されている回避策なし[処理 Active-Both 割り込み](handling-active-both-interrupts.md)します。

また、 [ **WDF\_INTERRUPT\_CONFIG**](https://msdn.microsoft.com/library/windows/hardware/ff552347)には、ドライバーは、次のドライバーが指定したイベントのコールバック関数へのポインターを提供します。

<a href="" id="---------evtinterruptenable--------"></a>[*EvtInterruptEnable*](https://msdn.microsoft.com/library/windows/hardware/ff541730)  
ハードウェアの割り込みを有効にします。

<a href="" id="---------evtinterruptdisable--------"></a>[*EvtInterruptDisable*](https://msdn.microsoft.com/library/windows/hardware/ff541714)  
ハードウェアの割り込みを無効にします。

<a href="" id="---------evtinterruptisr--------"></a>[*EvtInterruptIsr*](https://msdn.microsoft.com/library/windows/hardware/ff541735)  
割り込みサービス ルーチン (ISR) を中断します。

<a href="" id="---------evtinterruptdpc--------"></a>[*EvtInterruptDpc*](https://msdn.microsoft.com/library/windows/hardware/ff541721)  
割り込みの遅延プロシージャ呼び出し (DPC)。

<a href="" id="evtinterruptworkitem"></a>[*EvtInterruptWorkItem*](https://msdn.microsoft.com/library/windows/hardware/hh406422)  
作業項目、[パッシブ レベル割り込み](supporting-passive-level-interrupts.md)します。

ドライバーはフレームワークのバージョン 1.11 または後で Windows 8 またはそれ以降のバージョンのオペレーティング システムを使用して、ドライバーは (DIRQL またはパッシブ) は、framework 割り込みのオブジェクトの親を framework デバイス オブジェクトか、フレームワークのキュー オブジェクトを明示的に設定できます。 ドライバーを設定する必要があります、ドライバーは、親を指定する場合、 **AutomaticSerialization**割り込みオブジェクトのメンバー [ **WDF\_割り込み\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff552347)構造体を TRUE にします。 (場合にそのことを思い出してください**AutomaticSerialization**が true の場合、フレームワークは、割り込みオブジェクトの実行を同期[ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)または[ *EvtInterruptWorkItem* ](https://msdn.microsoft.com/library/windows/hardware/hh406422)割り込みの親オブジェクトの下にあるその他のオブジェクトからのコールバック関数でコールバック関数です)。

たとえば、ドライバーは、割り込みのキューのコールバックと同期する、割り込みの親としてキューを指定可能性があります[ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)または[ *EvtInterruptWorkItem* ](https://msdn.microsoft.com/library/windows/hardware/hh406422)コールバック。 この構成では、フレームワークは、デバイス オブジェクトを削除するときに、キュー オブジェクトを削除します。

呼び出した後[ **WdfInterruptCreate**](https://msdn.microsoft.com/library/windows/hardware/ff547345)、ドライバーは呼び出すことができます必要に応じて[ **WdfInterruptSetPolicy** ](https://msdn.microsoft.com/library/windows/hardware/ff547387)または[ **WdfInterruptSetExtendedPolicy** ](https://msdn.microsoft.com/library/windows/hardware/ff547381)割り込みの追加パラメーターを指定します。 通常、ドライバーがからこれらのメソッドを呼び出してその[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)コールバック関数。

フレームワークには、割り込みの親を削除する前に割り込みが自動的に削除されます。 ドライバーを呼び出すことができます必要に応じて、 [ **WdfObjectDelete** ](https://msdn.microsoft.com/library/windows/hardware/ff548734)を以前の時点で割り込みを削除します。

## <a name="supporting-message-signaled-interrupts"></a>メッセージ シグナル割り込みをサポートしています。


メッセージ シグナル割り込み (Msi) は、以降 Windows Vista でサポートされます。 デバイスの Msi をサポートするために、オペレーティング システムを有効にするには、ドライバーの INF ファイルは、レジストリのいくつかの値を設定する必要があります。 これらの値を設定する方法については、[Enabling Message-Signaled がレジストリへの割り込み](https://msdn.microsoft.com/library/windows/hardware/ff544246)を参照してください。

ドライバーは、割り込みベクトルまたはデバイスをサポートできる MSI メッセージごとに framework 割り込みオブジェクトを作成する必要があります。 PnP マネージャーでは付与されません、デバイスのすべてのデバイスをサポートする割り込みリソース、余分な割り込みオブジェクトは使用されませんし、これらのコールバック関数は呼び出されません。

Windows 7 では、オペレーティング システムではデバイス関数あたり以上 910 割り込みメッセージ リソース要求をできません。 Windows 8 のオペレーティング システムではデバイス関数あたり 2,048 個以下の割り込みのリソース要求をできません。

デバイス ドライバーは、この制限を超えている場合、デバイスが起動に失敗します。 多くの論理プロセッサを含むコンピューターで動作するに、ドライバーは 1 プロセッサあたり 1 つ以上の割り込みを要求する必要がありますされません。

ドライバーをする必要があります、しなくても許容エラー、再均衡化システム PnP マネージャーがデバイスに割り当てます割り込みリソースの任意の代替のセットは、リソース要件の一覧からリソースを中断します。 たとえば、デバイスの割り当ては、要求のドライバーよりもメッセージの割り込みの数を減らしてに可能性があります。 最悪の場合は、行ベースの割り込みを 1 つだけでデバイスの動作にドライバーを準備する必要があります。

 

 





