---
title: または、UMDF ドライバーが読み込みに失敗した原因を判断し、デバイスの起動に失敗
description: このトピックでは、UMDF ドライバーの読み込みに失敗または開始する、関連付けられているデバイスが失敗した場合に使用できるトラブルシューティングの手順について説明します。
ms.assetid: 366c0ab4-8d06-4dac-a301-f433cf7978bd
keywords:
- WDK UMDF のシナリオをデバッグするには、UMDF ドライバーの読み込みに失敗します。
- WDK UMDF のシナリオをデバッグするには、UMDF デバイスの起動に失敗します。
- UMDF デバッグ シナリオでは、WDK UMDF ドライバーの読み込みに失敗します。
- UMDF デバッグ シナリオでは、WDK UMDF デバイスの起動に失敗します。
- UMDF WDK、シナリオを読み込んでいないドライバー
- UMDF WDK、シナリオを開始していないデバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4725643bcd62dbf2d509d58e7131592ebaa75016
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377418"
---
# <a name="determining-why-the-umdf-driver-fails-to-load-or-the-umdf-device-fails-to-start"></a>UMDF ドライバーの読み込み失敗または UMDF デバイスの起動失敗の理由の特定


このトピックでは、UMDF ドライバーの読み込みに失敗または開始する、関連付けられているデバイスが失敗した場合に使用できるトラブルシューティングの手順について説明します。

両方の UMDF バージョン 1 と 2 ドライバーでは、次の手法を使用できます。

1.  次のファイルが正しいことを確認して、セットアップを確認します。
    -   ドライバーの INF ファイル。

        使用して、 [ChkINF](https://docs.microsoft.com/windows-hardware/drivers/devtest/chkinf)ドライバーの INF ファイルを検証するためのツール。

    -   %windir%\\inf\\setupapi.dev.log (Windows XP で setupapi.log)、%windir%\\setupact.log、および %windir%\\temp\\wudf\_update.log ファイル。

2.  セットアップの問題が見つからなかった場合に有効にする、 **HostProcessDbgBreakOnStart**レジストリ エントリを使用して、 [WDF Verifier コントロール アプリケーション](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdf-verifier-control-application)(WdfVerifier.exe)。 有効にすると**HostProcessDbgBreakOnStart**デバッガーを WUDFHost.exe 起動後すぐにデバイス (WUDFHost.exe) 区切りのためのドライバーのホスト プロセスが作成されますが、DLL の読み込みには、ドライバーの前にします。

    有効にする必要があります**HostProcessDbgBreakOnStart**ユーザー モード デバッガーとカーネル モードのデバッガーではありません。 カーネル モードのデバッガー、既定は、ユーザー モードのモジュールの読み込みが表示され、通知をアンロードするはありません。 そのため、遅延のブレークポイントを設定することはできません。

3.  開始ホストが表示されない場合は、デバイスを正しく構成するのには、次の手順を実行します。
    1.  すべてのドライバーの INF を使ってインストールが存在し、オペレーティング システムにコピーされることを確認します。
    2.  Reflector (WUDFRd.sys とも呼ばれます) がデバイス上のサービスでない場合、ドライバーは、サービスになりますし、サービス エントリ (たとえば、' sc qc' foo') があり、自動的に開始に設定されていることを確認します。

4.  ドライバーのシンボルがシンボル パス (つまり、.sympath) であることを確認します。

5.  一度に 1 つに、次の項目を確認します。 次の手順で、ドライバーが foo.dll であると仮定します。
    1.  いることを確認、ドライバーの**DllMain**ルーチンは (たとえば、bu Foo と呼ばれます!。DllMain)。
    2.  後続の手順については、ドライバ DLL が読み込ま場合使用することも、 **HostProcessDbgBreakOnDriverLoad**レジストリ エントリ。 ある**HostProcessDbgBreakOnDriverLoad**セットにより、ドライバー DLL が読み込まれた後、デバッガーを中断する WUDFHost.exe します。 **HostProcessDbgBreakOnDriverLoad**のため、この時点で、ドライバーの読み込みとプロセスを開始するデバイスでブレークポイントを設定できますでドライバー コードにも、カーネル モード デバッガーに使用できます。
    3.  この手順は、UMDF バージョン 1 のドライバーのみに適用されます。 いることを確認、ドライバーの**DllGetClassObject**ルーチンが呼び出されます。 ドライバーのクラス識別子 (ID) が正しいことを確認します。 いることを確認**DllGetClassObject**が正常に実行し、(たとえば、bu Foo ドライバー オブジェクトを返します!DllGetClassObject)。

    4.  Umdf バージョン 1 であることを確認、ドライバーの[ **IDriverEntry::OnDeviceAdd** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)メソッドが呼び出されます。 メソッドが、デバイスを作成し、正常に (たとえば bu Foo 返すことを確認します!CMyDriver::OnDeviceAdd)。

        Umdf バージョン 2 であることを確認、ドライバーの[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)関数が呼び出されます。 関数はデバイスを作成し、正常に (たとえば bu Foo を返しますを確認します。!MyDriverDeviceAdd)。

    5.  Umdf バージョン 1 であることを確認、ドライバーの[ **IPnpCallbackHardware::OnPrepareHardware** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware)または[ **IPnpCallback::OnD0Entry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallback-ond0entry)メソッドが呼び出されます。 正常に (たとえば bu Foo メソッドが返すことを確認!CMyDevice::OnPrepareHardware または Foo!CMyDevice::OnD0Entry)。

        Umdf バージョン 2 であることを確認、ドライバーの[ *EvtDevicePrepareHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)または[ *EvtDeviceD0Entry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)関数が呼び出されます。 正常に (たとえば bu Foo 関数によって返されることを確認!MyDevicePrepareHardware または Foo!MyDeviceD0Entry)。

    6.  以前の操作が正常に実行されましたが、次の操作が実行されない場合、次のものを確認する必要があります。
        1.  上と下、ドライバー、ユーザー モードのスタック内のすべてのドライバーが正常にもこれらの操作を実行することを確認します。
        2.  ドライバーの下に、カーネル スタックが正常に完了することを確認、 [ **IRP\_MJ\_PNP** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)と[ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device) Irp します。

 

 





