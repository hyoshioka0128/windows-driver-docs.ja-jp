---
Description: このトピックでは、クライアントドライバーが特定のエラーケースをテストできるようにする、USB 3.0 ドライバースタックの USB クライアントドライバーの検証機能について説明します。
title: USB クライアント ドライバー検証ツール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73d146a00d277b466b82117f6a3896687d399303
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837547"
---
# <a name="usb-client-driver-verifier"></a>USB クライアント ドライバー検証ツール


このトピックでは、クライアントドライバーが特定のエラーケースをテストできるようにする、USB 3.0 ドライバースタックの USB クライアントドライバーの検証機能について説明します。

-   [USB クライアントドライバーの検証ツールとは](#what-is-the-usb-client-driver-verifier)
-   [USB クライアントドライバーの検証ツールを有効にする方法](#how-to-enable-the-usb-client-driver-verifier)
-   [USB クライアントドライバーの検証ツールの構成設定](#configuration-settings-for-the-usb-client-driver-verifier)

## <a name="what-is-the-usb-client-driver-verifier"></a>USB クライアントドライバーの検証ツールとは


*Usb クライアントドライバーの検証ツール*は、Windows 8 に含まれる usb 3.0 ドライバースタックの機能です。 検証ツールが有効になっていると、USB ドライバースタックが失敗するか、クライアントドライバーによって実行される特定の操作が変更されます。 これらのエラーは、検出が困難なエラー条件をシミュレートし、後で望ましくない結果を招く可能性があります。 シミュレートされたエラーにより、ドライバーがエラーを適切に処理できるようになります。 クライアントは、エラー処理コードを使用してエラーを処理したり、別のコードパスを実行したりすることができます。

たとえば、クライアントドライバーは、一括エンドポイントの静的ストリームによる i/o 操作をサポートします。 検証ツールを使用すると、さまざまなホストコントローラーでサポートされているストリームの数に関係なく、ドライバーのストリームロジックが動作することを確認できます。 このシナリオをシミュレートするには、 **UsbVerifierStaticStreamCountOverride**設定を使用します (後で説明します)。 ドライバーが[**USBD\_QueryUsbCapability**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))を呼び出して、ホストコントローラーがサポートする静的ストリームの最大数を判断するたびに、ルーチンは異なる値を返します。

**重要**  USB クライアントドライバーの検証ツールは、さまざまな xHCI コントローラーに対してドライバーをテストするだけです。 この例では、チェーン化された MDL サポートがないなど、2.0 コントローラーの固有の動作の一部をシミュレートしています。 ただし、USB 2.0 コントローラーでクライアントドライバーをテストする必要があります。また、このツールを同じように交換することはできません。

 

Windows ハードウェア認定キットには、シミュレートされたテストケースを実行する自動テストが含まれています。 詳細については、「 [USB (USBDEX) 検証](https://docs.microsoft.com/previous-versions/windows/hardware/hck/hh998558(v=vs.85))機能のテスト」を参照してください。

## <a name="how-to-enable-the-usb-client-driver-verifier"></a>USB クライアントドライバーの検証ツールを有効にする方法


USB クライアントドライバーの検証ツールを使用するには、Windows 8 を実行しているターゲットコンピューターで有効にします。 ターゲットコンピューターには、USB デバイスが接続されている xHCI コントローラーが必要です。

クライアントドライバーの[ドライバー検証](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)ツールを有効にすると、USB クライアントドライバーの検証ツールが自動的に有効になります。 または、このレジストリエントリを設定して、検証を有効にすることもできます。

**注**  [Windows DRIVER Foundation (WDF) の検証コントロールアプリケーション (wdfverifier)](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdf-verifier-control-application)を有効にしても、USB クライアントドライバーの検証ツールは自動的に有効になりません。

 

```cpp
HKEY_LOCAL_MACHINE
   SYSTEM
      CurrentControlSet
         services
            <Client Driver>
               Parameters
                  UsbVerifierEnabled (DWORD)
```

**UsbVerifierEnabled**レジストリエントリには、DWORD 値を指定します。 **UsbVerifierEnabled**が1の場合、USB クライアントドライバーの検証ツールが有効になります。0を無効にします。 ドライバーの[検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)がクライアントドライバーに対して有効になっていて、 **UsbVerifierEnabled**が0の場合、USB クライアントドライバーの検証ツールは無効になります。

## <a name="configuration-settings-for-the-usb-client-driver-verifier"></a>USB クライアントドライバーの検証ツールの構成設定


検証ツールが有効になっている場合、USB ドライバースタックは、 **USBD\_Xxx UrURBs 検索**ルーチン (「 [USB ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#client)」を参照) を呼び出すことによって、クライアントドライバーが割り当てたを追跡します。 クライアントドライバーが URB をリークした場合、USB ドライバースタックはその情報を使用して、[ドライバーの検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)でバグチェックを行います。 その場合は、 **! usbanalyze-v**コマンドを使用して、リークの原因を特定します。

また、必要に応じて、USB クライアントドライバーの検証ツールを構成して、特定のルーチンを変更または失敗させたり、ルーチンが失敗する頻度を指定したりすることもできます。 検証ツールを構成するには、次のようにレジストリエントリを設定します。

```cpp
HKEY_LOCAL_MACHINE
   SYSTEM
      CurrentControlSet
         services
            <Client driver>
               Parameters
                  <USB client driver verifier setting> (DWORD)
```

*&lt;USB クライアント ドライバーの検証設定&gt;* レジストリ エントリは、DWORD 値を受け取ります。
設定を追加、変更、または削除する場合は、設定を適用するために、システムでデバイスを再列挙する必要があります。

次の表に、&lt;の*USB クライアントドライバーの検証ツールの設定&gt;* に使用できる値を示します。 設定は、**サービス**キーの下で指定されたクライアントドライバーに適用されます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>USB クライアントドライバーの検証の設定</th>
<th>次のいずれかの値を選択します。</th>
<th>シミュレートに使用...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>UsbVerifierFailRegistration</strong></p>
<p>クライアントドライバーによるこれらのルーチンの呼び出しに失敗します。</p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceCreateWithParameters&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)"><strong>WdfUsbTargetDeviceCreateWithParameters</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createhandle" data-raw-source="[&lt;strong&gt;USBD_CreateHandle&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createhandle)"><strong>USBD_CreateHandle</strong></a></li>
</ul></td>
<td><ul>
<li>0: 設定は無効になっています。</li>
<li>1: 呼び出しは常に失敗します。</li>
<li><em>N</em>: 呼び出しは 1/<em>N</em>の確率で失敗します。ここで、 <em>n</em>は 1 ~ 0x7ff の16進数の値です。 たとえば、 <em>N</em>が10の場合、 この呼び出しは、10回呼び出すたびに失敗します。</li>
</ul></td>
<td><p><strong>クライアントドライバーの登録に失敗した。</strong></p>
<p>クライアントドライバーの初期化タスクの1つは、基になるドライバースタックに自身を登録することです。 以降の複数の呼び出しでは、登録が必要です。</p>
<p>たとえば、クライアントドライバーは、登録のために<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createhandle" data-raw-source="[&lt;strong&gt;USBD_CreateHandle&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createhandle)"><strong>USBD_CreateHandle</strong></a>を呼び出します。 たとえば、ルーチンが常に STATUS_SUCCESS を返し、エラーを処理するコードを実装しないとします。 ルーチンがエラー NTSTATUS コードを返す場合、ドライバーは誤ってエラーを無視し、無効な USBD ハンドルを使用して後続の呼び出しに進むことができます。</p>
<p>この設定を使用すると、失敗コードパスをテストできるように、呼び出しを失敗させることができます。</p>
<p>登録が失敗したときにクライアントドライバーの動作が必要:</p>
<ul>
<li><p>ドライバーは想定されていませんが、通常どおりに機能します。</p></li>
<li><p>このエラーを無視するように選択することで、ドライバーがシステムのクラッシュを引き起こしたり応答しなくなったりすることはありません。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>UsbVerifierFailChainedMdlSupport</strong></p>
<p>呼び出し元が<em>CapabilityType</em>パラメーターに GUID_USB_CAPABILITY_CHAINED_MDLS を渡したときに、クライアントドライバーがこれらのルーチンを呼び出すことができません。</p>
<ul>
<li><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85)" data-raw-source="[&lt;strong&gt;USBD_QueryUsbCapability&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))"><strong>USBD_QueryUsbCapability</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceQueryUsbCapability&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability)"><strong>WdfUsbTargetDeviceQueryUsbCapability</strong></a></li>
</ul></td>
<td><ul>
<li>0: 設定は無効になっています。</li>
<li>1: 呼び出しは常に失敗します。</li>
<li><em>N</em>: 呼び出しは 1/<em>N</em>の確率で失敗します。ここで、 <em>n</em>は 1 ~ 0x7ff の16進数の値です。 たとえば、 <em>N</em>が10の場合、 この呼び出しは、10回呼び出すたびに失敗します。</li>
</ul></td>
<td><p><strong>チェーン MDLs をサポートしていないホストコントローラーとの通信。</strong></p>
<p>クライアントドライバーがチェーン MDLs ( <a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/using-mdls" data-raw-source="[MDL](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-mdls)">MDL</a>を参照) を送信するためには、USB ドライバースタックとホストコントローラーがそれらをサポートしている必要があります。</p>
<p>この設定を使用すると、クライアントドライバーがチェーンされている MDL 要求を、サポートされていないホストコントローラーに接続されているデバイスに送信したときに実行されるコードをテストできます。 ホストコントローラーがチェーン MDLs をサポートしているかどうかに関係なく、呼び出しは失敗します。</p>
<p>USB ドライバースタックでのチェーン MDLs のサポートの詳細については、「<a href="how-to-send-chained-mdls.md" data-raw-source="[How to Send Chained MDLs](how-to-send-chained-mdls.md)">チェーン MDLs の送信方法</a>」を参照してください。</p>
<p>ホストコントローラーでチェーン MDLs がサポートされていない場合は、クライアントドライバーの動作が必要です。</p>
<ul>
<li><p>ドライバーは、チェーン MDLs を使用せずに、引き続き i/o 転送を実行します。 また、このようなコントローラーでは、チェーン MDLs がサポートされていないため、ドライバーが USB 2.0 ホストコントローラーで動作することも確認してください。</p></li>
<li><p>このエラーを無視するように選択することで、ドライバーがシステムのクラッシュを引き起こしたり応答しなくなったりすることはありません。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>UsbVerifierFailStaticStreamsSupport</strong></p>
<p>呼び出し元が<em>CapabilityType</em>パラメーターに GUID_USB_CAPABILITY_STATIC_STREAMS を渡したときに、クライアントドライバーがこれらのルーチンを呼び出すことができません。</p>
<ul>
<li><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85)" data-raw-source="[&lt;strong&gt;USBD_QueryUsbCapability&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))"><strong>USBD_QueryUsbCapability</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceQueryUsbCapability&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability)"><strong>WdfUsbTargetDeviceQueryUsbCapability</strong></a></li>
</ul></td>
<td><ul>
<li>0: 設定は無効になっています。</li>
<li>1: 呼び出しは常に失敗します。</li>
<li><em>N</em>: 呼び出しは 1/<em>N</em>の確率で失敗します。ここで、 <em>n</em>は 1 ~ 0x7ff の16進数の値です。 たとえば、 <em>N</em>が10の場合、 この呼び出しは、10回呼び出すたびに失敗します。</li>
</ul></td>
<td><p><strong>静的ストリームをサポートしていないホストコントローラーとの通信。</strong></p>
<p>クライアントドライバーが一括エンドポイントの静的ストリームを介して i/o 転送を送信できるようにするには、ホストコントローラーでストリームがサポートされている必要があります。</p>
<p>デバイスがストリームをサポートしていないホストコントローラーに接続されていて、ドライバーがストリーム i/o 転送を実行しようとすると、転送は失敗します。 この設定により、このようなエラーが発生した場合にコードをテストできます。</p>
<p>ホストコントローラーで静的ストリームがサポートされていない場合は、クライアントドライバーの動作が必要です。</p>
<ul>
<li><p>ストリームをサポートしていない xHCI コントローラーをクライアントドライバーが使用する場合は、ストリームが有効な一括エンドポイントを使用せずにデバイスが動作できる必要があります。</p></li>
<li><p>このエラーを無視するように選択することで、ドライバーがシステムのクラッシュを引き起こしたり応答しなくなったりすることはありません。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>UsbVerifierStaticStreamCountOverride</strong></p>
クライアントが GUID_USB_CAPABILITY_STATIC_STREAMS でこれらのルーチンを呼び出すと、 <em>Outputbuffer</em>パラメーターで受け取った値を変更します。
<ul>
<li><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85)" data-raw-source="[&lt;strong&gt;USBD_QueryUsbCapability&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))"><strong>USBD_QueryUsbCapability</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceQueryUsbCapability&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability)"><strong>WdfUsbTargetDeviceQueryUsbCapability</strong></a></li>
</ul>
<p><em>Outputbuffer</em>値は、ホストコントローラーがサポートする静的ストリームの最大数を示します。</p></td>
<td><ul>
<li>0: 設定は無効になっています。</li>
<li>1: 検証ツールは<em>Outputbuffer</em>値をランダムに選択します。 この値は、 <em>Outputbuffer</em>値が繰り返されず、呼び出しがより多くのバリエーションでテストされるため、ストレステストに役立ちます。</li>
<li><p><em>N</em>: <em>outputbuffer</em>値を指定します。</p>
<p>フラグが<em>n</em>値で有効になっている場合、 <em>n</em>は、USB ドライバースタックがサポートするストリームの最大数よりも少なくする必要があります。 したがって、このフラグを設定する前に、正常な呼び出しによって実際の値を取得する必要があります。</p>
<p><em>N</em>がストリームの最大数よりも大きい場合、設定は無視されます。</p></li>
</ul></td>
<td><p><strong>さまざまなホストコントローラーとの通信。それぞれが、ストリームの最大数の異なる値をサポートします。</strong></p>
<p>この設定を使用すると、さまざまなホストコントローラーでサポートされているストリームの数に関係なく、ドライバーのストリームロジックが動作することを確認できます。</p>
<p>I/o 転送に使用できるストリームの数は、ホストコントローラーがサポートするストリームの数によって制限されます。</p>
<p>クライアントドライバーで静的ストリームをサポートする方法の詳細については、「 <a href="how-to-open-streams-in-a-usb-endpoint.md" data-raw-source="[How to Open and Close Static Streams in a USB Bulk Endpoint](how-to-open-streams-in-a-usb-endpoint.md)">USB 一括エンドポイントで静的ストリームを開いて閉じる方法</a>」を参照してください。</p>
<p>ホストコントローラーがエンドポイントよりも多くのストリームをサポートしている場合は、クライアントドライバーの動作が必要です。</p>
<ul>
<li><p>クライアントドライバーは、ストリームの数を減らすことにより、データ転送を実行することを選択できます。</p></li>
<li><p>このエラーを無視するように選択することで、ドライバーがシステムのクラッシュを引き起こしたり応答しなくなったりすることはありません。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>UsbVerifierFailEnableStaticStreams</strong></p>
<p>クライアントドライバーのオープンスタティックストリーム要求 (URB_FUNCTION_OPEN_STATIC_STREAMS) に失敗します。</p></td>
<td><ul>
<li>0: 設定は無効になっています。</li>
<li>1: 要求は常に失敗します。</li>
<li><em>N</em>: 要求は、1/<em>N</em>の確率で失敗します。ここで、 <em>n</em>は 1 ~ 0x7ff の16進数の値です。 たとえば、 <em>N</em>が10の場合、 要求は、10回呼び出すたびに失敗します。</li>
</ul>
<div class="alert">
<strong>メモ</strong> <a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85)" data-raw-source="[&lt;strong&gt;USBD_QueryUsbCapability&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))"><strong>USBD_QueryUsbCapability</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceQueryUsbCapability&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability)"><strong>WdfUsbTargetDeviceQueryUsbCapability</strong></a>への前回の呼び出しが失敗した場合、オープンスタティックストリーム要求は失敗します。
</div>
<div>
 
</div></td>
<td><p><strong>静的ストリームをサポートしているが、その他の理由により要求が失敗した場合のホストコントローラーとの通信。</strong></p>
<p>たとえば、ストリームをサポートするホストコントローラーにデバイスが接続されているとします。 クライアントドライバーは、ホストコントローラーでサポートされているストリームの最大数を超える数 (オープンストリームのストリーム) を含むオープンストリーム要求を送信します。 このような要求は、USB ドライバースタックによって失敗します。</p>
<p>この設定を使用すると、open streams 要求エラーのエラー処理コードをテストできます。</p>
<p>オープンストリーム要求が失敗した場合のクライアントドライバーの動作:</p>
<ul>
<li><p>ドライバーは想定されていませんが、通常どおりに機能します。</p></li>
<li><p>このエラーを無視するように選択することで、ドライバーがシステムのクラッシュを引き起こしたり応答しなくなったりすることはありません。</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[**USBD\_CreateHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createhandle)  
[**USBD\_QueryUsbCapability**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))  
[USB 一括エンドポイントで静的ストリームを開いて閉じる方法](how-to-open-streams-in-a-usb-endpoint.md)  
[チェーン MDLs を送信する方法](how-to-send-chained-mdls.md)  
[USB 診断とテストガイド](usb-driver-testing-guide.md)  



