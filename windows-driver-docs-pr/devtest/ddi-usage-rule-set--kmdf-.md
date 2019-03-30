---
title: DDI 使用の規則セット (KMDF)
description: これらの規則を使用すると、ドライバー、正しく使用する KMDF Ddi 正しくを確認します。
ms.assetid: 0A3A012C-A1BB-43A5-B38D-4E98928D07E5
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6c109f4a92f9311712281fd9c8576fd1fdd31aca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577699"
---
# <a name="ddi-usage-rule-set-kmdf"></a>DDI 使用の規則セット (KMDF)


これらの規則を使用すると、ドライバー、正しく使用する KMDF Ddi 正しくを確認します。

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="kmdf-bufafterreqcompletedioctl.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedIoctl&lt;/strong&gt;](kmdf-bufafterreqcompletedioctl.md)"><strong>BufAfterReqCompletedIoctl</strong></a></p></td>
<td align="left"><p><a href="kmdf-bufafterreqcompletedioctl.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedIoctl&lt;/strong&gt;](kmdf-bufafterreqcompletedioctl.md)"> <strong>BufAfterReqCompletedIoctl</strong> </a>ルールでは、ことを指定します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff541758" data-raw-source="[&lt;em&gt;EvtIoDeviceControl&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541758)"> <em>EvtIoDeviceControl</em> </a>コールバック関数では、I/O 要求バッファーの取得は、I/O 要求が完了した後にアクセスできません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-bufafterreqcompletedintioctl.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedIntIoctl&lt;/strong&gt;](kmdf-bufafterreqcompletedintioctl.md)"><strong>BufAfterReqCompletedIntIoctl</strong></a></p></td>
<td align="left"><p><a href="kmdf-bufafterreqcompletedintioctl.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedIntIoctl&lt;/strong&gt;](kmdf-bufafterreqcompletedintioctl.md)"> <strong>BufAfterReqCompletedIntIoctl</strong> </a>ルールでは、要求が完了すると、そのバッファーにアクセスできないことを指定します (内部<a href="https://msdn.microsoft.com/library/windows/hardware/ff541768" data-raw-source="[&lt;em&gt;EvtIoInternalDeviceControl&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541768)"> <em>EvtIoInternalDeviceControl</em></a>コールバック関数のみ)。 バッファーが呼び出すことによって取得<a href="https://msdn.microsoft.com/library/windows/hardware/ff550018" data-raw-source="[&lt;strong&gt;WdfRequestRetrieveOutputBuffer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550018)"> <strong>WdfRequestRetrieveOutputBuffer</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff550024" data-raw-source="[&lt;strong&gt;WdfRequestRetrieveUnsafeUserOutputBuffer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550024)"> <strong>WdfRequestRetrieveUnsafeUserOutputBuffer</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff550014" data-raw-source="[&lt;strong&gt;WdfRequestRetrieveInputBuffer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550014)"> <strong>WdfRequestRetrieveInputBuffer</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff550022" data-raw-source="[&lt;strong&gt;WdfRequestRetrieveUnsafeUserInputBuffer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550022)"> <strong>WdfRequestRetrieveUnsafeUserInputBuffer</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-bufafterreqcompletedintioctla.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedIntIoctlA&lt;/strong&gt;](kmdf-bufafterreqcompletedintioctla.md)"><strong>BufAfterReqCompletedIntIoctlA</strong></a></p></td>
<td align="left"><p><a href="kmdf-bufafterreqcompletedintioctla.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedIntIoctlA&lt;/strong&gt;](kmdf-bufafterreqcompletedintioctla.md)"> <strong>BufAfterReqCompletedIntIoctlA</strong> </a>ルールは、要求が完了した後、バッファーにアクセスできないことを確認します (内部<a href="https://msdn.microsoft.com/library/windows/hardware/ff541768" data-raw-source="[&lt;em&gt;EvtIoInternalDeviceControl&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541768)"> <em>EvtIoInternalDeviceControl</em></a>コールバックのみ)。 バッファーが呼び出すことによって取得された<a href="https://msdn.microsoft.com/library/windows/hardware/ff550014" data-raw-source="[&lt;strong&gt;WdfRequestRetrieveInputBuffer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550014)"> <strong>WdfRequestRetrieveInputBuffer</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff550018" data-raw-source="[&lt;strong&gt;WdfRequestRetrieveOutputBuffer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550018)"> <strong>WdfRequestRetrieveOutputBuffer</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff550022" data-raw-source="[&lt;strong&gt;WdfRequestRetrieveUnsafeUserInputBuffer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550022)"> <strong>WdfRequestRetrieveUnsafeUserInputBuffer</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff550024" data-raw-source="[&lt;strong&gt;WdfRequestRetrieveUnsafeUserOutputBuffer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550024)"> <strong>WdfRequestRetrieveUnsafeUserOutputBuffer</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-bufafterreqcompletedioctla.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedIoctlA&lt;/strong&gt;](kmdf-bufafterreqcompletedioctla.md)"><strong>BufAfterReqCompletedIoctlA</strong></a></p></td>
<td align="left"><p><a href="kmdf-bufafterreqcompletedioctla.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedIoctlA&lt;/strong&gt;](kmdf-bufafterreqcompletedioctla.md)"> <strong>BufAfterReqCompletedIoctlA</strong> </a>ルールでは、ことを指定します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff541758" data-raw-source="[&lt;em&gt;EvtIoDeviceControl&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541758)"> <em>EvtIoDeviceControl</em> </a>コールバック関数では、I/O 要求バッファーの取得は、I/O 要求が完了した後にアクセスできません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-bufafterreqcompletedread.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedRead&lt;/strong&gt;](kmdf-bufafterreqcompletedread.md)"><strong>BufAfterReqCompletedRead</strong></a></p></td>
<td align="left"><p><a href="kmdf-bufafterreqcompletedread.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedRead&lt;/strong&gt;](kmdf-bufafterreqcompletedread.md)"> <strong>BufAfterReqCompletedRead</strong> </a>ルールでは、ことを指定します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff541776" data-raw-source="[&lt;em&gt;EvtIoRead&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541776)"> <em>EvtIoRead</em> </a>コールバック関数では、I/O 要求のバッファー取得される I/O 要求が完了した後にアクセスすることはできません。 バッファーへのアクセス方法として機能する 14 Ddi があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-bufafterreqcompletedreada.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedReadA&lt;/strong&gt;](kmdf-bufafterreqcompletedreada.md)"><strong>BufAfterReqCompletedReadA</strong></a></p></td>
<td align="left"><p>BufAfterReqCompletedReadA ルールでは、ことを指定します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff541776" data-raw-source="[&lt;em&gt;EvtIoRead&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541776)"> <em>EvtIoRead</em> </a> I/O 要求が完了した後、コールバック関数、取得される I/O 要求のバッファーにアクセスできません。 バッファーへのアクセス方法として機能する 14 Ddi があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-bufafterreqcompletedwrite.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedWrite&lt;/strong&gt;](kmdf-bufafterreqcompletedwrite.md)"><strong>BufAfterReqCompletedWrite</strong></a></p></td>
<td align="left"><p>BufAfterReqCompletedWrite ルールでは、ことを指定します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff541813" data-raw-source="[&lt;em&gt;EvtIoWrite&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541813)"> <em>EvtIoWrite</em> </a> I/O 要求が完了した後、コールバック関数、取得される I/O 要求のバッファーにアクセスできません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-bufafterreqcompletedwritea.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedWriteA&lt;/strong&gt;](kmdf-bufafterreqcompletedwritea.md)"><strong>BufAfterReqCompletedWriteA</strong></a></p></td>
<td align="left"><p>BufAfterReqCompletedWriteA ルールでは、ことを指定します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff541813" data-raw-source="[&lt;em&gt;EvtIoWrite&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541813)"> <em>EvtIoWrite</em> </a> I/O 要求が完了した後、コールバック関数、取得される I/O 要求のバッファーにアクセスできません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-childdeviceinitapi.md" data-raw-source="[&lt;strong&gt;ChildDeviceInitApi&lt;/strong&gt;](kmdf-childdeviceinitapi.md)"><strong>ChildDeviceInitApi</strong></a></p></td>
<td align="left"><p><a href="kmdf-childdeviceinitapi.md" data-raw-source="[&lt;strong&gt;ChildDeviceInitApi&lt;/strong&gt;](kmdf-childdeviceinitapi.md)"> <strong>ChildDeviceInitApi</strong> </a>ルールでは、子デバイスの場合は、framework デバイス オブジェクトの初期化メソッドをドライバーの呼び出しの前に呼び出す必要がありますを指定します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff545926" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545926)"> <strong>WdfDeviceCreate</strong> </a>子デバイス オブジェクトのメソッド。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-controldevicedeleted.md" data-raw-source="[&lt;strong&gt;ControlDeviceDeleted&lt;/strong&gt;](kmdf-controldevicedeleted.md)"><strong>ControlDeviceDeleted</strong></a></p></td>
<td align="left"><p>ControDeviceDeleted ルールでは、PnP ドライバーでは、コントロールのデバイス オブジェクトを作成する場合、ドライバーはドライバーがアンロードする前に、クリーンアップのコールバック関数のいずれかで制御デバイス オブジェクトを削除する必要があるを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-controldeviceinitapi.md" data-raw-source="[&lt;strong&gt;ControlDeviceInitAPI&lt;/strong&gt;](kmdf-controldeviceinitapi.md)"><strong>ControlDeviceInitAPI</strong></a></p></td>
<td align="left"><p>ControlDeviceInitAPI ルールを指定する<a href="https://msdn.microsoft.com/library/windows/hardware/ff545841" data-raw-source="[&lt;strong&gt;WdfControlDeviceInitAllocate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545841)"> <strong>WdfControlDeviceInitAllocate</strong> </a>とすべての他のデバイス オブジェクトの初期化を設定する Ddi、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff546951" data-raw-source="[&lt;strong&gt;WDFDEVICE_INIT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546951)"> <strong>WDFDEVICE_INIT</strong></a>制御デバイスは、前に呼び出す必要がありますの構造体<a href="https://msdn.microsoft.com/library/windows/hardware/ff545926" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545926)"> <strong>WdfDeviceCreate</strong> </a>制御デバイスです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-ctldevicefinishinitdeviceadd.md" data-raw-source="[&lt;strong&gt;CtlDeviceFinishInitDeviceAdd&lt;/strong&gt;](kmdf-ctldevicefinishinitdeviceadd.md)"><strong>CtlDeviceFinishInitDeviceAdd</strong></a></p></td>
<td align="left"><p><a href="kmdf-ctldevicefinishinitdeviceadd.md" data-raw-source="[&lt;strong&gt;CtlDeviceFinishInitDeviceAdd&lt;/strong&gt;](kmdf-ctldevicefinishinitdeviceadd.md)"> <strong>CtlDeviceFinishInitDeviceAdd</strong> </a>ルール指定するドライバーでデバイス オブジェクトのコントロールを作成する場合、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff541693" data-raw-source="[&lt;em&gt;EvtDriverDeviceAdd&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541693)"> <em>EvtDriverDeviceAdd</em> </a>コールバック関数を呼び出す必要があります<a href="https://msdn.microsoft.com/library/windows/hardware/ff545854" data-raw-source="[&lt;strong&gt;WdfControlFinishInitializing&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545854)"> <strong>WdfControlFinishInitializing</strong> </a>から終了前に、デバイスが作成された後、 <strong>EvtDriverDeviceAdd</strong>コールバック関数。 このルールは、非 PnP ドライバーには適用されません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-ctldevicefinishinitdrentry.md" data-raw-source="[&lt;strong&gt;CtlDeviceFinishInitDrEntry&lt;/strong&gt;](kmdf-ctldevicefinishinitdrentry.md)"><strong>CtlDeviceFinishInitDrEntry</strong></a></p></td>
<td align="left"><p>CtlDeviceFinishInitDrEntry ルール指定するドライバーの制御デバイス オブジェクトを作成する場合、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff540807" data-raw-source="[&lt;strong&gt;DriverEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540807)"> <strong>DriverEntry</strong> </a>コールバック関数を呼び出す必要があります<a href="https://msdn.microsoft.com/library/windows/hardware/ff545854" data-raw-source="[&lt;strong&gt;WdfControlFinishInitializing&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545854)"> <strong>WdfControlFinishInitializing</strong> </a>から終了前に、デバイスが作成された後、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff541693" data-raw-source="[&lt;em&gt;EvtDriverDeviceAdd&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541693)"> <em>EvtDriverDeviceAdd</em> </a>コールバック関数。 このルールは、非 PnP ドライバーには適用されません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-devicecreatefail.md" data-raw-source="[&lt;strong&gt;DeviceCreateFail&lt;/strong&gt;](kmdf-devicecreatefail.md)"><strong>DeviceCreateFail</strong></a></p></td>
<td align="left"><p><a href="kmdf-devicecreatefail.md" data-raw-source="[&lt;strong&gt;DeviceCreateFail&lt;/strong&gt;](kmdf-devicecreatefail.md)"> <strong>DeviceCreateFail</strong> </a>ルール EVT_WDF_DRIVER_DEVICE_ADD がエラー状態を返すことを指定するときにへの呼び出し<a href="https://msdn.microsoft.com/library/windows/hardware/ff545926" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545926)"> <strong>WdfDeviceCreate</strong> </a>は失敗します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-deviceinitallocate.md" data-raw-source="[&lt;strong&gt;DeviceInitAllocate&lt;/strong&gt;](kmdf-deviceinitallocate.md)"><strong>DeviceInitAllocate</strong></a></p></td>
<td align="left"><p><a href="kmdf-deviceinitallocate.md" data-raw-source="[&lt;strong&gt;DeviceInitAllocate&lt;/strong&gt;](kmdf-deviceinitallocate.md)"> <strong>DeviceInitAllocate</strong> </a>ルールは、PDO デバイスまたはデバイスにコントロール オブジェクトは、framework デバイス オブジェクトの初期化メソッドを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548786" data-raw-source="[&lt;strong&gt;WdfPdoInitAllocate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548786)"> <strong>WdfPdoInitAllocate</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff545841" data-raw-source="[&lt;strong&gt;WdfControlDeviceInitAllocate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545841)"> <strong>WdfControlDeviceInitAllocate</strong> </a>ドライバー呼び出しの前に呼び出す必要があります<a href="https://msdn.microsoft.com/library/windows/hardware/ff545926" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545926)"> <strong>WdfDeviceCreate</strong></a>.</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-deviceinitapi.md" data-raw-source="[&lt;strong&gt;DeviceInitAPI&lt;/strong&gt;](kmdf-deviceinitapi.md)"><strong>DeviceInitAPI</strong></a></p></td>
<td align="left"><p>ドライバーの呼び出しの前に、framework デバイス オブジェクトの初期化方法と framework FDO の初期化メソッド FDO デバイスの場合、呼び出す必要があります、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff545926" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545926)"> <strong>WdfDeviceCreate</strong> </a>デバイスのメソッドオブジェクト。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-doubledeviceinitfree.md" data-raw-source="[&lt;strong&gt;DoubleDeviceInitFree&lt;/strong&gt;](kmdf-doubledeviceinitfree.md)"><strong>DoubleDeviceInitFree</strong></a></p></td>
<td align="left"><p><a href="kmdf-doubledeviceinitfree.md" data-raw-source="[&lt;strong&gt;DoubleDeviceInitFree&lt;/strong&gt;](kmdf-doubledeviceinitfree.md)"> <strong>DoubleDeviceInitFree</strong> </a>ルールでは、ドライバーする必要がありますデバイス初期化構造体を 2 回解放していないことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-drivercreate.md" data-raw-source="[&lt;strong&gt;DriverCreate&lt;/strong&gt;](kmdf-drivercreate.md)"><strong>DriverCreate</strong></a></p></td>
<td align="left"><p><a href="kmdf-drivercreate.md" data-raw-source="[&lt;strong&gt;DriverCreate&lt;/strong&gt;](kmdf-drivercreate.md)"> <strong>DriverCreate</strong> </a>ルールでは、カーネル モード ドライバー フレームワーク (KMDF) を使用するドライバーを呼び出す必要がありますを指定します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff547175" data-raw-source="[&lt;strong&gt;WdfDriverCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547175)"> <strong>WdfDriverCreate</strong> </a>メソッド内から、framework ドライバー オブジェクトを作成するその<a href="https://msdn.microsoft.com/library/windows/hardware/ff540807" data-raw-source="[&lt;strong&gt;DriverEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540807)"> <strong>DriverEntry</strong> </a>ルーチン。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-initfreedevicecallback.md" data-raw-source="[&lt;strong&gt;InitFreeDeviceCallback&lt;/strong&gt;](kmdf-initfreedevicecallback.md)"><strong>InitFreeDeviceCallback</strong></a></p></td>
<td align="left"><p>InitFreeDeviceCallback ルールでは、ドライバーを呼び出す必要がありますを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff546050" data-raw-source="[&lt;strong&gt;WdfDeviceInitFree&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546050)"> <strong>WdfDeviceInitFree</strong> </a>ドライバーでは、新しい framework デバイス オブジェクトを初期化中にエラーが発生した場合と、ドライバーが受信した場合<a href="https://msdn.microsoft.com/library/windows/hardware/ff546951" data-raw-source="[&lt;strong&gt;WDFDEVICE_INIT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546951)"> <strong>WDFDEVICE_INIT</strong> </a>構造体への呼び出しから<a href="https://msdn.microsoft.com/library/windows/hardware/ff545841" data-raw-source="[&lt;strong&gt;WdfControlDeviceInitAllocate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545841)"> <strong>WdfControlDeviceInitAllocate</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-initfreedevicecreate.md" data-raw-source="[&lt;strong&gt;InitFreeDeviceCreate&lt;/strong&gt;](kmdf-initfreedevicecreate.md)"><strong>InitFreeDeviceCreate</strong></a></p></td>
<td align="left"><p><a href="kmdf-initfreedevicecreate.md" data-raw-source="[&lt;strong&gt;InitFreeDeviceCreate&lt;/strong&gt;](kmdf-initfreedevicecreate.md)"> <strong>InitFreeDeviceCreate</strong> </a>ルールでは、ドライバーを呼び出す必要がありますを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff546050" data-raw-source="[&lt;strong&gt;WdfDeviceInitFree&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546050)"> <strong>WdfDeviceInitFree</strong> </a>の代わりに<a href="https://msdn.microsoft.com/library/windows/hardware/ff545926" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545926)"> <strong>WdfDeviceCreate</strong> </a>デバイス オブジェクトの初期化メソッドのいずれかでエラーが発生した場合と、ドライバーが受信した場合、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff546951" data-raw-source="[&lt;strong&gt;WDFDEVICE_INIT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546951)"> <strong>WDFDEVICE_INIT</strong> </a>構造体呼び出しから<a href="https://msdn.microsoft.com/library/windows/hardware/ff545841" data-raw-source="[&lt;strong&gt;WdfControlDeviceInitAllocate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545841)"> <strong>WdfControlDeviceInitAllocate</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-initfreedevicecreatetype2.md" data-raw-source="[&lt;strong&gt;InitFreeDeviceCreateType2&lt;/strong&gt;](kmdf-initfreedevicecreatetype2.md)"><strong>InitFreeDeviceCreateType2</strong></a></p></td>
<td align="left"><p>InitFreeDeviceCreateType2 ルールでは、ドライバーを呼び出してはならないことを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff545926" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545926)"> <strong>WdfDeviceCreate</strong> </a>呼び出した後<a href="https://msdn.microsoft.com/library/windows/hardware/ff546050" data-raw-source="[&lt;strong&gt;WdfDeviceInitFree&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546050)"> <strong>WdfDeviceInitFree</strong> </a>.</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-initfreedevicecreatetype4.md" data-raw-source="[&lt;strong&gt;InitFreeDeviceCreateType4&lt;/strong&gt;](kmdf-initfreedevicecreatetype4.md)"><strong>InitFreeDeviceCreateType4</strong></a></p></td>
<td align="left"><p><a href="kmdf-initfreedevicecreatetype4.md" data-raw-source="[&lt;strong&gt;InitFreeDeviceCreateType4&lt;/strong&gt;](kmdf-initfreedevicecreatetype4.md)"> <strong>InitFreeDeviceCreateType4</strong> </a>ルールでは、ドライバーを呼び出す必要がありますを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff546050" data-raw-source="[&lt;strong&gt;WdfDeviceInitFree&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546050)"> <strong>WdfDeviceInitFree</strong> </a>ドライバーが検出したかどうか、呼び出し中にエラー <a href="https://msdn.microsoft.com/library/windows/hardware/ff545926" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545926)"> <strong>WdfDeviceCreate</strong> </a>ドライバーが受信した場合と、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff546951" data-raw-source="[&lt;strong&gt;WDFDEVICE_INIT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546951)"> <strong>WDFDEVICE_INIT</strong> </a>呼び出しからの構造<a href="https://msdn.microsoft.com/library/windows/hardware/ff545841" data-raw-source="[&lt;strong&gt;WdfControlDeviceInitAllocate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545841)"> <strong>WdfControlDeviceInitAllocate</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-initfreenull.md" data-raw-source="[&lt;strong&gt;InitFreeNull&lt;/strong&gt;](kmdf-initfreenull.md)"><strong>InitFreeNull</strong></a></p></td>
<td align="left"><p><a href="kmdf-initfreenull.md" data-raw-source="[&lt;strong&gt;InitFreeNull&lt;/strong&gt;](kmdf-initfreenull.md)"> <strong>InitFreeNull</strong> </a>ルール Ddi PWDFDEVICE_INIT をパラメーターとして受け取ることはできません呼び出すように指定して、使用して、 <strong>NULL</strong>へのポインターを<a href="https://msdn.microsoft.com/library/windows/hardware/ff546951" data-raw-source="[WDFDEVICE_INIT](https://msdn.microsoft.com/library/windows/hardware/ff546951)">WDFDEVICE_INIT</a>構造体。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-mdlafterreqcompletedintioctl.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedIntIoctl&lt;/strong&gt;](kmdf-mdlafterreqcompletedintioctl.md)"><strong>MdlAfterReqCompletedIntIoctl</strong></a></p></td>
<td align="left"><p>MdlAfterReqCompletedIntIoctl ルールでは、ことを指定します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff541768" data-raw-source="[&lt;em&gt;EvtIoInternalDeviceControl&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541768)"> <em>EvtIoInternalDeviceControl</em> </a> I/O 要求がコールバック関数では、メモリの記述子のリスト (MDL) にアクセスできません完了しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-mdlafterreqcompletedintioctla.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedIntIoctlA&lt;/strong&gt;](kmdf-mdlafterreqcompletedintioctla.md)"><strong>MdlAfterReqCompletedIntIoctlA</strong></a></p></td>
<td align="left"><p><a href="kmdf-mdlafterreqcompletedintioctla.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedIntIoctlA&lt;/strong&gt;](kmdf-mdlafterreqcompletedintioctla.md)"> <strong>MdlAfterReqCompletedIntIoctlA</strong> </a>ルールでは、ことを指定します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff541768" data-raw-source="[&lt;em&gt;EvtIoInternalDeviceControl&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541768)"> <em>EvtIoInternalDeviceControl</em> </a>コールバック関数、メモリ記述子一覧 (MDL) は、I/O 要求が完了した後にアクセスすることはできません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-mdlafterreqcompletedioctl.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedIoctl&lt;/strong&gt;](kmdf-mdlafterreqcompletedioctl.md)"><strong>MdlAfterReqCompletedIoctl</strong></a></p></td>
<td align="left"><p><a href="kmdf-mdlafterreqcompletedioctl.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedIoctl&lt;/strong&gt;](kmdf-mdlafterreqcompletedioctl.md)"> <strong>MdlAfterReqCompletedIoctl</strong> </a>ルールでは、ことを指定します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff541758" data-raw-source="[&lt;em&gt;EvtIoDeviceControl&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541758)"> <em>EvtIoDeviceControl</em> </a>コールバック関数では、メモリ記述子一覧 (MDL) は、I/O 要求が完了した後にアクセスすることはできません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-mdlafterreqcompletedioctla.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedIoctlA&lt;/strong&gt;](kmdf-mdlafterreqcompletedioctla.md)"><strong>MdlAfterReqCompletedIoctlA</strong></a></p></td>
<td align="left"><p><a href="kmdf-mdlafterreqcompletedioctla.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedIoctlA&lt;/strong&gt;](kmdf-mdlafterreqcompletedioctla.md)"> <strong>MdlAfterReqCompletedIoctlA</strong> </a>ルールでは、ことを指定します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff541758" data-raw-source="[&lt;em&gt;EvtIoDeviceControl&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541758)"> <em>EvtIoDeviceControl</em> </a>コールバック関数では、メモリ記述子一覧 (MDL) は、I/O 要求が完了した後にアクセスすることはできません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-mdlafterreqcompletedread.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedRead&lt;/strong&gt;](kmdf-mdlafterreqcompletedread.md)"><strong>MdlAfterReqCompletedRead</strong></a></p></td>
<td align="left"><p><a href="kmdf-mdlafterreqcompletedread.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedRead&lt;/strong&gt;](kmdf-mdlafterreqcompletedread.md)"> <strong>MdlAfterReqCompletedRead</strong> </a>ルールでは、ことを指定します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff541776" data-raw-source="[&lt;em&gt;EvtIoRead&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541776)"> <em>EvtIoRead</em> </a>コールバック関数では、メモリの記述子のリスト (取得 MDL) オブジェクトは、I/O 要求が完了した後にアクセスできません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-mdlafterreqcompletedreada.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedReadA&lt;/strong&gt;](kmdf-mdlafterreqcompletedreada.md)"><strong>MdlAfterReqCompletedReadA</strong></a></p></td>
<td align="left"><p><a href="kmdf-mdlafterreqcompletedreada.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedReadA&lt;/strong&gt;](kmdf-mdlafterreqcompletedreada.md)"> <strong>MdlAfterReqCompletedReadA</strong> </a>ルールでは、ことを指定します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff541776" data-raw-source="[&lt;em&gt;EvtIoRead&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541776)"> <em>EvtIoRead</em> </a>コールバック関数では、メモリの記述子のリスト (取得 MDL) オブジェクトは、I/O 要求が完了した後にアクセスできません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-mdlafterreqcompletedwrite.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedWrite&lt;/strong&gt;](kmdf-mdlafterreqcompletedwrite.md)"><strong>MdlAfterReqCompletedWrite</strong></a></p></td>
<td align="left"><p><a href="kmdf-mdlafterreqcompletedwrite.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedWrite&lt;/strong&gt;](kmdf-mdlafterreqcompletedwrite.md)"> <strong>MdlAfterReqCompletedWrite</strong> </a>ルールでは、ことを指定します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff541813" data-raw-source="[&lt;em&gt;EvtIoWrite&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541813)"> <em>EvtIoWrite</em> </a>コールバック関数、メモリの記述子のリスト取得 (MDL) オブジェクトは、I/O 要求が完了した後にアクセスできません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-mdlafterreqcompletedwritea.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedWriteA&lt;/strong&gt;](kmdf-mdlafterreqcompletedwritea.md)"><strong>MdlAfterReqCompletedWriteA</strong></a></p></td>
<td align="left"><p><a href="kmdf-mdlafterreqcompletedwritea.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedWriteA&lt;/strong&gt;](kmdf-mdlafterreqcompletedwritea.md)"> <strong>MdlAfterReqCompletedWriteA</strong> </a>ルールでは、ことを指定します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff541813" data-raw-source="[&lt;em&gt;EvtIoWrite&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541813)"> <em>EvtIoWrite</em> </a>コールバック関数では、メモリ記述子I/O 要求が完了した後、取得したオブジェクトの一覧 (MDL) はアクセスできません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-memafterreqcompletedintioctl.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIntIoctl&lt;/strong&gt;](kmdf-memafterreqcompletedintioctl.md)"><strong>MemAfterReqCompletedIntIoctl</strong></a></p></td>
<td align="left"><p><a href="kmdf-memafterreqcompletedintioctl.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIntIoctl&lt;/strong&gt;](kmdf-memafterreqcompletedintioctl.md)"> <strong>MemAfterReqCompletedIntIoctl</strong> </a>ルールでは、ことを指定します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff541768" data-raw-source="[&lt;em&gt;EvtIoInternalDeviceControl&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541768)"> <em>EvtIoInternalDeviceControl</em> </a>コールバック関数、framework メモリ オブジェクトは、I/O 要求が完了した後にアクセスできません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-memafterreqcompletedintioctla.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIntIoctlA&lt;/strong&gt;](kmdf-memafterreqcompletedintioctla.md)"><strong>MemAfterReqCompletedIntIoctlA</strong></a></p></td>
<td align="left"><p><a href="kmdf-memafterreqcompletedintioctla.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIntIoctlA&lt;/strong&gt;](kmdf-memafterreqcompletedintioctla.md)"> <strong>MemAfterReqCompletedIntIoctlA</strong> </a>ルールでは、ことを指定します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff541768" data-raw-source="[&lt;em&gt;EvtIoInternalDeviceControl&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541768)"> <em>EvtIoInternalDeviceControl</em> </a>コールバック関数、framework メモリ オブジェクトは、I/O 要求が完了した後にアクセスできません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-memafterreqcompletedioctl.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIoctl&lt;/strong&gt;](kmdf-memafterreqcompletedioctl.md)"><strong>MemAfterReqCompletedIoctl</strong></a></p></td>
<td align="left"><p><a href="kmdf-memafterreqcompletedioctl.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIoctl&lt;/strong&gt;](kmdf-memafterreqcompletedioctl.md)"> <strong>MemAfterReqCompletedIoctl</strong> </a>ルールでは、ことを指定します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff541758" data-raw-source="[&lt;em&gt;EvtIoDeviceControl&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541758)"> <em>EvtIoDeviceControl</em> </a>コールバック関数では、フレームワークメモリ オブジェクトは、I/O 要求が完了した後にアクセスできません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-memafterreqcompletedioctla.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIoctlA&lt;/strong&gt;](kmdf-memafterreqcompletedioctla.md)"><strong>MemAfterReqCompletedIoctlA</strong></a></p></td>
<td align="left"><p><a href="kmdf-memafterreqcompletedioctla.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIoctlA&lt;/strong&gt;](kmdf-memafterreqcompletedioctla.md)"> <strong>MemAfterReqCompletedIoctlA</strong> </a>ルールでは、ことを指定します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff541758" data-raw-source="[&lt;em&gt;EvtIoDeviceControl&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541758)"> <em>EvtIoDeviceControl</em> </a>コールバック関数では、フレームワークメモリ オブジェクトは、I/O 要求が完了した後にアクセスできません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-memafterreqcompletedread.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedRead&lt;/strong&gt;](kmdf-memafterreqcompletedread.md)"><strong>MemAfterReqCompletedRead</strong></a></p></td>
<td align="left"><p><a href="kmdf-memafterreqcompletedread.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedRead&lt;/strong&gt;](kmdf-memafterreqcompletedread.md)"> <strong>MemAfterReqCompletedRead</strong> </a>ルールでは、ことを指定します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff541776" data-raw-source="[&lt;em&gt;EvtIoRead&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541776)"> <em>EvtIoRead</em> </a> framework のメモリ オブジェクトを使用してコールバック関数I/O 要求が完了した後にアクセスできません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-memafterreqcompletedreada.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedReadA&lt;/strong&gt;](kmdf-memafterreqcompletedreada.md)"><strong>MemAfterReqCompletedReadA</strong></a></p></td>
<td align="left"><p><a href="kmdf-memafterreqcompletedreada.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedReadA&lt;/strong&gt;](kmdf-memafterreqcompletedreada.md)"> <strong>MemAfterReqCompletedReadA</strong> </a>ルールでは、ことを指定します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff541776" data-raw-source="[&lt;em&gt;EvtIoRead&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541776)"> <em>EvtIoRead</em> </a> framework のメモリ オブジェクトを使用してコールバック関数I/O 要求が完了した後にアクセスできません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-memafterreqcompletedwrite.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedWrite&lt;/strong&gt;](kmdf-memafterreqcompletedwrite.md)"><strong>MemAfterReqCompletedWrite</strong></a></p></td>
<td align="left"><p><a href="kmdf-memafterreqcompletedwrite.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedWrite&lt;/strong&gt;](kmdf-memafterreqcompletedwrite.md)"> <strong>MemAfterReqCompletedWrite</strong> </a>ルールでは、ことを指定します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff541813" data-raw-source="[&lt;em&gt;EvtIoWrite&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541813)"> <em>EvtIoWrite</em> </a>コールバック関数では、framework のメモリオブジェクトは、I/O 要求が完了した後にアクセスできません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-memafterreqcompletedwritea.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedWriteA&lt;/strong&gt;](kmdf-memafterreqcompletedwritea.md)"><strong>MemAfterReqCompletedWriteA</strong></a></p></td>
<td align="left"><p><a href="kmdf-memafterreqcompletedwritea.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedWriteA&lt;/strong&gt;](kmdf-memafterreqcompletedwritea.md)"> <strong>MemAfterReqCompletedWriteA</strong> </a>ルールでは、ことを指定します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff541813" data-raw-source="[&lt;em&gt;EvtIoWrite&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541813)"> <em>EvtIoWrite</em> </a>コールバック関数では、framework のメモリオブジェクトは、I/O 要求が完了した後にアクセスできません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="nullcheck.md" data-raw-source="[&lt;strong&gt;NullCheck&lt;/strong&gt;](nullcheck.md)"><strong>NullCheck</strong></a></p></td>
<td align="left"><p>NullCheck ルールは、ドライバーの後で、ドライバーのコード内の NULL 値が逆参照しないことを確認します。 このルールは、これらの条件のいずれかが true の場合、欠陥を報告します。</p>
<ul>
<li>以降は逆参照が NULL の代入です。</li>
<li>ドライバーでは、後で逆参照が NULL の可能性があるプロシージャにグローバル/パラメーターがあるし、ポインターの初期値は NULL である可能性がありますの候補を示す、ドライバーでの明示的なチェックがあります。</li>
</ul>
<p>NullCheck ルール違反では、最も関連のコード ステートメントは、トレースのツリー ペインで強調表示されます。 レポートの出力の使用方法の詳細については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/hardware/ff552834" data-raw-source="[Static Driver Verifier Report](https://msdn.microsoft.com/library/windows/hardware/ff552834)">静的ドライバー検証ツールのレポート</a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff554020" data-raw-source="[Understanding the Trace Viewer](https://msdn.microsoft.com/library/windows/hardware/ff554020)">トレース ビューアーを理解する</a>します。</p>
<p></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-pdodeviceinitapi.md" data-raw-source="[&lt;strong&gt;PdoDeviceInitAPI&lt;/strong&gt;](kmdf-pdodeviceinitapi.md)"><strong>PdoDeviceInitAPI</strong></a></p></td>
<td align="left"><p><a href="kmdf-pdodeviceinitapi.md" data-raw-source="[&lt;strong&gt;PdoDeviceInitAPI&lt;/strong&gt;](kmdf-pdodeviceinitapi.md)"> <strong>PdoDeviceInitAPI</strong> </a>ルールを指定する<a href="https://msdn.microsoft.com/library/windows/hardware/ff548786" data-raw-source="[&lt;strong&gt;WdfPdoInitAllocate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548786)"> <strong>WdfPdoInitAllocate</strong> </a>とすべての他のデバイス オブジェクトの初期化を設定する Ddi<a href="https://msdn.microsoft.com/library/windows/hardware/ff546951" data-raw-source="[&lt;strong&gt;WDFDEVICE_INIT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546951)"> <strong>WDFDEVICE_INIT</strong> </a>ドライバー呼び出しの前に、物理デバイス オブジェクト (PDO) を呼び出す必要がありますの構造体<a href="https://msdn.microsoft.com/library/windows/hardware/ff545926" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545926)"> <strong>WdfDeviceCreate</strong></a> pdo します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-pdoinitfreedevicecallback.md" data-raw-source="[&lt;strong&gt;PdoInitFreeDeviceCallback&lt;/strong&gt;](kmdf-pdoinitfreedevicecallback.md)"><strong>PdoInitFreeDeviceCallback</strong></a></p></td>
<td align="left"><p><a href="kmdf-pdoinitfreedevicecallback.md" data-raw-source="[&lt;strong&gt;PdoInitFreeDeviceCallback&lt;/strong&gt;](kmdf-pdoinitfreedevicecallback.md)"> <strong>PdoInitFreeDeviceCallback</strong> </a>ルールでは、ドライバーを呼び出す必要がありますを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff546050" data-raw-source="[&lt;strong&gt;WdfDeviceInitFree&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546050)"> <strong>WdfDeviceInitFree</strong> </a>場合は、エラーが発生したときに、ドライバーでは、すべて framework デバイス オブジェクトの初期化関数を呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-pdoinitfreedevicecreate.md" data-raw-source="[&lt;strong&gt;PdoInitFreeDeviceCreate&lt;/strong&gt;](kmdf-pdoinitfreedevicecreate.md)"><strong>PdoInitFreeDeviceCreate</strong></a></p></td>
<td align="left"><p><a href="kmdf-pdoinitfreedevicecreate.md" data-raw-source="[&lt;strong&gt;PdoInitFreeDeviceCreate&lt;/strong&gt;](kmdf-pdoinitfreedevicecreate.md)"> <strong>PdoInitFreeDeviceCreate</strong> </a>ルールでは、ドライバーを呼び出す必要がありますを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff546050" data-raw-source="[&lt;strong&gt;WdfDeviceInitFree&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546050)"> <strong>WdfDeviceInitFree</strong> </a>の代わりに<a href="https://msdn.microsoft.com/library/windows/hardware/ff545926" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545926)"><strong>WdfDeviceCreate</strong> </a>ドライバーへの呼び出しから WDFDEVICE_INIT 構造体を受信した場合、デバイス オブジェクトの初期化関数のいずれかでエラーが発生した場合と<a href="https://msdn.microsoft.com/library/windows/hardware/ff548786" data-raw-source="[&lt;strong&gt;WdfPdoInitAllocate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548786)"> <strong>WdfPdoInitAllocate</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-pdoinitfreedevicecreatetype2.md" data-raw-source="[&lt;strong&gt;PdoInitFreeDeviceCreateType2&lt;/strong&gt;](kmdf-pdoinitfreedevicecreatetype2.md)"><strong>PdoInitFreeDeviceCreateType2</strong></a></p></td>
<td align="left"><p>PdoInitFreeDeviceCreateType2 ルールでは、ドライバーを呼び出してはならないことを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff545926" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545926)"> <strong>WdfDeviceCreate</strong> </a>呼び出した後<a href="https://msdn.microsoft.com/library/windows/hardware/ff546050" data-raw-source="[&lt;strong&gt;WdfDeviceInitFree&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546050)"> <strong>WdfDeviceInitFree</strong> </a>.</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-pdoinitfreedevicecreatetype4.md" data-raw-source="[&lt;strong&gt;PdoInitFreeDeviceCreateType4&lt;/strong&gt;](kmdf-pdoinitfreedevicecreatetype4.md)"><strong>PdoInitFreeDeviceCreateType4</strong></a></p></td>
<td align="left"><p>PdoInitFreeDeviceCreateType4 ルールでは、ドライバーを呼び出す必要がありますを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff546050" data-raw-source="[&lt;strong&gt;WdfDeviceInitFree&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546050)"> <strong>WdfDeviceInitFree</strong> </a>ドライバーを呼び出すときにエラーが発生した場合<a href="https://msdn.microsoft.com/library/windows/hardware/ff545926" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545926)"> <strong>WdfDeviceCreate</strong></a>.</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-controldeviceinitallocate.md" data-raw-source="[&lt;strong&gt;ControlDeviceInitAllocate&lt;/strong&gt;](kmdf-controldeviceinitallocate.md)"><strong>ControlDeviceInitAllocate</strong></a></p></td>
<td align="left"><p><a href="kmdf-controldeviceinitallocate.md" data-raw-source="[&lt;strong&gt;ControlDeviceInitAllocate&lt;/strong&gt;](kmdf-controldeviceinitallocate.md)"> <strong>ControlDeviceInitAllocate</strong> </a>ルール呼び出すを指定すること、制御デバイス オブジェクトのドライバーする必要があります、framework デバイス オブジェクトの初期化メソッド<a href="https://msdn.microsoft.com/library/windows/hardware/ff545841" data-raw-source="[&lt;strong&gt;WdfControlDeviceInitAllocate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545841)"> <strong>WdfControlDeviceInitAllocate</strong> </a>ドライバー呼び出しの前に<a href="https://msdn.microsoft.com/library/windows/hardware/ff545926" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545926)"> <strong>WdfDeviceCreate</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-inputbufferapi.md" data-raw-source="[&lt;strong&gt;InputBufferAPI&lt;/strong&gt;](kmdf-inputbufferapi.md)"><strong>InputBufferAPI</strong></a></p></td>
<td align="left"><p><a href="kmdf-inputbufferapi.md" data-raw-source="[&lt;strong&gt;InputBufferAPI&lt;/strong&gt;](kmdf-inputbufferapi.md)"> <strong>InputBufferAPI</strong> </a>ルールでは、バッファー取得のための正しい Ddi で使用されることを指定します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff541776" data-raw-source="[&lt;em&gt;EvtIoRead&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541776)"> <em>EvtIoRead</em></a>コールバック関数。 内で、 <em>EvtIoRead</em>コールバック関数では、次の Ddi はバッファー取得のため呼び出すことができません。</p></td>
</tr>
</tbody>
</table>

 

**DDI 使用量のルールを選択するには、次のように設定します。**

1.  Microsoft Visual Studio で、ドライバーのプロジェクト (.vcxProj) を選択します。 **ドライバー**  メニューのをクリックして**Static Driver Verifier を起動しています**.

2.  をクリックして、**ルール**タブ。**規則セット**、 **DDIUsage**します。

    Visual Studio の開発者コマンド プロンプト ウィンドウから既定のルールを選択するには、次のように指定します。 **DDIUsage.sdv**で、 **/check**オプション。 以下に例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:DDIUsage.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、次を参照してください。[ドライバーで障害を検出する Static Driver Verifier を使用して](https://msdn.microsoft.com/library/windows/hardware/hh454281)と[Static Driver Verifier のコマンド (MSBuild)](https://msdn.microsoft.com/library/windows/hardware/hh466459)します。

 

 




