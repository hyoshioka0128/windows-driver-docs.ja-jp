---
title: ファイル名を管理します。
description: ファイル名を管理します。
ms.assetid: 390c3817-e306-4d20-9ec0-9d68ccc8ff1b
keywords:
- フィルター マネージャー WDK ファイル システム ミニフィルター、ファイル名
- ファイル名の WDK ファイル システム ミニフィルター
- WDK の名前のファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e49472487be997520fac5bd3d98960ed81d8a48
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537571"
---
# <a name="managing-file-names"></a>ファイル名を管理します。


フィルター マネージャーは、レガシ フィルター ドライバーを取得し、ファイル名を管理するために必要な作業の大半を排除します。 フィルター マネージャーが、現在の操作、適切な形式で参照カウントされた構造に名前を提供する名前が要求されたときに: 名前、開かれている名前、または短い名前を正規化します。

ミニフィルター ドライバーが呼び出せる[ **FltGetDestinationFileNameInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff543003)ファイルまたはディレクトリを変更する場合、または NTFS のハード リンクされている対象のリンク先の完全パス名を作成するには作成されます。 この名前は、正規化されたまたは開かれたファイルのいずれかの形式で返されることができます。

フィルター マネージャーも用意されています。、 [ **FltGetTunneledName** ](https://msdn.microsoft.com/library/windows/hardware/ff543177)を取得するためのルーチンは、ファイル名のトンネリングにより無効化されたファイル名の情報を正規化します。

パフォーマンスを向上させるフィルター マネージャー名をキャッシュに保存可能な限りシステムのすべてのミニフィルター ドライバーの間で共有されます。 ミニフィルター ドライバーには、キャッシュまたはファイル システム、またはその両方を照会できます。

ミニフィルター ドライバー、名前空間の変更を利用できますフィルター マネージャーのサポートの名プロバイダーの要求を生成するか、名前を正規化する上限ミニフィルター ドライバーなどの名前クエリ操作を傍受するコールバック ルーチンを登録することで。

### <a name="span-idfiltermanagerroutinesfornamemanagementspanspan-idfiltermanagerroutinesfornamemanagementspanspan-idfiltermanagerroutinesfornamemanagementspanfilter-manager-routines-for-name-management"></a><span id="Filter_Manager_Routines_for_Name_Management"></span><span id="filter_manager_routines_for_name_management"></span><span id="FILTER_MANAGER_ROUTINES_FOR_NAME_MANAGEMENT"></span>名前の管理用フィルター マネージャー ルーチン

フィルター マネージャーでは、名前の管理の次のサポート ルーチンを提供します。

[**FltGetDestinationFileNameInformation**](https://msdn.microsoft.com/library/windows/hardware/ff543003)

[**FltGetFileNameInformation**](https://msdn.microsoft.com/library/windows/hardware/ff543032)

[**FltGetFileNameInformationUnsafe**](https://msdn.microsoft.com/library/windows/hardware/ff543035)

[**FltGetTunneledName**](https://msdn.microsoft.com/library/windows/hardware/ff543177)

[**FltParseFileNameInformation**](https://msdn.microsoft.com/library/windows/hardware/ff543417)

[**FltReleaseFileNameInformation**](https://msdn.microsoft.com/library/windows/hardware/ff544320)

### <a name="span-idminifilterdrivercallbackroutinesfornamemanagementspanspan-idminifilterdrivercallbackroutinesfornamemanagementspanspan-idminifilterdrivercallbackroutinesfornamemanagementspanminifilter-driver-callback-routines-for-name-management"></a><span id="Minifilter_Driver_Callback_Routines_for_Name_Management"></span><span id="minifilter_driver_callback_routines_for_name_management"></span><span id="MINIFILTER_DRIVER_CALLBACK_ROUTINES_FOR_NAME_MANAGEMENT"></span>ミニフィルター ドライバー コールバック ルーチン名の管理

次のコールバック ルーチンが格納されている、 [ **FLT\_登録**](https://msdn.microsoft.com/library/windows/hardware/ff544811)構造体へのパラメーターとして渡される[ **FltRegisterFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff544305)、名前空間を変更するミニフィルター ドライバーに対して。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コールバック ルーチンの名前</th>
<th align="left">コールバック ルーチンの種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>GenerateFileNameCallback</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551087" data-raw-source="[&lt;strong&gt;PFLT_GENERATE_FILE_NAME&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551087)"><strong>PFLT_GENERATE_FILE_NAME</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><em>NormalizeContextCleanupCallback</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551100" data-raw-source="[&lt;strong&gt;PFLT_NORMALIZE_CONTEXT_CLEANUP&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551100)"><strong>PFLT_NORMALIZE_CONTEXT_CLEANUP</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>NormalizeNameComponentCallback</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551102" data-raw-source="[&lt;strong&gt;PFLT_NORMALIZE_NAME_COMPONENT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551102)"><strong>PFLT_NORMALIZE_NAME_COMPONENT</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 




