---
title: WSK_TRANSPORT_LIST_CHANGE
description: WSK_TRANSPORT_LIST_CHANGE
ms.assetid: 3b12d692-467c-4d31-bd2a-bb6e34d87fde
ms.date: 07/18/2017
keywords:
- WSK_TRANSPORT_LIST_CHANGE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 1f5a9e6657e6d1d4d58956ad99695e0da5370bb8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539542"
---
# <a name="wsktransportlistchange"></a>WSK\_トランスポート\_一覧\_変更


WSK アプリケーションの使用、WSK\_トランスポート\_一覧\_使用可能なネットワークの一覧の変更を転送する場合に通知を受信するクライアント管理操作を変更します。

使用可能なネットワークの一覧が変更を転送するときの通知を受信する WSK アプリケーションが呼び出す、 [ **WskControlClient** ](https://msdn.microsoft.com/library/windows/hardware/ff571126)関数は次のパラメーター。

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
<td><p>WSK_TRANSPORT_LIST_CHANGE</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>NULL</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>NULL</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
<tr class="odd">
<td><p><em>Irp</em></p></td>
<td><p>使用可能なネットワークの一覧が変更を転送するまで、WSK サブシステムによってキューにある IRP へのポインター。 新しいネットワーク トランスポートを追加するか、既存のネットワーク トランスポートを削除した後、WSK サブシステムは IRP を完了します。</p></td>
</tr>
</tbody>
</table>

IRP では、このクライアントの管理操作に必要です。

WSK サブシステムが保留中の取り消し Irp WSK アプリケーションから呼び出す場合[ **WskDeregister** ](https://msdn.microsoft.com/library/windows/hardware/ff571128) WSK サブシステムから自体をデタッチします。

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

 

 




