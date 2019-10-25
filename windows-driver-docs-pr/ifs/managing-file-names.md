---
title: ファイル名の管理
description: ファイル名の管理
ms.assetid: 390c3817-e306-4d20-9ec0-9d68ccc8ff1b
keywords:
- フィルターマネージャー WDK ファイルシステムミニフィルター、ファイル名
- ファイル名 WDK ファイルシステムミニフィルター
- WDK ファイルシステムの名前
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af6e56f3585fd618d18091c3783869c8f8f19c53
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841129"
---
# <a name="managing-file-names"></a>ファイル名の管理


フィルターマネージャーを使用すると、レガシフィルタードライバーがファイル名を取得して管理するために必要な作業の多くが不要になります。 名前が要求されると、フィルターマネージャーは、現在の操作に対して適切な形式 (正規化された名前、開かれた名前、または短い名前) で、参照カウント構造内の名前を提供します。

ミニパスのドライバーは、 [**FltGetDestinationFileNameInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetdestinationfilenameinformation)を呼び出して、名前を変更するか、NTFS ハードリンクを作成するファイルまたはディレクトリの完全な宛先パス名を作成できます。 この名前は、正規化またはオープンファイル形式で返すことができます。

フィルターマネージャーでは、ファイル名のトンネリングによって無効になる正規化されたファイル名情報を取得するための[**FltGetTunneledName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgettunneledname)ルーチンも用意されています。

パフォーマンスを向上させるために、フィルターマネージャーは、システム内のすべてのミニフィルタードライバー間で共有される名前をキャッシュに配置します (可能な場合)。 ミニフィルタードライバーは、キャッシュまたはファイルシステムのいずれか、またはその両方に対してクエリを実行できます。

名前空間を変更するミニフィルタードライバーでは、コールバックルーチンを登録して名前のクエリ操作 (上位ミニフィルタードライバーによる名前の生成または正規化要求など) をインターセプトすることによって、名前プロバイダーのフィルターマネージャーのサポートを利用できます。

### <a name="span-idfilter_manager_routines_for_name_managementspanspan-idfilter_manager_routines_for_name_managementspanspan-idfilter_manager_routines_for_name_managementspanfilter-manager-routines-for-name-management"></a><span id="Filter_Manager_Routines_for_Name_Management"></span><span id="filter_manager_routines_for_name_management"></span><span id="FILTER_MANAGER_ROUTINES_FOR_NAME_MANAGEMENT"></span>名前管理のフィルターマネージャールーチン

フィルターマネージャーでは、次の名前管理ルーチンがサポートされています。

[**FltGetDestinationFileNameInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetdestinationfilenameinformation)

[**FltGetFileNameInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetfilenameinformation)

[**FltGetFileNameInformationUnsafe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetfilenameinformationunsafe)

[**FltGetTunneledName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgettunneledname)

[**FltParseFileNameInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltparsefilenameinformation)

[**FltReleaseFileNameInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreleasefilenameinformation)

### <a name="span-idminifilter_driver_callback_routines_for_name_managementspanspan-idminifilter_driver_callback_routines_for_name_managementspanspan-idminifilter_driver_callback_routines_for_name_managementspanminifilter-driver-callback-routines-for-name-management"></a><span id="Minifilter_Driver_Callback_Routines_for_Name_Management"></span><span id="minifilter_driver_callback_routines_for_name_management"></span><span id="MINIFILTER_DRIVER_CALLBACK_ROUTINES_FOR_NAME_MANAGEMENT"></span>名前管理用のミニフィルタードライバーコールバックルーチン

次のコールバックルーチンは、 [**FLT\_登録**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_registration)構造体に格納されています。この構造は、名前空間を変更するミニフィルタードライバーの[**Fltregisterfilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter)にパラメーターとして渡されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コールバックルーチン名</th>
<th align="left">コールバックルーチンの種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>GenerateFileNameCallback</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_generate_file_name" data-raw-source="[&lt;strong&gt;PFLT_GENERATE_FILE_NAME&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_generate_file_name)"><strong>PFLT_GENERATE_FILE_NAME</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><em>NormalizeContextCleanupCallback</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_normalize_context_cleanup" data-raw-source="[&lt;strong&gt;PFLT_NORMALIZE_CONTEXT_CLEANUP&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_normalize_context_cleanup)"><strong>PFLT_NORMALIZE_CONTEXT_CLEANUP</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>NormalizeNameComponentCallback</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_normalize_name_component" data-raw-source="[&lt;strong&gt;PFLT_NORMALIZE_NAME_COMPONENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_normalize_name_component)"><strong>PFLT_NORMALIZE_NAME_COMPONENT</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 




