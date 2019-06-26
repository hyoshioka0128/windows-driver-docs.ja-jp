---
title: AVStream ドライバーの規則
description: AVStream ミニポート ドライバーの DDI 準拠規則は、カーネル ストリーミング ドライバー (ks.sys) とそのミニポート ドライバー間 DDI インターフェイス プロトコルを確認します。
ms.assetid: 0A104ADF-8607-4708-A0E3-1697F55B0CF5
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 07f8405af25de54c30eb31f296c47def2ca1cf88
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353871"
---
# <a name="rules-for-avstream-drivers"></a>AVStream ドライバーの規則


AVStream ミニポート ドライバーの DDI 準拠規則は、カーネル ストリーミング ドライバー (ks.sys) とそのミニポート ドライバー間 DDI インターフェイス プロトコルを確認します。

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
<td align="left"><p>KsCallbackReturn ルールでは、カーネル ストリーミング (KS) ミニポート ドライバー コールバック関数が許可される状態値のみを返すことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ks-ksdevicemutex.md" data-raw-source="[&lt;strong&gt;KsDeviceMutex&lt;/strong&gt;](ks-ksdevicemutex.md)"><strong>KsDeviceMutex</strong></a></p></td>
<td align="left"><p><a href="ks-ksdevicemutex.md" data-raw-source="[&lt;strong&gt;KsDeviceMutex&lt;/strong&gt;](ks-ksdevicemutex.md)"> <strong>KsDeviceMutex</strong> </a>ルールでは、ミニポート ドライバーをストリーミング カーネルが使用するように指定<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksacquiredevice" data-raw-source="[&lt;strong&gt;KsAcquireDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksacquiredevice)"> <strong>KsAcquireDevice</strong> </a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksreleasedevice" data-raw-source="[&lt;strong&gt;KsReleaseDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksreleasedevice)"><strong>KsReleaseDevice</strong> </a>正しい順序で。 すべての呼び出しには、 <strong>KsAcquireDevice</strong>に対応する呼び出しがあります。 <strong>KsReleaseDevice</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ks-ksfiltermutex.md" data-raw-source="[&lt;strong&gt;KsFilterMutex&lt;/strong&gt;](ks-ksfiltermutex.md)"><strong>KsFilterMutex</strong></a></p></td>
<td align="left"><p>KsFilterMutex ルールでは、KS ミニポート ドライバーが取得し、正しい順序でフィルター ミュー テックスを解放を指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ks-ksirqlddis.md" data-raw-source="[&lt;strong&gt;KsIrqlDDIs&lt;/strong&gt;](ks-ksirqlddis.md)"><strong>KsIrqlDDIs</strong></a></p></td>
<td align="left"><p>KsIrqlDDIs ルールは、カーネル ストリーミング (KS) ミニポート ドライバーを呼び出す KS Ddi 適切な IRQL でレベルを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ks-ksirqldevicecallbacks.md" data-raw-source="[&lt;strong&gt;KsIrqlDeviceCallbacks&lt;/strong&gt;](ks-ksirqldevicecallbacks.md)"><strong>KsIrqlDeviceCallbacks</strong></a></p></td>
<td align="left"><p>KsIrqlDeviceCallbacks ルールでは、カーネル ストリーミング (KS) ミニポート ドライバーが呼び出された時と同じ IRQL で KS デバイス コールバック関数から返すことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ks-ksirqlfiltercallbacks.md" data-raw-source="[&lt;strong&gt;KsIrqlFilterCallbacks&lt;/strong&gt;](ks-ksirqlfiltercallbacks.md)"><strong>KsIrqlFilterCallbacks</strong></a></p></td>
<td align="left"><p>KsIrqlFilterCallbacks ルールでは、カーネル ストリーミング (KS) ミニポート ドライバーがコールバック関数が呼び出された時と同じ IRQL で KS フィルターのコールバック関数から返すことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ksmarkpendingirp.md" data-raw-source="[&lt;strong&gt;KsMarkPendingIrp&lt;/strong&gt;](ksmarkpendingirp.md)"><strong>KsMarkPendingIrp</strong></a></p></td>
<td align="left"><p>KsMarkPendingIrp ルールでは、次のコールバック関数から STATUS_PENDING を返すときに、カーネル ストリーム (KS) ミニポート ドライバーに保留中として Irp をマークする必要がありますを指定します。</p>
<ul>
<li>AVStrMiniFilterClose</li>
<li>AVStrMiniPinClose</li>
<li>AVStrMiniPinCreate</li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ks-ksirqlpincallbacks.md" data-raw-source="[&lt;strong&gt;KsIrqlPinCallbacks&lt;/strong&gt;](ks-ksirqlpincallbacks.md)"><strong>KsIrqlPinCallbacks</strong></a></p></td>
<td align="left"><p>KsIrqlPinCallbacks ルールでは、カーネル ストリーム (KS) ミニポート ドライバーが呼び出された時と同じ IRQL で KS Pin コールバック関数から返すことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ks-ksprocessingmutex.md" data-raw-source="[&lt;strong&gt;KsProcessingMutex&lt;/strong&gt;](ks-ksprocessingmutex.md)"><strong>KsProcessingMutex</strong></a></p></td>
<td align="left"><p>KsProcessingMutex ルールでは、KS ミニポート ドライバーが、正しい順序で処理ミュー テックスを使用することを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ks-ksstreampointerclone.md" data-raw-source="[&lt;strong&gt;KsStreamPointerClone&lt;/strong&gt;](ks-ksstreampointerclone.md)"><strong>KsStreamPointerClone</strong></a></p></td>
<td align="left"><p>KsStreamPointerClone ルールでは、カーネル ストリーム (KS) ミニポート ドライバーが正しく使用を指定します、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerclone" data-raw-source="[&lt;strong&gt;KsStreamPointerClone&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerclone)"> <strong>KsStreamPointerClone</strong> </a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerdelete" data-raw-source="[&lt;strong&gt;KsStreamPointerDelete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerdelete)"> <strong>KsStreamPointerDelete</strong></a>関数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ks-ksstreampointerlock.md" data-raw-source="[&lt;strong&gt;KsStreamPointerLock&lt;/strong&gt;](ks-ksstreampointerlock.md)"><strong>KsStreamPointerLock</strong></a></p></td>
<td align="left"><p>KsStreamPointerLock ルールでは、カーネル ストリーミング (KS) ミニポート ドライバーが使用するように指定、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerlock" data-raw-source="[&lt;strong&gt;KsStreamPointerLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerlock)"> <strong>KsStreamPointerLock</strong> </a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerunlock" data-raw-source="[&lt;strong&gt;KsStreamPointerUnlock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerunlock)"> <strong>KsStreamPointerUnlock</strong></a>正しいシーケンスで機能します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ks-ksstreampointerunlock.md" data-raw-source="[&lt;strong&gt;KsStreamPointerUnlock&lt;/strong&gt;](ks-ksstreampointerunlock.md)"><strong>KsStreamPointerUnlock</strong></a></p></td>
<td align="left"><p>KsStreamPointerUnlock ルールでは、ドライバーが読み込まれていない (またはデバイスを停止) する前に、カーネル ストリーミング (KS) ミニポート ドライバーはすべてのストリーム ポインターをロック解除。 を指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ks-kstimeddevicecallbacks.md" data-raw-source="[&lt;strong&gt;KsTimedDeviceCallbacks&lt;/strong&gt;](ks-kstimeddevicecallbacks.md)"><strong>KsTimedDeviceCallbacks</strong></a></p></td>
<td align="left"><p>KsTimedDeviceCallbacks ルールでは、カーネル ストリーミング (KS) ミニポート ドライバーが 500 ミリ秒以内でデバイスのコールバック関数から返すことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ks-kstimedfiltercallbacks.md" data-raw-source="[&lt;strong&gt;KsTimedFilterCallbacks&lt;/strong&gt;](ks-kstimedfiltercallbacks.md)"><strong>KsTimedFilterCallbacks</strong></a></p></td>
<td align="left"><p>KsTimedFilterCallbacks ルールでは、カーネル ストリーミング (KS) ミニポート ドライバーが 500 ミリ秒以内で、フィルターのコールバック関数から返すことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ks-kstimedpincallbacks.md" data-raw-source="[&lt;strong&gt;KsTimedPinCallbacks&lt;/strong&gt;](ks-kstimedpincallbacks.md)"><strong>KsTimedPinCallbacks</strong></a></p></td>
<td align="left"><p>KsTimedPinCallbacks ルールでは、カーネル ストリーミング (KS) ミニポート ドライバーが 500 ミリ秒以内でピン留めするコールバック関数から返すことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ks-kstimedpinsetdevicestate.md" data-raw-source="[&lt;strong&gt;KsTimedPinSetDeviceState&lt;/strong&gt;](ks-kstimedpinsetdevicestate.md)"><strong>KsTimedPinSetDeviceState</strong></a></p></td>
<td align="left"><p>KsTimedPinSetDeviceState ルールでは、AVStream (KS) ミニポート ドライバー、AVStream ミニドライバーを使用して、状態遷移することを指定します<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnkspinsetdevicestate" data-raw-source="[&lt;em&gt;AVStrMiniPinSetDeviceState&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnkspinsetdevicestate)"> <em>AVStrMiniPinSetDeviceState</em> </a>ルーチン内で、必要な時間。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ks-kstimedprocessingmutex.md" data-raw-source="[&lt;strong&gt;KsTimedProcessingMutex&lt;/strong&gt;](ks-kstimedprocessingmutex.md)"><strong>KsTimedProcessingMutex</strong></a></p></td>
<td align="left"><p>KsTimedProcessingMutex ルールでは、KS ミニポート ドライバーでは、100 を超えるミリ秒間処理ミュー テックスは保持しないようにすることを指定します。</p></td>
</tr>
</tbody>
</table>

 

 

 





