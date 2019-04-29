---
title: ファイル システム オブジェクトのクエリと設定ルーチン
description: ファイル システム オブジェクトのクエリと設定ルーチン
ms.assetid: 34b97a6e-a155-443c-94dd-4d8f1fc4b430
keywords:
- ミニ リダイレクター WDK、クエリ操作
- ミニ リダイレクターの WDK セット操作
- クエリ操作 WDK ネットワーク リダイレクター
- セット操作 WDK ネットワーク リダイレクター
- ファイル オブジェクト WDK のミニ リダイレクター
- WDK のミニ リダイレクター オブジェクト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a85652432f7a6328ce169e8a0726bcfb4ce8d21d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383839"
---
# <a name="file-system-object-query-and-set-routines"></a>ファイル システム オブジェクトのクエリと設定ルーチン


さまざまなネットワークのミニ リダイレクターで実装できるルーチンでは、クエリはし、ファイルに対する操作のシステム オブジェクトを設定します。 RDBSS では、ほとんどのクエリまたはファイル オブジェクトの情報を設定する IRP を受信したときにこれらの呼び出しを発行します。 IRP RDBSS を受信して、MRx の間の直接的な対応関係があるクエリまたは RDBSS 呼び出す操作を設定します。

次の表では、ファイル システム オブジェクトのクエリに対して、ネットワーク ミニ リダイレクターによって実装され、セットの操作が可能なルーチンを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ルーチン</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550696" data-raw-source="[&lt;strong&gt;MRxIsValidDirectory&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550696)"><strong>MRxIsValidDirectory</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが、パスが有効なディレクトリを示すことを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550755" data-raw-source="[&lt;strong&gt;MRxQueryDirectory&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550755)"><strong>MRxQueryDirectory</strong></a></td>
<td align="left"><p>RDBSS は、ファイル ディレクトリのシステム オブジェクトでネットワークのミニ リダイレクター クエリ情報を要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550759" data-raw-source="[&lt;strong&gt;MRxQueryEaInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550759)"><strong>MRxQueryEaInfo</strong></a></td>
<td align="left"><p>RDBSS は、ネットワーク ミニリダイレクター クエリがファイル システム オブジェクトの属性情報を拡張することを要求するには、このルーチンを呼び出します。 RDBSS では、受信、IRP_MJ_QUERY_EA への応答には、この呼び出しを発行します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550770" data-raw-source="[&lt;strong&gt;MRxQueryFileInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550770)"><strong>MRxQueryFileInfo</strong></a></td>
<td align="left"><p>RDBSS は、ファイル システム オブジェクトでネットワーク ミニリダイレクター クエリ ファイルの情報を要求するには、このルーチンを呼び出します。 RDBSS では、受信、IRP_MJ_QUERY_INFORMATION への応答には、この呼び出しを発行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550773" data-raw-source="[&lt;strong&gt;MRxQueryQuotaInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550773)"><strong>MRxQueryQuotaInfo</strong></a></td>
<td align="left"><p>RDBSS は、ファイル システム オブジェクトでネットワーク ミニリダイレクター クエリのクォータ情報を要求するには、このルーチンを呼び出します。 RDBSS では、受信、IRP_MJ_QUERY_QUOTA への応答には、この呼び出しを発行します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550776" data-raw-source="[&lt;strong&gt;MRxQuerySdInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550776)"><strong>MRxQuerySdInfo</strong></a></td>
<td align="left"><p>RDBSS は、ファイル システム オブジェクトでネットワーク ミニリダイレクター クエリ セキュリティ記述子の情報を要求するには、このルーチンを呼び出します。 RDBSS では、受信、IRP_MJ_QUERY_SECURITY への応答には、この呼び出しを発行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550782" data-raw-source="[&lt;strong&gt;MRxQueryVolumeInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550782)"><strong>MRxQueryVolumeInfo</strong></a></td>
<td align="left"><p>RDBSS は、ネットワーク ミニリダイレクター クエリのボリューム情報を要求するには、このルーチンを呼び出します。 RDBSS では、受信、IRP_MJ_QUERY_VOLUME_INFORMATION への応答には、この呼び出しを発行します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550786" data-raw-source="[&lt;strong&gt;MRxSetEaInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550786)"><strong>MRxSetEaInfo</strong></a></td>
<td align="left"><p>RDBSS は、ネットワーク ミニ リダイレクターのセットがファイル システム オブジェクトの属性情報を拡張することを要求するには、このルーチンを呼び出します。 RDBSS では、受信、IRP_MJ_SET_EA への応答には、この呼び出しを発行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550790" data-raw-source="[&lt;strong&gt;MRxSetFileInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550790)"><strong>MRxSetFileInfo</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターがファイル システム オブジェクトでファイルの情報を設定することを要求するには、このルーチンを呼び出します。 RDBSS では、受信、IRP_MJ_SET_INFORMATION への応答には、この呼び出しを発行します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550796" data-raw-source="[&lt;strong&gt;MRxSetFileInfoAtCleanup&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550796)"><strong>MRxSetFileInfoAtCleanup</strong></a></td>
<td align="left"><p>RDBSS cleanup ファイル システム オブジェクトのファイル情報を設定する、ネットワーク ミニ リダイレクターを要求するには、このルーチンを呼び出します。 RDBSS は、アプリケーションがハンドルを閉じるときにクリーンアップが終了する前に、この呼び出しを発行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550800" data-raw-source="[&lt;strong&gt;MRxSetQuotaInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550800)"><strong>MRxSetQuotaInfo</strong></a></td>
<td align="left"><p>RDBSS は、ネットワーク ミニ リダイレクターがファイル システム オブジェクトのクォータ情報を設定することを要求するには、このルーチンを呼び出します。 RDBSS では、受信、IRP_MJ_SET_QUOTA への応答には、この呼び出しを発行します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550805" data-raw-source="[&lt;strong&gt;MRxSetSdInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550805)"><strong>MRxSetSdInfo</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターがファイル システム オブジェクトのセキュリティ記述子の情報を設定することを要求するには、このルーチンを呼び出します。 RDBSS では、受信、IRP_MJ_SET_SECURITY への応答には、この呼び出しを発行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550810" data-raw-source="[&lt;strong&gt;MRxSetVolumeInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550810)"><strong>MRxSetVolumeInfo</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターがボリューム情報を設定することを要求するには、このルーチンを呼び出します。 RDBSS では、受信、IRP_MJ_SET_VOLUME_INFORMATION への応答には、この呼び出しを発行します。</p></td>
</tr>
</tbody>
</table>

 

 

 




