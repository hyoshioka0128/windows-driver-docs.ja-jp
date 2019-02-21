---
Description: This topic describes the USB client driver verifier feature of the USB 3.0 driver stack that enables the client driver to test certain failure cases.
title: USB クライアント ドライバーの検証ツール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da7649e1b6a7698b8b3e94f8fb4cb67ea0a4dbc0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527578"
---
# <a name="usb-client-driver-verifier"></a>USB クライアント ドライバーの検証ツール


このトピックでは、により、特定のエラー ケースをテストするクライアント ドライバーを USB 3.0 ドライバー スタックの USB クライアント ドライバーの検証の機能について説明します。

-   [USB クライアント ドライバーの検証機能とは](#what-is--the-usb-client-driver-verifier)
-   [USB クライアント ドライバーの検証機能を有効にする方法](#how-to-enable-the-usb-client-driver-verifier)
-   [USB クライアント ドライバーの検証ツールの構成設定](#configuration--settings-for-the-usb-client-driver-verifier)

## <a name="what-is-the-usb-client-driver-verifier"></a>USB クライアント ドライバーの検証機能とは


*USB クライアント ドライバーの検証ツール*Windows 8 に含まれる、USB 3.0 ドライバー スタックの機能です。 検証を有効にすると、USB ドライバー スタックは失敗または、クライアント ドライバーによって実行される特定の操作を変更します。 そのようなエラー シミュレートできない場合がありますそれ以外の場合にエラー状態を検索し、後で、望ましくない結果につながることができます。 シミュレートされたエラーでは、ドライバーがエラーを適切に処理できることを確認する機会を提供します。 クライアントでは、エラー処理コードを使用したエラーを処理したり、異なるコード パスを練習することができます。

たとえば、クライアント ドライバーでは、一括エンドポイントの静的なストリーム間で I/O 操作をサポートしています。 検証ツールを使用するには、そのドライバーのさまざまなホスト コント ローラーでサポートされているストリームの数に関係なくロジックをストリームすることを確認の操作を行うことができます。 このシナリオをシミュレートするには、使用することができます、 **UsbVerifierStaticStreamCountOverride** (後述) を設定します。 ドライバーの呼び出しごとに[ **USBD\_QueryUsbCapability** ](https://msdn.microsoft.com/library/windows/hardware/hh406230)ホスト コント ローラーをサポートする静的なストリームの最大数を確認するのに、ルーチンが別の値を返します。

**重要な**  USB クライアント ドライバーの検証ツールはさまざまな xHCI コント ローラーに対して、ドライバーのみをテストします。 チェーンの MDL サポートの不足など、本質的な 2.0 コント ローラー動作の一部をシミュレートします。 ただし、USB 2.0 コント ローラーと、クライアント ドライバーのテストし、同じの代わりとしてこのツールを使用する必要がありますお勧めします。

 

Windows ハードウェア認定キットには、シミュレートされたテスト_ケースを実行する自動テストが含まれています。 詳細については、次を参照してください。 [USB (USBDEX) Verifier テスト](https://msdn.microsoft.com/library/windows/hardware/hh998558.aspx)します。

## <a name="how-to-enable-the-usb-client-driver-verifier"></a>USB クライアント ドライバーの検証機能を有効にする方法


USB クライアント ドライバーの検証ツールを使用するにを実行する Windows 8 でターゲット コンピューターに有効にします。 ターゲット コンピューターには、xHCI コント ローラー、USB デバイスが接続されている必要があります。

有効にすると、USB クライアント ドライバーの検証ツールが自動的に有効になって、 [Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)クライアント ドライバー用です。 また、このレジストリ エントリを設定して、検証機能を有効にできます。

**注**  Enabling [Windows Driver Foundation (WDF) Verifier コントロール アプリケーション (WdfVerifier.exe)](https://msdn.microsoft.com/library/windows/hardware/ff556129) USB クライアント ドライバーの検証ツールが自動的に有効にできません。

 

```cpp
HKEY_LOCAL_MACHINE
   SYSTEM
      CurrentControlSet
         services
            <Client Driver>
               Parameters
                  UsbVerifierEnabled (DWORD)
```

**UsbVerifierEnabled**レジストリ エントリは、DWORD 値を受け取ります。 ときに**UsbVerifierEnabled**は 1 です。 USB クライアント ドライバーの検証機能が有効になります。 0 はそれを無効にします。 場合、 [Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)クライアント ドライバーが有効になって、 **UsbVerifierEnabled**が 0 の場合、USB クライアント ドライバー検証機能が無効になっています。

## <a name="configuration-settings-for-the-usb-client-driver-verifier"></a>USB クライアント ドライバーの検証ツールの構成設定


USB ドライバー スタックには呼び出すことによって、クライアント ドライバーによって割り当てられる翻訳がの追跡、検証機能を有効にすると、 **USBD\_xxxUrbAllocate**ルーチン (を参照してください[USB ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff540134#client))。 USB ドライバー スタックでその情報を使用してでのバグチェックが発生する場合は、クライアント ドライバーでは、任意 URB をリークで、 [Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)します。 その場合を使用して、 **! usbanalyze v**リークの原因を特定するコマンド。

さらに、必要に応じて、変更または特定のルーチンが失敗してどのくらいの頻度、ルーチンが失敗する必要がありますを指定する USB クライアント ドライバーの検証機能を構成できます。 で、検証機能を構成するには、次のようにレジストリ エントリを設定します。

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
追加、変更、または任意の設定を削除する場合は、デバイス設定を適用するシステムを再列挙する必要があります。

このテーブルは、可能な値を示しています。  *&lt;USB クライアント ドライバーの検証設定&gt;* します。 設定で指定されているクライアント ドライバーを適用する、**サービス**キー。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>USB クライアント ドライバーの検証の設定</th>
<th>これらの使用可能な値のいずれかを選択します。</th>
<th>これを使用すると、シミュレートしてください.</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>UsbVerifierFailRegistration</strong></p>
<p>クライアント ドライバーが失敗した&#39;にこれらのルーチンの呼び出し。</p>
<ul>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh439428" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceCreateWithParameters&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439428)"><strong>WdfUsbTargetDeviceCreateWithParameters</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh406241" data-raw-source="[&lt;strong&gt;USBD_CreateHandle&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406241)"><strong>USBD_CreateHandle</strong></a></li>
</ul></td>
<td><ul>
<li>0:設定を無効にします。</li>
<li>1:呼び出しは常に失敗します。</li>
<li><em>N</em>:1 の確率で呼び出しに失敗した/<em>N</em>ここで、 <em>N</em> 0x7FF に 1 の間の 16 進値です。 たとえば場合、 <em>N</em> 10。 呼び出しでは、10 回ごとに 1 回が失敗します。</li>
</ul></td>
<td><p><strong>クライアント ドライバーの登録に失敗しました。</strong></p>
<p>基になるドライバー スタックの登録に、クライアント ドライバーの初期化タスクの 1 つです。 いくつかの後続の呼び出しで、登録が必要です。</p>
<p>たとえば、クライアント ドライバーが呼び出す<a href="https://msdn.microsoft.com/library/windows/hardware/hh406241" data-raw-source="[&lt;strong&gt;USBD_CreateHandle&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406241)"> <strong>USBD_CreateHandle</strong> </a>登録します。 ように&#39;とドライバーには、ルーチンが常に STATUS_SUCCESS を返し、エラーを処理するコードを実装していないことが前提としています。 ルーチンがエラー NTSTATUS コードを返した場合、ドライバーできます誤ってエラーを無視して USBD 無効なハンドルを使用して、後続の呼び出しを続行します。</p>
<p>設定を使用すると、コード パスの障害をテストすることができるため、呼び出しが失敗することができます。</p>
<p>登録に失敗したときに、クライアント ドライバーの動作が必要です。</p>
<ul>
<li><p>ドライバーでは引き続き通常どおりに機能を必要はありません。</p></li>
<li><p>ドライバーがシステム クラッシュが発生するかによってこのエラーを無視する選択が応答しなくなるいない必要があります。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>UsbVerifierFailChainedMdlSupport</strong></p>
<p>クライアント ドライバーが失敗した&#39;s、呼び出し元で GUID_USB_CAPABILITY_CHAINED_MDLS が成功したとき、これらのルーチンの呼び出し、 <em>CapabilityType</em>パラメーター。</p>
<ul>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh406230" data-raw-source="[&lt;strong&gt;USBD_QueryUsbCapability&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406230)"><strong>USBD_QueryUsbCapability</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh439434" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceQueryUsbCapability&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439434)"><strong>WdfUsbTargetDeviceQueryUsbCapability</strong></a></li>
</ul></td>
<td><ul>
<li>0:設定を無効にします。</li>
<li>1:呼び出しは常に失敗します。</li>
<li><em>N</em>:1 の確率で呼び出しに失敗した/<em>N</em>ここで、 <em>N</em> 0x7FF に 1 の間の 16 進値です。 たとえば場合、 <em>N</em> 10。 呼び出しでは、10 回ごとに 1 回が失敗します。</li>
</ul></td>
<td><p><strong>サポートされていないホスト コント ローラーとの通信には、MDLs がチェーンされています。</strong></p>
<p>クライアント ドライバーに送信するチェーン MDLs (を参照してください<a href="https://msdn.microsoft.com/library/windows/hardware/ff565421" data-raw-source="[MDL](https://msdn.microsoft.com/library/windows/hardware/ff565421)">MDL</a>)、USB ドライバー スタックとホスト コント ローラーはそれらでサポートする必要があります。</p>
<p>この設定では、クライアント ドライバーがサポートしていないホスト コント ローラーに接続されているデバイスに連鎖 MDL 要求を送信するときに実行されるコードをテストできます。 ホスト コント ローラーが連鎖 MDLs をサポートするかどうかに関係なく、呼び出しが失敗します。</p>
<p>USB ドライバー スタック内のチェーンの MDLs サポートの詳細については、次を参照してください。<a href="how-to-send-chained-mdls.md" data-raw-source="[How to Send Chained MDLs](how-to-send-chained-mdls.md)">チェーン MDLs の送信方法</a>します。</p>
<p>ホスト コント ローラーがサポートされていないときに必要なクライアント ドライバーの動作は、MDLs を連結します。</p>
<ul>
<li><p>I/O の転送を連鎖 MDLs を使用せず実行を継続、ドライバーが必要です。 これにより、ことを確認することも、これらのコント ローラーはサポートされないために、ドライバーが USB 2.0 ホスト コント ローラーで動作する MDLs をチェーンします。</p></li>
<li><p>ドライバーがシステム クラッシュが発生するかによってこのエラーを無視する選択が応答しなくなるいない必要があります。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>UsbVerifierFailStaticStreamsSupport</strong></p>
<p>クライアント ドライバーが失敗した&#39;s、呼び出し元で GUID_USB_CAPABILITY_STATIC_STREAMS が成功したとき、これらのルーチンの呼び出し、 <em>CapabilityType</em>パラメーター。</p>
<ul>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh406230" data-raw-source="[&lt;strong&gt;USBD_QueryUsbCapability&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406230)"><strong>USBD_QueryUsbCapability</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh439434" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceQueryUsbCapability&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439434)"><strong>WdfUsbTargetDeviceQueryUsbCapability</strong></a></li>
</ul></td>
<td><ul>
<li>0:設定を無効にします。</li>
<li>1:呼び出しは常に失敗します。</li>
<li><em>N</em>:1 の確率で呼び出しに失敗した/<em>N</em>ここで、 <em>N</em> 0x7FF に 1 の間の 16 進値です。 たとえば場合、 <em>N</em> 10。 呼び出しには、10 回ごとに 1 回は失敗します。</li>
</ul></td>
<td><p><strong>静的なストリームをサポートしないホスト コント ローラーと通信します。</strong></p>
<p>クライアント ドライバーの一括エンドポイント静的ストリーム間で I/O の転送を送信するためには、ホスト コント ローラーは、ストリームをサポートする必要があります。</p>
<p>場合は、デバイスは、ストリームをサポートしないホスト コント ローラーに接続し、ドライバーがストリーム I/O の転送を実行して、それらの転送は失敗します。 この設定では、このようなエラーが発生した場合、コードをテストできます。</p>
<p>ホスト コント ローラーは静的なストリームをサポートしていない場合、クライアント ドライバーの動作が必要です。</p>
<ul>
<li><p>クライアント ドライバーは、ストリームをサポートしていない xHCI コント ローラーを使用する場合、デバイスは、一括のストリームが有効なエンドポイントを使用せずに作業できる必要があります。</p></li>
<li><p>ドライバーがシステム クラッシュが発生するかによってこのエラーを無視する選択が応答しなくなるいない必要があります。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>UsbVerifierStaticStreamCountOverride</strong></p>
受信した値を変更、 <em>OutputBuffer</em> GUID_USB_CAPABILITY_STATIC_STREAMS でこれらのルーチンへのクライアントの呼び出し時にパラメーター。
<ul>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh406230" data-raw-source="[&lt;strong&gt;USBD_QueryUsbCapability&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406230)"><strong>USBD_QueryUsbCapability</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh439434" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceQueryUsbCapability&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439434)"><strong>WdfUsbTargetDeviceQueryUsbCapability</strong></a></li>
</ul>
<p><em>OutputBuffer</em>値は、ホスト コント ローラーをサポートする静的なストリームの最大数を示します。</p></td>
<td><ul>
<li>0:設定を無効にします。</li>
<li>1:検証方法の選択、 <em>OutputBuffer</em>値をランダムにします。 この値は、ストレス テストのための便利な<em>OutputBuffer</em>値は繰り返されません、呼び出しは複数のバリエーションでテストします。</li>
<li><p><em>N</em>:指定します、 <em>OutputBuffer</em>値。</p>
<p>フラグが有効な場合<em>N</em>値、 <em>N</em> USB ドライバー スタックをサポートするストリームの最大数より小さくなければなりません。 そのため、このフラグを設定する前にする必要がありますが取得した正常な呼び出しによって実際の値。</p>
<p>場合<em>N</em>が最大数よりも大きい、ストリームの設定は無視されます。</p></li>
</ul></td>
<td><p><strong>ストリームの最大数の異なる値をサポートしており、さまざまなホスト コント ローラーとの通信をします。</strong></p>
<p>この設定を使用して確認できますドライバー&#39;s のさまざまなホスト コント ローラーでサポートされているストリームの数に関係なくロジックはストリームです。</p>
<p>I/O の転送に使用できるストリームの数は、ホスト コント ローラーをサポートするストリームの数によって制限されます。</p>
<p>クライアント ドライバーで静的なストリームをサポートする方法については、次を参照してください。 <a href="how-to-open-streams-in-a-usb-endpoint.md" data-raw-source="[How to Open and Close Static Streams in a USB Bulk Endpoint](how-to-open-streams-in-a-usb-endpoint.md)">USB 一括エンドポイントで静的ストリームを開くおよび閉じる方法</a>します。</p>
<p>ホスト コント ローラーは、エンドポイントよりも少ないストリームをサポートしている場合、クライアント ドライバーの動作が必要です。</p>
<ul>
<li><p>ストリーム数が少ないデータの転送を実行するクライアント ドライバーを選択できます。</p></li>
<li><p>ドライバーがシステム クラッシュが発生するかによってこのエラーを無視する選択が応答しなくなるいない必要があります。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>UsbVerifierFailEnableStaticStreams</strong></p>
<p>クライアント ドライバーが失敗した&#39;s は、静的なストリーム要求 (URB_FUNCTION_OPEN_STATIC_STREAMS) を開きます。</p></td>
<td><ul>
<li>0:設定を無効にします。</li>
<li>1:要求は常に失敗します。</li>
<li><em>N</em>:1 の確率で、要求は失敗/<em>N</em>ここで、 <em>N</em> 0x7FF に 1 の間の 16 進値です。 たとえば場合、 <em>N</em> 10。 要求では、10 回ごとに 1 回が失敗します。</li>
</ul>
<div class="alert">
<strong>注</strong>場合、開いている静的ストリーム要求が失敗した前回の呼び出し<a href="https://msdn.microsoft.com/library/windows/hardware/hh406230" data-raw-source="[&lt;strong&gt;USBD_QueryUsbCapability&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406230)"> <strong>USBD_QueryUsbCapability</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/hh439434" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceQueryUsbCapability&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439434)"> <strong>WdfUsbTargetDeviceQueryUsbCapability</strong> </a>できませんでした。
</div>
<div>
 
</div></td>
<td><p><strong>要求が静的なストリームをサポートするホスト コント ローラーとの通信は、その他の理由で失敗します。</strong></p>
<p>たとえば、デバイスは、ストリームをサポートするホスト コント ローラーに接続されます。 クライアント ドライバーでは、ホスト コント ローラーでサポートされているストリームの最大数を超える数 (ストリームを開く) の要求を開いているストリームを送信します。 USB ドライバー スタックは、このような要求は失敗します。</p>
<p>この設定を使用すると、エラー処理コードを開いているストリーム要求の失敗をテストできます。</p>
<p>オープン ストリーム要求が失敗した場合、クライアント ドライバーの動作が必要です。</p>
<ul>
<li><p>ドライバーでは引き続き通常どおりに機能を必要はありません。</p></li>
<li><p>ドライバーがシステム クラッシュが発生するかによってこのエラーを無視する選択が応答しなくなるいない必要があります。</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[**USBD\_CreateHandle**](https://msdn.microsoft.com/library/windows/hardware/hh406241)  
[**USBD\_QueryUsbCapability**](https://msdn.microsoft.com/library/windows/hardware/hh406230)  
[USB 一括エンドポイントでのオープンとクローズの静的なストリームする方法](how-to-open-streams-in-a-usb-endpoint.md)  
[連鎖 MDLs を送信する方法](how-to-send-chained-mdls.md)  
[USB の診断結果とテスト ガイド](usb-driver-testing-guide.md)  



