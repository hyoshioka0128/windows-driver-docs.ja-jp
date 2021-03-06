---
title: GUID_D3COLD_SUPPORT_INTERFACE ドライバー インターフェイスの使用
description: Windows 8 以降、ドライバーは D3cold を使用して、これらのデバイスを有効にしてデバイスの D3cold 機能を決定する GUID_D3COLD_SUPPORT_INTERFACE インターフェイスで、ルーチンを呼び出すことができます。
ms.assetid: 525637E8-B16F-4038-A78D-A47064E36449
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a83f6b21e1159c198314a88beacb94b360ee378f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381654"
---
# <a name="using-the-guidd3coldsupportinterface-driver-interface"></a>GUID を使用して\_D3COLD\_サポート\_ドライバー インターフェイス


Windows 8 以降、ドライバーで呼び出すことが、ルーチン、GUID\_D3COLD\_サポート\_インターフェイス D3cold を使用して、これらのデバイスを有効にしてデバイスの D3cold 機能を判断します。 このインターフェイスで 2 つの主なルーチンは[ *SetD3ColdSupport* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-set_d3cold_support)と[ *GetIdleWakeInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-get_idle_wake_info)します。


GUID_D3COLD_SUPPORT_INTERFACE ドライバー インターフェイスは、D3 デバイスの電源状態の D3cold 下位状態のサポートを提供します。 D3 は D3hot と D3cold の 2 つの下位に分割されます。 D3 が最も低い搭載デバイスの電源の状態と D3cold D3hot に比べて、電力消費を使用します。 デバイスは、デバイス、親のバス ドライバー、およびプラットフォームのファームウェアは、この状態をサポートする場合にのみ、D3cold を入力できます。 D3cold をサポートするデバイスを入力して、コンピューターが、S0 の場合、この状態を終了 (操作) のシステム電源の状態。

デバイスの電源ポリシー所有者 (PPO) である、ドライバーは、このインターフェイスには、次のルーチンを呼び出します。

-    デバイスでは、親バス ドライバー、およびプラットフォームのファームウェアが D3cold 下位状態に遷移をサポートするかどうかを検出します。 
-    デバイスが、デバイスが下位 D3cold 状態プロセッサにウェイク イベントを通知できるかどうかを検出します。 
-    有効にして、デバイスによって D3cold 下位状態に遷移を無効にします。 

このインターフェイスを照会するには、デバイス ドライバーはドライバー スタック ダウン IRP_MN_QUERY_INTERFACE IRP を送信します。 この IRP では、ドライバーは GUID_D3COLD_SUPPORT_INTERFACE に InterfaceType 入力パラメーターを設定します。 IRP の正常終了時に、インターフェイスの出力パラメーターは、D3COLD_SUPPORT_INTERFACE 構造体へのポインターです。 この構造体には、インターフェイスのルーチンへのポインターが含まれています。

D3cold デバイスの電源状態の詳細については、次を参照してください。[ドライバーではサポートしている D3cold](supporting-d3cold-in-a-driver.md)します。


ドライバーを呼び出し、 *SetD3ColdSupport*ルーチンを動的に有効にして、S0 がコンピューターの場合に発生する可能性が D3cold にデバイスの移行を無効にします。 デバイスは、デバイスが入力する低電力 Dx 状態からスリープ解除イベントを通知できる必要があります、ドライバーは、デバイスが D3cold からウェイク イベントを通知できます D3cold のみを入力するのには、デバイスを有効にする必要があります。 それ以外の場合、D3cold を入力すると、デバイスが利用できないコンピューター S0 状態のままになるまで。

既定では、最初の呼び出しの前に、 *SetD3ColdSupport*ルーチン、D3hot-D3cold に遷移が無効になります。 D3hot-D3cold に遷移が 1 つ目の前に有効にするために、この既定を変更する*SetD3ColdSupport*呼び出すには、次を含めることができます、デバイスのドライバー パッケージ ファイルを INF の DDInstall.HW セクションの 2 つの行ドライバーがインストールされます。

```Text
Include = machine.inf
Needs = PciD3ColdSupported
```

*GetIdleWakeInfo*ルーチンは、デバイスが、コンピューターが特定のシステム電源の状態の場合、ウェイク イベントを通知デバイスの電源状態を検出するデバイスのドライバーを使用します。 このルーチンを呼び出し元は、入力パラメーターとしてシステム電源の状態を指定して、ルーチンが、デバイスが、コンピューターが、指定したシステムの電源状態の場合は、待機イベントを通知できます最小電力デバイス電源状態を報告する出力パラメーターとして. たとえば、 *GetIdleWakeInfo*ルーチンは、ドライバーを確認するかどうか、デバイス通知できますウェイク イベント D3cold から S0 がコンピューターの場合。

*GetIdleWakeInfo*ルーチン提供詳細デバイス ウェイクはから使用できるよりも、 [ **IRP\_MN\_クエリ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)要求。 この要求は、Windows のすべてのバージョンがサポートを提供する[**デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_capabilities)デバイスの機能を記述する構造体。 **DeviceWake**この構造体のメンバーにはから提供される情報のサブセットが含まれています、 *GetIdleWakeInfo*ルーチン。 このメンバーは、デバイスが待機イベントを通知できます最も低い搭載デバイスの電源状態を示します。 このメンバーの情報は、コンピューターで示されるシステム低電力状態にある場合にのみ正確であることが保証されます、 **SystemWake**構造体のメンバー。 場合**SystemWake** = **PowerSystemSleeping3**の情報は、 **DeviceWake**を有効にし、S3 の場合が頻繁に S1 と s2 の場合、有効な既知は、S0 に対して有効であるも可能性があります。

ただし、ベスト プラクティスとして、ドライバーを想定しないでくださいを内の情報、 **DeviceWake**メソッドは、システム電源の状態で示される状態以外の有効な**SystemWake**します。 一部のデバイスでは、デバイスが、ウェイク イベントを信号最低 Dx 状態に従って、コンピューターは、作業状態 S0 または (S1、S2、S3 または S4) は、低電力状態にするかどうかは異なります。 それ以外のデバイス、デバイスが接続されているバスは、コンピューターは、S0 ができない、デバイスとウェイク信号を処理できます。 のみ、 *GetIdleWakeInfo*ルーチンは、これらのデバイスのデバイスのウェイク アップ機能を正確に記述できます。

たとえば、 [PCI Express ベース 3.0 仕様](https://pcisig.com/specifications/pciexpress/specifications/)ウェイク イベントを通知する 2 つの異なるメカニズムを定義します-PCI Express リンク (バス) は有効になり、リンクが入っていないときに、その他の使用時に 1 つのメカニズムを使用します。 デバイスが PM のストリームを送信するリンクをオンにすると\_PME トランザクション レイヤー パケット (TLPs) デバイスは、D0 を低電力状態に Dx から移動することを通知します。 デバイスでは、デバイスは、PM を送信できるように、リンクが有効である要求のリンクが入っていないときに\_PME TLPs します。 リンクが入っていることを要求するデバイスか、アサートのウェイク アップ\#(より一般的なデバイス フォーム ファクター) のシグナルまたは (あまり一般的)、「ビーコン」メカニズムを使用します。

PCI Express 仕様は、ドライバー開発者は、デバイスが正しくない、有効にする必要がありますが D3cold からイベントを通知する電源管理 (PMEs) 機能を提供するすべてのデバイスでは、これらのデバイスにスリープを解除メカニズムの両方を実装が必要です。これらのメカニズムを実装します。

場合は、デバイスが PM を正しく配信\_PME TLPs のリンクをオンにすると、ドライバーは、コンピューターが S0 D3hot を入力するデバイスを有効にします。 デバイスでは、ウェイク アップをアサートできます正しく場合\#をリンクをオンにし、PM を使用して通知\_PME TLPs D0、ドライバーへの移行を開始するには、コンピューターが S0 D3cold を入力するデバイスが有効にすることができます。

ただし、ドライバーは、PCI Express デバイス ウェイク メカニズムが正しくハードウェア プラットフォームによって処理されているシステム ファームウェア (BIOS) が保証できない場合に、D3hot または D3cold のいずれかを入力するデバイスを有効にする必要があります。 ドライバーを呼び出すことができます、 [ *GetIdleWakeInfo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-get_idle_wake_info)ルーチンをファームウェアがこれらのメカニズムのサポートを要求するかどうかを検出します。 ドライバーはカーネル モード ドライバー フレームワーク (KMDF) 1.11 以降呼び出しに代わる便利な方法を使用している場合*GetIdleWakeInfo*を許可するのには、 [ **WdfDeviceAssignS0IdleSettings** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)メソッドを利用した最も低い Dx でアイドル状態にデバイスを有効にする状態、デバイスが、ウェイク イベントを通知できます。

 

 




