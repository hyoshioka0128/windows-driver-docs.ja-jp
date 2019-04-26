---
title: WSK_SET_STATIC_EVENT_CALLBACKS
description: WSK_SET_STATIC_EVENT_CALLBACKS
ms.assetid: fa95bc7d-c7b2-4cca-a419-ef5eb2520976
ms.date: 07/18/2017
keywords:
- WSK_SET_STATIC_EVENT_CALLBACKS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 19bee586264f06c08e2f8d8831d88ad743b4d2a5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356776"
---
# <a name="wsksetstaticeventcallbacks"></a>WSK\_設定\_静的\_イベント\_コールバック


WSK アプリケーションの使用、WSK\_設定\_静的\_イベント\_自動的に作成したすべてのソケットでの特定のイベント コールバック関数を有効にするクライアント管理操作をコールバックします。 この方法で有効になっているイベントのコールバック関数は常に有効になっていると、無効になっているまたは WSK アプリケーションを後で再度有効にすることはできません。 ただし、この WSK アプリケーションは常に、特定のイベント コールバック関数で作成されたすべてのソケットでは可能である場合、アプリケーションは優れたパフォーマンスが生成されますので、これらのイベントのコールバック関数を自動的に有効にするこのメソッドを使用する必要があります。

WSK アプリケーション、WSK を使用している場合\_設定\_静的\_イベント\_コールバック クライアント コントロールの操作が行う必要があります、ソケットを作成する前にします。

WSK アプリケーションを呼び出す特定イベントのコールバック関数のすべてのソケットが作成されますを自動的に有効にする、 [ **WskControlClient** ](https://msdn.microsoft.com/library/windows/hardware/ff571126)関数は次のパラメーター。

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
<td><p>sizeof(WSK_EVENT_CALLBACK_CONTROL)</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>ポインターを<a href="https://msdn.microsoft.com/library/windows/hardware/ff571166" data-raw-source="[&lt;strong&gt;WSK_EVENT_CALLBACK_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571166)"> <strong>WSK_EVENT_CALLBACK_CONTROL</strong> </a>を自動的に有効にする目的のイベントのコールバック関数を指定する構造体</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>Irp</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
</tbody>
</table>

WSK アプリケーションのさまざまなソケットの種類についてイベント フラグの組み合わせを指定できます、**使う**のメンバー、 [ **WSK\_イベント\_コールバック\_コントロール** ](https://msdn.microsoft.com/library/windows/hardware/ff571166)構造体。 WSK サブシステムで、特定の適切なイベントのコールバック関数が自動的に有効に WSK アプリケーションでは、新しいソケットを作成するとき[カテゴリ](https://msdn.microsoft.com/library/windows/hardware/ff571093)WSK ソケットが作成されるのです。

標準的な WSK イベントのコールバック関数のイベント フラグの詳細については、次を参照してください。 [**ように\_WSK\_イベント\_コールバック**](so-wsk-event-callback.md)します。

有効にして、ソケットのイベントのコールバック関数を無効化の詳細については、次を参照してください。[の有効化と無効にするとイベントのコールバック関数](https://msdn.microsoft.com/library/windows/hardware/ff548851)します。

*Irp*パラメーターである必要があります**NULL**このクライアントのコントロールの操作。

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
<td><p>Windows Vista および Windows オペレーティング システムの以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wsk.h (Wsk.h を含む)</td>
</tr>
</tbody>
</table>

 

 




