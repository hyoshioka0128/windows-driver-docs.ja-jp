---
title: SO_WSK_SECURITY
description: SO_WSK_SECURITY
ms.assetid: 169680ba-6486-48fe-89d7-dcd4e5930605
ms.date: 07/18/2017
keywords:
- SO_WSK_SECURITY ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 49658a55beabad6539913604a6ccdc5a2f425d8f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331225"
---
# <a name="sowsksecurity"></a>したがって\_WSK\_セキュリティ


SO\_WSK\_セキュリティ ソケット オプションにより、WSK アプリケーションをソケットにセキュリティ記述子を適用またはソケットからソケットのセキュリティ記述子のキャッシュされたコピーを取得します。 セキュリティ記述子は、ソケットがバインドされているローカル トランスポート アドレスの共有を制御します。

このソケット オプションは、リッスンしているソケット、データグラム ソケットでは、接続指向のソケットにのみ適用されます。

WSK アプリケーションでは、ソケットにセキュリティ記述子を適用するこのソケット オプションを使用している場合、ソケットがローカル トランスポート アドレスにバインドする前にする必要があります。

WSK アプリケーションの呼び出しにソケットをセキュリティ記述子を適用する、 [ **WskControlSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571127)関数は次のパラメーター。

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
<td><p><em>RequestType</em></p></td>
<td><p><strong>WskSetOption</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SO_WSK_SECURITY</p></td>
</tr>
<tr class="odd">
<td><p><em>Level</em></p></td>
<td><p>取得</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof(PSECURITY_DESCRIPTOR)</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>PSECURITY_DESCRIPTOR に型指定された変数へのポインター。 この変数は、呼び出すことによって取得されたセキュリティ記述子のキャッシュされたコピーへのポインターを含める必要があります、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff571126" data-raw-source="[&lt;strong&gt;WskControlClient&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571126)"> <strong>WskControlClient</strong> </a>関数と、 <a href="wsk-cache-sd.md" data-raw-source="[&lt;strong&gt;WSK_CACHE_SD&lt;/strong&gt;](wsk-cache-sd.md)"> <strong>WSK_CACHE_SD</strong> </a>コードを制御します。</p></td>
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
</tbody>
</table>

呼び出すときに、WSK アプリケーションは IRP へのポインターを指定する必要があります、 **WskControlSocket**ソケットにセキュリティ記述子を適用する関数。

WSK アプリケーションでは、ソケットにセキュリティ記述子を適用するこのソケット オプションを使用している場合、新しいセキュリティ記述子には、ソケットに適用していた任意のセキュリティ記述子が置き換えられます。

IRP が完了した後、WSK アプリケーションはまでセキュリティ記述子のキャッシュされたコピーを解放できませんする必要があります。

WSK アプリケーションは、また、ソケットがセキュリティ記述子のキャッシュされたコピーへのポインターを指定することによって最初に作成されたときにソケットにセキュリティ記述子を適用できます、 *SecurityDescriptor*パラメーター、を呼び出すときに[ **WskSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571149)または[ **WskSocketConnect** ](https://msdn.microsoft.com/library/windows/hardware/ff571150)関数。

WSK アプリケーションでソケットにセキュリティ記述子が適用されない場合、WSK サブシステムは、ローカル トランスポート アドレスの共有を許可しない既定のセキュリティ記述子を使用します。

ソケットのセキュリティ記述子のキャッシュされたコピー ソケットからを取得する WSK アプリケーションが呼び出す、 [ **WskControlSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571127)関数は次のパラメーター。

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
<td><p><em>RequestType</em></p></td>
<td><p><strong>WskGetOption</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SO_WSK_SECURITY</p></td>
</tr>
<tr class="odd">
<td><p><em>Level</em></p></td>
<td><p>取得</p></td>
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
<td><p>sizeof(PSECURITY_DESCRIPTOR)</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>PSECURITY_DESCRIPTOR に型指定された変数へのポインター。 この変数は、ソケットのセキュリティ記述子のキャッシュされたコピーへのポインターを受け取ります。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>

呼び出すときに、WSK アプリケーションは IRP へのポインターを指定する必要があります、 **WskControlSocket**ソケットからソケットのセキュリティ記述子のキャッシュされたコピーを取得します。

WSK アプリケーションを呼び出す必要があります、 [ **WskControlClient** ](https://msdn.microsoft.com/library/windows/hardware/ff571126)関数と、 [ **WSK\_リリース\_SD** ](wsk-release-sd.md)不要になったときに、セキュリティ記述子のキャッシュされたコピーを解放するコードを制御します。

セキュリティの詳細については\_記述子構造体をセキュリティのリファレンス ページを参照してください\_Microsoft Windows SDK ドキュメントの記述子。

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

 

 




