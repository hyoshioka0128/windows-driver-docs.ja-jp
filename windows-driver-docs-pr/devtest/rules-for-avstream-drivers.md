---
title: AVStream ドライバーの規則
description: AVStream ミニポートドライバーの DDI コンプライアンス規則は、カーネルストリーミングドライバー (ks) とそのミニポートドライバー間の DDI インターフェイスプロトコルを検証します。
ms.assetid: 0A104ADF-8607-4708-A0E3-1697F55B0CF5
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: fc5aceb51bb87258551155096a69bb6702ad5187
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840048"
---
# <a name="rules-for-avstream-drivers"></a>AVStream ドライバーの規則


AVStream ミニポートドライバーの DDI コンプライアンス規則は、カーネルストリーミングドライバー (ks) とそのミニポートドライバー間の DDI インターフェイスプロトコルを検証します。

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
<td align="left"><p><a href="ks-kscallbackreturn.md" data-raw-source="[&lt;strong&gt;KsCallbackReturn&lt;/strong&gt;](ks-kscallbackreturn.md)"><strong>KsCallbackReturn</strong></a></p></td>
<td align="left"><p>KsCallbackReturn ルールは、カーネルストリーミング (KS) ミニポートドライバーのコールバック関数が、許可されている状態値のみを返すことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ks-ksdevicemutex.md" data-raw-source="[&lt;strong&gt;KsDeviceMutex&lt;/strong&gt;](ks-ksdevicemutex.md)"><strong>KsDeviceMutex</strong></a></p></td>
<td align="left"><p><a href="ks-ksdevicemutex.md" data-raw-source="[&lt;strong&gt;KsDeviceMutex&lt;/strong&gt;](ks-ksdevicemutex.md)"><strong>KsDeviceMutex</strong></a>ルールは、カーネルストリーミングミニポートドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksacquiredevice" data-raw-source="[&lt;strong&gt;KsAcquireDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksacquiredevice)"><strong>KsAcquireDevice</strong></a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksreleasedevice" data-raw-source="[&lt;strong&gt;KsReleaseDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksreleasedevice)"><strong>ksreleasedevice</strong></a>を正しい順序で使用することを指定します。 つまり、 <strong>KsAcquireDevice</strong>を呼び出すたびに、対応する<strong>ksk releasedevice</strong>への呼び出しが必要になります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ks-ksfiltermutex.md" data-raw-source="[&lt;strong&gt;KsFilterMutex&lt;/strong&gt;](ks-ksfiltermutex.md)"><strong>KsFilterMutex</strong></a></p></td>
<td align="left"><p>KsFilterMutex ルールは、KS ミニポートドライバーがフィルターミューテックスを取得し、正しい順序で解放することを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ks-ksirqlddis.md" data-raw-source="[&lt;strong&gt;KsIrqlDDIs&lt;/strong&gt;](ks-ksirqlddis.md)"><strong>KsIrqlDDIs</strong></a></p></td>
<td align="left"><p>KsIrqlDDIs 規則は、カーネルストリーミング (KS) ミニポートドライバーが KS DDIs を正しい IRQL レベルで呼び出すことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ks-ksirqldevicecallbacks.md" data-raw-source="[&lt;strong&gt;KsIrqlDeviceCallbacks&lt;/strong&gt;](ks-ksirqldevicecallbacks.md)"><strong>KsIrqlDeviceCallbacks</strong></a></p></td>
<td align="left"><p>KsIrqlDeviceCallbacks ルールでは、カーネルストリーミング (KS) ミニポートドライバーが、呼び出されたときと同じ IRQL を持つ KS デバイスコールバック関数から返されることを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ks-ksirqlfiltercallbacks.md" data-raw-source="[&lt;strong&gt;KsIrqlFilterCallbacks&lt;/strong&gt;](ks-ksirqlfiltercallbacks.md)"><strong>KsIrqlFilterCallbacks バック</strong></a></p></td>
<td align="left"><p>KsIrqlFilterCallbacks 規則は、カーネルストリーミング (KS) ミニポートドライバーが、コールバック関数が呼び出されたときと同じ IRQL を持つ KS フィルターコールバック関数から戻ることを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ksmarkpendingirp.md" data-raw-source="[&lt;strong&gt;KsMarkPendingIrp&lt;/strong&gt;](ksmarkpendingirp.md)"><strong>KsMarkPendingIrp</strong></a></p></td>
<td align="left"><p>KsMarkPendingIrp 規則は、次のコールバック関数からありますを返した場合に、カーネルストリーム (KS) ミニポートドライバーが Irp を pending としてマークする必要があることを指定します。</p>
<ul>
<li>AVStrMiniFilterClose</li>
<li>AVStrMiniPinClose</li>
<li>AVStrMiniPinCreate</li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ks-ksirqlpincallbacks.md" data-raw-source="[&lt;strong&gt;KsIrqlPinCallbacks&lt;/strong&gt;](ks-ksirqlpincallbacks.md)"><strong>KsIrqlPinCallbacks バック</strong></a></p></td>
<td align="left"><p>KsIrqlPinCallbacks 規則は、カーネルストリーム (KS) ミニポートドライバーが、呼び出されたときと同じ IRQL を持つ KS ピンコールバック関数から戻ることを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ks-ksprocessingmutex.md" data-raw-source="[&lt;strong&gt;KsProcessingMutex&lt;/strong&gt;](ks-ksprocessingmutex.md)"><strong>KsProcessingMutex</strong></a></p></td>
<td align="left"><p>KsProcessingMutex ルールは、KS ミニポートドライバーが処理ミューテックスを正しい順序で使用することを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ks-ksstreampointerclone.md" data-raw-source="[&lt;strong&gt;KsStreamPointerClone&lt;/strong&gt;](ks-ksstreampointerclone.md)"><strong>Ksstreamポインターの複製</strong></a></p></td>
<td align="left"><p>Ksk Streamポインタの複製ルールは、カーネルストリーム (KS) ミニポートドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerclone" data-raw-source="[&lt;strong&gt;KsStreamPointerClone&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerclone)"><strong>Ksk Streamポインタ clone</strong></a>および<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerdelete" data-raw-source="[&lt;strong&gt;KsStreamPointerDelete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerdelete)"><strong>Ksstreamポインター delete</strong></a>関数を正しく使用することを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ks-ksstreampointerlock.md" data-raw-source="[&lt;strong&gt;KsStreamPointerLock&lt;/strong&gt;](ks-ksstreampointerlock.md)"><strong>KsStreamPointerLock ロック</strong></a></p></td>
<td align="left"><p>Ksk Streampounlock 規則は、カーネルストリーミング (KS) ミニポートドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerlock" data-raw-source="[&lt;strong&gt;KsStreamPointerLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerlock)"><strong>Ksk streampounlock</strong></a>関数および<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerunlock" data-raw-source="[&lt;strong&gt;KsStreamPointerUnlock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerunlock)"><strong>ksstreamポインターロック解除</strong></a>関数を正しい順序で使用することを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ks-ksstreampointerunlock.md" data-raw-source="[&lt;strong&gt;KsStreamPointerUnlock&lt;/strong&gt;](ks-ksstreampointerunlock.md)"><strong>Ksstreamポインターロック解除</strong></a></p></td>
<td align="left"><p>Ksk Streamポインタ Unlock 規則は、ドライバーがアンロードされる前 (またはデバイスが停止される前) に、カーネルストリーミング (KS) ミニポートドライバーがすべてのストリームポインターをロック解除することを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ks-kstimeddevicecallbacks.md" data-raw-source="[&lt;strong&gt;KsTimedDeviceCallbacks&lt;/strong&gt;](ks-kstimeddevicecallbacks.md)"><strong>KsTimedDeviceCallbacks</strong></a></p></td>
<td align="left"><p>KsTimedDeviceCallbacks ルールは、カーネルストリーミング (KS) ミニポートドライバーが500ミリ秒以内にデバイスコールバック関数から戻ることを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ks-kstimedfiltercallbacks.md" data-raw-source="[&lt;strong&gt;KsTimedFilterCallbacks&lt;/strong&gt;](ks-kstimedfiltercallbacks.md)"><strong>KsTimedFilterCallbacks</strong></a></p></td>
<td align="left"><p>KsTimedFilterCallbacks ルールは、カーネルストリーミング (KS) ミニポートドライバーが500ミリ秒以内にフィルターコールバック関数から戻ることを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ks-kstimedpincallbacks.md" data-raw-source="[&lt;strong&gt;KsTimedPinCallbacks&lt;/strong&gt;](ks-kstimedpincallbacks.md)"><strong>KsTimedPinCallbacks</strong></a></p></td>
<td align="left"><p>KsTimedPinCallbacks ルールは、カーネルストリーミング (KS) ミニポートドライバーが500ミリ秒以内に pin コールバック関数から戻ることを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ks-kstimedpinsetdevicestate.md" data-raw-source="[&lt;strong&gt;KsTimedPinSetDeviceState&lt;/strong&gt;](ks-kstimedpinsetdevicestate.md)"><strong>KsTimedPinSetDeviceState</strong></a></p></td>
<td align="left"><p>KsTimedPinSetDeviceState 規則は、avstream (KS) ミニポートドライバーが AVStream ミニドライバーの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdevicestate" data-raw-source="[&lt;em&gt;AVStrMiniPinSetDeviceState&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdevicestate)"><em>Avstrminipinsetdevicestate</em></a>ルーチンを使用して、必要な時間内に状態遷移を行うことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ks-kstimedprocessingmutex.md" data-raw-source="[&lt;strong&gt;KsTimedProcessingMutex&lt;/strong&gt;](ks-kstimedprocessingmutex.md)"><strong>KsTimedProcessingMutex</strong></a></p></td>
<td align="left"><p>KsTimedProcessingMutex ルールは、KS ミニポートドライバーが100ミリ秒を超える処理ミューテックスを保持しないことを指定します。</p></td>
</tr>
</tbody>
</table>

 

 

 





