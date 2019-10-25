---
title: WSK_SET_STATIC_EVENT_CALLBACKS
description: WSK_SET_STATIC_EVENT_CALLBACKS
ms.assetid: fa95bc7d-c7b2-4cca-a419-ef5eb2520976
ms.date: 07/18/2017
keywords:
- WSK_SET_STATIC_EVENT_CALLBACKS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: ccb6ddd44f591b5611715b5076c14d0e20d088f9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844425"
---
# <a name="wsk_set_static_event_callbacks"></a>WSK\_静的\_イベント\_コールバック\_設定する


WSK アプリケーションでは、WSK\_SET\_STATIC\_EVENT\_callback クライアントコントロール操作を使用して、作成するすべてのソケットで特定のイベントコールバック関数を自動的に有効にします。 この方法で有効になっているイベントコールバック関数は常に有効になり、後で WSK アプリケーションで無効にしたり再度有効にしたりすることはできません。 ただし、WSK アプリケーションで、作成されるすべてのソケットで特定のイベントコールバック関数が常に有効になっている場合、アプリケーションはこのメソッドを使用して、これらのイベントコールバック関数を自動的に有効にする必要があります。これにより、パフォーマンスが大幅に向上します。

WSK アプリケーションが WSK\_使用して\_静的\_イベント\_コールバッククライアントコントロール操作を使用する場合は、ソケットを作成する前に、これを行う必要があります。

作成されるすべてのソケットで特定のイベントコールバック関数を自動的に有効にするために、WSK アプリケーションは次のパラメーターを使用して[**Wskcontrolclient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_client)関数を呼び出します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ControlCode</em></p></td>
<td><p>WSK_SET_STATIC_EVENT_CALLBACKS</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof (WSK_EVENT_CALLBACK_CONTROL)</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>自動的に有効にする目的のイベントコールバック関数を指定する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_event_callback_control" data-raw-source="[&lt;strong&gt;WSK_EVENT_CALLBACK_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_event_callback_control)"><strong>WSK_EVENT_CALLBACK_CONTROL</strong></a>構造体へのポインター。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p><strong>空白</strong></p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p><strong>空白</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>Irp</em></p></td>
<td><p><strong>空白</strong></p></td>
</tr>
</tbody>
</table>

WSK アプリケーションでは、 [**wsk\_イベント\_コールバック\_制御**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_event_callback_control)構造の**eventmask**メンバー内のさまざまな種類のソケットに対して、イベントフラグの組み合わせを指定できます。 WSK アプリケーションが新しいソケットを作成すると、wsk サブシステムによって、作成されている WSK ソケットの特定の[カテゴリ](https://docs.microsoft.com/windows-hardware/drivers/network/winsock-kernel-socket-categories)に対して適切なイベントコールバック関数が自動的に有効になります。

標準 WSK イベントコールバック関数のイベントフラグの詳細については、「 [ **\_wsk\_イベント\_コールバック**](so-wsk-event-callback.md)」を参照してください。

ソケットのイベントコールバック関数の有効化と無効化の詳細については、「[イベントコールバック関数の有効化と無効化](https://docs.microsoft.com/windows-hardware/drivers/network/enabling-and-disabling-event-callback-functions)」を参照してください。

このクライアントコントロール操作では、 *Irp*パラメーターは**NULL**である必要があります。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows Vista 以降のバージョンの Windows オペレーティングシステムで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wsk .h (Wsk .h を含む)</td>
</tr>
</tbody>
</table>

 

 




