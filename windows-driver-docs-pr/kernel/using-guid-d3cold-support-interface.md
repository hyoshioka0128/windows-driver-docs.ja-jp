---
title: GUID_D3COLD_SUPPORT_INTERFACE Driver インターフェイスの使用
description: Windows 8 以降では、ドライバーは GUID_D3COLD_SUPPORT_INTERFACE インターフェイスのルーチンを呼び出して、デバイスの D3cold 機能を判別し、これらのデバイスで D3cold を使用できるようにします。
ms.assetid: 525637E8-B16F-4038-A78D-A47064E36449
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: db4fc5ed00d76e24f0a8865c13aff373569144ad
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838355"
---
# <a name="using-the-guid_d3cold_support_interface-driver-interface"></a>GUID\_D3COLD\_サポート\_インターフェイスドライバーインターフェイス


Windows 8 以降では、ドライバーは、GUID\_D3COLD\_サポート\_インターフェイスインターフェイスのルーチンを呼び出して、デバイスの D3cold 機能を特定し、これらのデバイスで D3cold を使用できるようにします。 このインターフェイスの2つの主なルーチンは、 [*SetD3ColdSupport*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-set_d3cold_support)と[*GetIdleWakeInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-get_idle_wake_info)です。


GUID_D3COLD_SUPPORT_INTERFACE driver インターフェイスでは、D3 デバイスの電源状態の D3cold 下位部分がサポートされています。 D3 は、D3hot と D3cold の2つに分かれています。 D3 は、デバイスの電源状態が最も低いデバイスであり、D3cold は D3hot よりも消費電力が少なくなっています。 デバイス、親バスドライバー、およびプラットフォームファームウェアがこの状態をサポートしている場合にのみ、デバイスは D3cold に入ることができます。 D3cold をサポートするデバイスは、コンピューターが S0 (動作) システムの電源状態にあるときに、この状態に入ることができます。

デバイスの電源ポリシー所有者 (PPO) であるドライバーは、このインターフェイスのルーチンを呼び出して、次の操作を実行します。

-    デバイス、親バスドライバー、およびプラットフォームファームウェアのサポートが D3cold 下位変換に対応しているかどうかを検出します。 
-    デバイスが D3cold の下位にあるときに、デバイスがプロセッサにウェイクアップイベントを通知できるかどうかを検出します。 
-    デバイスによる D3cold の下位変換への切り替え効果を有効または無効にします。 

このインターフェイスを照会するために、デバイスドライバーは IRP_MN_QUERY_INTERFACE IRP をドライバースタックに送信します。 この IRP の場合、ドライバーは InterfaceType 入力パラメーターを GUID_D3COLD_SUPPORT_INTERFACE に設定します。 IRP が正常に完了すると、インターフェイスの出力パラメーターは D3COLD_SUPPORT_INTERFACE 構造体へのポインターになります。 この構造体には、インターフェイス内のルーチンへのポインターが含まれています。

D3cold デバイスの電源状態の詳細については、「[ドライバーでの D3cold のサポート](supporting-d3cold-in-a-driver.md)」を参照してください。


ドライバーは、 *SetD3ColdSupport*ルーチンを呼び出して、コンピューターが S0 にあるときに発生する可能性がある D3cold へのデバイスの移行を動的に有効または無効にします。 デバイスが、デバイスが入力する低電力の Dx 状態からウェイクアップイベントを通知できる必要がある場合、ドライバーは、デバイスが D3cold から D3cold に信号を送ることができる場合にのみ、デバイスがデバイスを自動的に入力できるようにする必要があります。 そうしないと、デバイスが D3cold に入った後、コンピューターが S0 状態から出るまで使用できなくなる可能性があります。

既定では、 *SetD3ColdSupport*ルーチンへの最初の呼び出しの前に、D3hot 遷移は無効になっています。 最初の*SetD3ColdSupport*呼び出しの前に D3hot 遷移が有効になるようにこの既定値を変更するには、ドライバーをインストールする INF ファイルの ddinstall. HW セクションに、デバイスのドライバーパッケージに次の2行を含めることができます。

```Text
Include = machine.inf
Needs = PciD3ColdSupported
```

*GetIdleWakeInfo*ルーチンを使用すると、デバイスのドライバーは、コンピューターが特定のシステム電源状態にあるときに、デバイスがスリープ解除イベントを通知できるデバイスの電源状態を検出できます。 このルーチンへの呼び出し元は、システムの電源状態を入力パラメーターとして指定し、出力パラメーターとして、コンピューターが指定されたシステムの電源状態にあるときに、デバイスが待機イベントを通知できる最も電力の低いデバイスの電源状態を報告します. たとえば、 *GetIdleWakeInfo*ルーチンは、コンピューターが S0 にあるときに、デバイスが D3cold からウェイクイベントに信号を送ることができるかどうかをドライバーに指示できます。

*GetIdleWakeInfo*ルーチンは、 [**IRP\_\_QUERY\_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)要求から取得したものよりも詳細なデバイスウェイクアップ情報を提供します。 この要求は、すべてのバージョンの Windows でサポートされており、デバイスの機能を説明する[**デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)の構造を提供します。 この構造体の**Devicewake**メンバーには、 *GetIdleWakeInfo*ルーチンから入手できる情報のサブセットが含まれています。 このメンバーは、デバイスが待機イベントに信号を送ることができるデバイスの電源の最低状態を示します。 このメンバーの情報は、コンピューターが、構造体の**Systemwake**メンバーによって示されるシステムの低電力状態にある場合にのみ、正確であることが保証されます。 **Systemwake** = **PowerSystemSleeping3**の場合、 **Devicewake**内の情報は S3 に対して有効であることがわかっています。 S1 および S2 では多くの場合有効であり、S0 に対して有効である場合もあります。

ただし、ベストプラクティスとして、ドライバーでは、 **devicewake**メソッドの情報が**systemwake**によって示される状態以外のシステム電源の状態に対して有効であると想定しないでください。 一部のデバイスでは、デバイスがウェイクアップイベントを通知できる最小の Dx 状態は、コンピューターが動作状態 S0 であるか、低電力状態 (S1、S2、S3、または S4) であるかによって異なります。 その他のデバイスの場合、デバイスが接続されているバスは、コンピューターが S0 にあるときに wake シグナルを処理できますが、デバイスは使用できません。 これらのデバイスのデバイスのウェイクアップ機能を正確に記述できるのは、 *GetIdleWakeInfo*ルーチンだけです。

たとえば、 [Pci Express Base 3.0 仕様](https://pcisig.com/specifications/pciexpress/specifications/)では、ウェイクアップイベントを通知するための2つの独立したメカニズムが定義されています。 pci express link (bus) が有効になっている場合、もう1つのメカニズムが使用され、リンクがオフになっているときに使用されます。 リンクが有効になっている場合、デバイスは PM\_PME トランザクション層パケット (TLPs) のストリームを送信し、デバイスが低電力の Dx 状態から D0 に移動する必要があることを通知します。 リンクがオフになっている場合、デバイスは、デバイスが PM\_PME TLPs を送信できるように、リンクを有効にするように要求します。 リンクを有効にするように要求するために、デバイスは、(より一般的なデバイスフォームファクターの) WAKE\# シグナルをアサートするか、"ビーコン" メカニズムを使用します (あまり一般的ではありません)。

PCI Express 仕様では、D3cold から電源管理イベント (PMEs) を通知する機能を提供するすべてのデバイスが、これらのデバイスウェイクアップメカニズムの両方を実装する必要がありますが、ドライバー開発者は、正しくないデバイスを有効にする必要がある場合があります。これらのメカニズムを実装します。

リンクが有効になっているときにデバイスが PM\_を正しく配信できる場合は、コンピューターが S0 にあるときに、ドライバーによってデバイスが D3hot に入ることができます。 デバイスが WAKE\# 信号を正しくアサートしてリンクをオンにした後、PM\_PME TLPs を使用して D0 への移行を開始できる場合、ドライバーは、コンピューターが S0 にあるときにデバイスが D3cold に入ることを可能にすることができます。

ただし、システムファームウェア (BIOS) が PCI Express device wake メカニズムがハードウェアプラットフォームによって正しく処理されることを保証できない場合、ドライバーは、デバイスが D3hot または D3cold のいずれかを入力できるようにする必要があります。 ドライバーは、 [*GetIdleWakeInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-get_idle_wake_info)ルーチンを呼び出して、ファームウェアがこれらのメカニズムをサポートしているかどうかを検出できます。 ドライバーでカーネルモードドライバーフレームワーク (KMDF) 1.11 以降が使用されている場合は、 *GetIdleWakeInfo*を呼び出すのに便利な方法として、 [**WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)メソッドによって、デバイスのアイドル状態が最も低いデバイスをアイドル状態にすることができます。デバイスがウェイクイベントを通知できる。

 

 




