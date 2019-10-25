---
title: 割り込みオブジェクトの作成
description: 割り込みオブジェクトの作成
ms.assetid: 8bea7498-9fee-4d84-9e6b-976102c54876
keywords:
- ハードウェア割り込み WDK KMDF、オブジェクトの作成
- WDK KMDF の割り込み、オブジェクトの作成
- メッセージシグナル割り込み (WDK KMDF)
- Msi WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97cb9d129163ad65963123d1b084ef356661851a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845611"
---
# <a name="creating-an-interrupt-object"></a>割り込みオブジェクトの作成


デバイスのハードウェア割り込みを処理する Windows Driver Framework (WDF) ドライバーは、各デバイスがサポートできる各割り込みのフレームワーク割り込みオブジェクトを作成する必要があります。 Windows 8 以降のバージョンのオペレーティングシステムで実行されている framework バージョン1.11 以降では、カーネルモードドライバーフレームワーク (KMDF) およびユーザーモードドライバーフレームワーク (UMDF) ドライバーは、[パッシブレベルの処理](supporting-passive-level-interrupts.md)を必要とする割り込みオブジェクトを作成できます。 ただし、チップ (SoC) プラットフォーム上のシステムのドライバーを記述する場合を除き、ドライバーは DIRQL 割り込みオブジェクトを使用する必要があります。

通常、ドライバーは、 [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数にフレームワークの割り込みオブジェクトを作成します。 ドライバーは、 [*Evtdevicepreparehardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック関数から割り込みオブジェクトを作成することもできます。

フレームワークは、ドライバーの[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数を呼び出してから、割り込みベクターなどのシステムリソースがプラグアンドプレイ (PnP) マネージャーによってデバイスに割り当てられるようにします。 PnP マネージャーによってリソースが割り当てられると、そのデバイスの interrupt オブジェクトに割り込みリソースが格納されます。 (プラグアンドプレイを[サポートしていない](using-kernel-mode-driver-framework-with-non-pnp-drivers.md)ドライバーは、interrupt オブジェクトを使用できません)。

フレームワークの割り込みオブジェクトを作成するには、ドライバーが[**WDF\_interrupt\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config)構造体を初期化し、それを[**WdfInterruptCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate)メソッドに渡す必要があります。

UMDF では、次の種類の割り込みがサポートされています。

-   レベルトリガー (共有または排他)
-   エッジトリガー (排他のみ)
-   MSI (定義による排他)

**注**  UMDF は、エッジによってトリガーされる*共有*の割り込みをサポートしていません。

 

Umdf バージョン2.15 以降では、UMDF は、ハードウェアプッシュボタンなどの単純なデバイス (通常は GPIO ピンによってサポートされる) などの単純なデバイスの割り込みをサポートしています。ハードウェアレジスタを明示的に使用することはできません。 このようなデバイスをサポートするために、UMDF ドライバーは、エッジによってトリガーされる排他的な割り込みを使用する必要があります。

Kmdf バージョン1.15 以降では、KMDF は、このようなデバイスの割り込みもサポートしています。「[アクティブな両方の割り込みの処理](handling-active-both-interrupts.md)」で説明されている回避策はありません。

また、 [**WDF\_INTERRUPT\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config)では、ドライバーによって提供される次のイベントコールバック関数へのポインターが提供されます。

<a href="" id="---------evtinterruptenable--------"></a>[*EvtInterruptEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable)  
ハードウェアの割り込みを有効にします。

<a href="" id="---------evtinterruptdisable--------"></a>[*EvtInterruptDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)  
ハードウェアの割り込みを無効にします。

<a href="" id="---------evtinterruptisr--------"></a>[*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)  
割り込みの中断サービスルーチン (ISR)。

<a href="" id="---------evtinterruptdpc--------"></a>[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)  
割り込みの遅延プロシージャ呼び出し (DPC)。

<a href="" id="evtinterruptworkitem"></a>[*EvtInterruptWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)  
[パッシブレベルの割り込み](supporting-passive-level-interrupts.md)の作業項目。

Windows 8 以降のバージョンのオペレーティングシステムで、framework バージョン1.11 以降を使用しているドライバーの場合、ドライバーはフレームワークの割り込みオブジェクト (DIRQL またはパッシブ) の親をフレームワークのデバイスオブジェクトまたはフレームワークキューオブジェクトに明示的に設定できます。 ドライバーで親が指定されている場合、ドライバーは、割り込みオブジェクトの[**WDF\_interrupt\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config)構造体の自動**シリアル化**メンバーを TRUE に設定する必要があります。 (自動**シリアル化**が TRUE の場合、フレームワークは、割り込みオブジェクトの[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)または[*EvtInterruptWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem) callback 関数の実行を、その他のオブジェクトからのコールバック関数と同期します。割り込みの親オブジェクトの下にあります)。

たとえば、ドライバーは、キューのコールバックを割り込みの[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)または[*EvtInterruptWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)コールバックと同期するために、割り込みの親としてキューを指定する場合があります。 この構成では、デバイスオブジェクトを削除するときに、フレームワークによってキューオブジェクトが削除されます。

[**WdfInterruptCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate)を呼び出した後、ドライバーは必要に応じて[**WdfInterruptSetPolicy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptsetpolicy)または[**WdfInterruptSetExtendedPolicy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptsetextendedpolicy)を呼び出して、追加の割り込みパラメーターを指定できます。 通常、ドライバーは、 [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数からこれらのメソッドを呼び出します。

割り込みの親を削除する前に、フレームワークによって割り込みが自動的に削除されます。 必要に応じて、ドライバーは[**Wdfobjectdelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)を呼び出して、以前の時刻に割り込みを削除できます。

## <a name="supporting-message-signaled-interrupts"></a>メッセージシグナル割り込みのサポート


Windows Vista 以降では、メッセージシグナル割り込み (Msi) がサポートされています。 オペレーティングシステムがデバイスの Msi をサポートできるようにするには、ドライバーの INF ファイルでレジストリに値を設定する必要があります。 これらの値を設定する方法については、「[レジストリでのメッセージシグナル割り込みの有効化](https://docs.microsoft.com/windows-hardware/drivers/kernel/enabling-message-signaled-interrupts-in-the-registry)」を参照してください。

ドライバーは、デバイスがサポートできる各割り込みベクターまたは MSI メッセージに対して、フレームワークの interrupt オブジェクトを作成する必要があります。 デバイスがサポートできるすべての割り込みリソースがデバイスに付与されていない場合、余分な割り込みオブジェクトは使用されず、そのコールバック関数は呼び出されません。

Windows 7 では、オペレーティングシステムは、デバイスごとの割り込みメッセージ数が910を超えるリソース要求をサポートしていません。 Windows 8 では、オペレーティングシステムは、デバイスごとの割り込みが2048を超えるリソース要求をサポートしていません。

デバイスドライバーがこの制限を超えると、デバイスの起動に失敗する可能性があります。 多数の論理プロセッサが含まれているコンピューターで操作するには、ドライバーがプロセッサごとに複数の割り込みを要求しないようにする必要があります。

ドライバーは、障害を発生させることなく、割り込みリソースのシステム再調整を許容する必要があります。これにより、PnP マネージャーは、リソース要件の一覧から別の割り込みリソースのセットをデバイスに割り当てます。 たとえば、デバイスには、要求されたドライバーよりも少ない数のメッセージ割り込みが割り当てられる場合があります。 最悪の場合、ドライバーは、1行ベースの割り込みだけでデバイスを操作できるように準備する必要があります。

 

 





