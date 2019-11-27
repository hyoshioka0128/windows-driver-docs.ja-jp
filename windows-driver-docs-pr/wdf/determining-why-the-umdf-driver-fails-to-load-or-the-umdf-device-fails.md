---
title: UMDF ドライバーの読み込みに失敗した理由、またはデバイスの起動に失敗した原因を特定する
description: このトピックでは、UMDF ドライバーの読み込みに失敗した場合、または関連付けられたデバイスを起動できない場合に使用できるトラブルシューティング手順について説明します。
ms.assetid: 366c0ab4-8d06-4dac-a301-f433cf7978bd
keywords:
- デバッグシナリオ WDK UMDF、UMDF ドライバーの読み込みが失敗する
- デバッグシナリオ WDK UMDF、UMDF デバイスを起動できない
- UMDF WDK、デバッグシナリオ、UMDF ドライバーの読み込みに失敗する
- UMDF WDK、デバッグシナリオ、UMDF デバイスを起動できない
- UMDF WDK、ドライバーを読み込まないシナリオ
- UMDF WDK、デバイスを開始しないシナリオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ef23e04d8451fc3b058b2cc6e2c228a75980a0b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833673"
---
# <a name="determining-why-the-umdf-driver-fails-to-load-or-the-umdf-device-fails-to-start"></a>UMDF ドライバーの読み込み失敗または UMDF デバイスの起動失敗の理由の特定


このトピックでは、UMDF ドライバーの読み込みに失敗した場合、または関連付けられたデバイスを起動できない場合に使用できるトラブルシューティング手順について説明します。

次の手法は、UMDF バージョン1と2ドライバーの両方で使用できます。

1.  次のファイルが正しいことを確認して、セットアップを確認します。
    -   ドライバーの INF ファイル。

        [ChkINF](https://docs.microsoft.com/windows-hardware/drivers/devtest/chkinf)ツールを使用して、ドライバーの INF ファイルを検証します。

    -   % windir%\\inf\\setupapi.log (Windows XP の場合)、% windir%\\setupact .log、および% windir%\\temp\\wudf\_更新 .log ファイルになります。

2.  セットアップの問題が見つからない場合は、 [WDF Verifier コントロールアプリケーション](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdf-verifier-control-application)(wdfverifier) を使用して**Hostprocessdbgbreakonstart**レジストリエントリを有効にします。 **Hostprocessdbgbreakonstart**を有効にすることにより、デバイス (wudfhost .exe) のドライバーホストプロセスは、wudfhost .exe が開始されてからドライバー DLL が読み込まれる前に、デバッガーに中断されるようになります。

    カーネルモードのデバッガーではなく、ユーザーモードのデバッガーで**Hostprocessdbgbreakonstart**を有効にする必要があります。 既定では、カーネルモードのデバッガーは、ユーザーモードモジュールの読み込みとアンロードの通知を受け取りません。 したがって、遅延ブレークポイントを設定することはできません。

3.  ホストの開始が表示されない場合は、次の手順を実行してデバイスを正しく構成します。
    1.  INF を通じてインストールするすべてのドライバーが存在し、オペレーティングシステムにコピーされていることを確認します。
    2.  リフレクター (WUDFRd. sys とも呼ばれます) がデバイス上のサービスでない場合は、ドライバーがサービスであること、およびサービスエントリ (例、"sc qc foo") を持ち、自動的に開始するように設定されていることを確認します。

4.  ドライバーのシンボルがシンボルパス (つまり、sympath) にあることを確認します。

5.  次の項目を一度に1つずつ確認します。 次の手順では、ドライバーが foo .dll であると仮定します。
    1.  ドライバーの**DllMain**ルーチンが呼び出されていることを確認します (たとえば、bu Foo!DllMain)。
    2.  ドライバー DLL が読み込まれる場合、以降の手順では、 **Hostprocessdbgbreakondriverload**レジストリエントリを使用することもできます。 **Hostprocessdbgbreakondriverload** set を使用すると、ドライバー DLL が読み込まれた後、WUDFHost .exe がデバッガーに中断されます。 **Hostprocessdbgbreakondriverload**は、カーネルモードのデバッガーでも使用できます。これは、ドライバーの読み込みおよびデバイスの開始プロセスの時点で、ドライバーコードにブレークポイントを設定できるためです。
    3.  この手順は、UMDF version 1 ドライバーのみに適用されます。 ドライバーの**DllGetClassObject**ルーチンが呼び出されていることを確認します。 ドライバーのクラス識別子 (ID) が正しいことを確認します。 **DllGetClassObject**が正常に実行され、ドライバーオブジェクトを返すことを確認します (例、bu Foo!DllGetClassObject)。

    4.  UMDF version 1 の場合は、ドライバーの[**Idriverentry:: OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)メソッドが呼び出されていることを確認します。 メソッドによってデバイスが作成され、正常に返されたことを確認します (たとえば、bu Foo!CMyDriver:: OnDeviceAdd)。

        UMDF version 2 の場合は、ドライバーの[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)関数が呼び出されていることを確認します。 関数がデバイスを作成し、正常に返されたことを確認します (たとえば、bu Foo!MyDriverDeviceAdd)。

    5.  UMDF バージョン1の場合は、ドライバーの[**IPnpCallbackHardware:: OnIPnpCallback hardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware)または[ **:: OnD0Entry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0entry)メソッドが呼び出されていることを確認します。 メソッドが正常に返されたことを確認します (例、bu Foo!CMyDevice:: On Hardware または Foo!CMyDevice::OnD0Entry).

        UMDF version 2 の場合は、ドライバーの[*EvtdeviceEvtDeviceD0Entry ハードウェア*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)または[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)関数が呼び出されていることを確認します。 関数が正常に返されたことを確認します (例、bu Foo!Mydevice(ハードウェアまたは Foo)MyDeviceD0Entry).

    6.  前の各操作が正常に実行されても、次の操作が実行されない場合は、次の項目を確認する必要があります。
        1.  ユーザーモードスタック内のドライバーよりも前のすべてのドライバーが、これらの操作を正常に実行できることを確認します。
        2.  ドライバーの下にあるカーネルスタックが正常に[**irp\_MJ\_PNP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)と[**irp\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)完了したことを確認します。これにより、デバイスの irp が\_開始されます。

 

 





