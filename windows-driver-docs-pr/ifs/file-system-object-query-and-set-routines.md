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
ms.openlocfilehash: 4316ed469efe2a27c85b76faf6c436119312a224
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369268"
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
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_chkdir_calldown" data-raw-source="[&lt;strong&gt;MRxIsValidDirectory&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_chkdir_calldown)"><strong>MRxIsValidDirectory</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが、パスが有効なディレクトリを示すことを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxquerydirectory" data-raw-source="[&lt;strong&gt;MRxQueryDirectory&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxquerydirectory)"><strong>MRxQueryDirectory</strong></a></td>
<td align="left"><p>RDBSS は、ファイル ディレクトリのシステム オブジェクトでネットワークのミニ リダイレクター クエリ情報を要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxqueryeainfo" data-raw-source="[&lt;strong&gt;MRxQueryEaInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxqueryeainfo)"><strong>MRxQueryEaInfo</strong></a></td>
<td align="left"><p>RDBSS は、ネットワーク ミニリダイレクター クエリがファイル システム オブジェクトの属性情報を拡張することを要求するには、このルーチンを呼び出します。 RDBSS では、受信、IRP_MJ_QUERY_EA への応答には、この呼び出しを発行します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxqueryfileinfo" data-raw-source="[&lt;strong&gt;MRxQueryFileInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxqueryfileinfo)"><strong>MRxQueryFileInfo</strong></a></td>
<td align="left"><p>RDBSS は、ファイル システム オブジェクトでネットワーク ミニリダイレクター クエリ ファイルの情報を要求するには、このルーチンを呼び出します。 RDBSS では、受信、IRP_MJ_QUERY_INFORMATION への応答には、この呼び出しを発行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxqueryquotainfo" data-raw-source="[&lt;strong&gt;MRxQueryQuotaInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxqueryquotainfo)"><strong>MRxQueryQuotaInfo</strong></a></td>
<td align="left"><p>RDBSS は、ファイル システム オブジェクトでネットワーク ミニリダイレクター クエリのクォータ情報を要求するには、このルーチンを呼び出します。 RDBSS では、受信、IRP_MJ_QUERY_QUOTA への応答には、この呼び出しを発行します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxquerysdinfo" data-raw-source="[&lt;strong&gt;MRxQuerySdInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxquerysdinfo)"><strong>MRxQuerySdInfo</strong></a></td>
<td align="left"><p>RDBSS は、ファイル システム オブジェクトでネットワーク ミニリダイレクター クエリ セキュリティ記述子の情報を要求するには、このルーチンを呼び出します。 RDBSS では、受信、IRP_MJ_QUERY_SECURITY への応答には、この呼び出しを発行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxqueryvolumeinfo" data-raw-source="[&lt;strong&gt;MRxQueryVolumeInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxqueryvolumeinfo)"><strong>MRxQueryVolumeInfo</strong></a></td>
<td align="left"><p>RDBSS は、ネットワーク ミニリダイレクター クエリのボリューム情報を要求するには、このルーチンを呼び出します。 RDBSS では、受信、IRP_MJ_QUERY_VOLUME_INFORMATION への応答には、この呼び出しを発行します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxseteainfo" data-raw-source="[&lt;strong&gt;MRxSetEaInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxseteainfo)"><strong>MRxSetEaInfo</strong></a></td>
<td align="left"><p>RDBSS は、ネットワーク ミニ リダイレクターのセットがファイル システム オブジェクトの属性情報を拡張することを要求するには、このルーチンを呼び出します。 RDBSS では、受信、IRP_MJ_SET_EA への応答には、この呼び出しを発行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxsetfileinfo" data-raw-source="[&lt;strong&gt;MRxSetFileInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxsetfileinfo)"><strong>MRxSetFileInfo</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターがファイル システム オブジェクトでファイルの情報を設定することを要求するには、このルーチンを呼び出します。 RDBSS では、受信、IRP_MJ_SET_INFORMATION への応答には、この呼び出しを発行します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxsetfileinfoatcleanup" data-raw-source="[&lt;strong&gt;MRxSetFileInfoAtCleanup&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxsetfileinfoatcleanup)"><strong>MRxSetFileInfoAtCleanup</strong></a></td>
<td align="left"><p>RDBSS cleanup ファイル システム オブジェクトのファイル情報を設定する、ネットワーク ミニ リダイレクターを要求するには、このルーチンを呼び出します。 RDBSS は、アプリケーションがハンドルを閉じるときにクリーンアップが終了する前に、この呼び出しを発行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxsetquotainfo" data-raw-source="[&lt;strong&gt;MRxSetQuotaInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxsetquotainfo)"><strong>MRxSetQuotaInfo</strong></a></td>
<td align="left"><p>RDBSS は、ネットワーク ミニ リダイレクターがファイル システム オブジェクトのクォータ情報を設定することを要求するには、このルーチンを呼び出します。 RDBSS では、受信、IRP_MJ_SET_QUOTA への応答には、この呼び出しを発行します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxsetsdinfo" data-raw-source="[&lt;strong&gt;MRxSetSdInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxsetsdinfo)"><strong>MRxSetSdInfo</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターがファイル システム オブジェクトのセキュリティ記述子の情報を設定することを要求するには、このルーチンを呼び出します。 RDBSS では、受信、IRP_MJ_SET_SECURITY への応答には、この呼び出しを発行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxsetvolumeinfo" data-raw-source="[&lt;strong&gt;MRxSetVolumeInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxsetvolumeinfo)"><strong>MRxSetVolumeInfo</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターがボリューム情報を設定することを要求するには、このルーチンを呼び出します。 RDBSS では、受信、IRP_MJ_SET_VOLUME_INFORMATION への応答には、この呼び出しを発行します。</p></td>
</tr>
</tbody>
</table>

 

 

 




