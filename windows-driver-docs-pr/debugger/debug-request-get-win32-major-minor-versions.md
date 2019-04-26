---
title: デバッグ\_要求\_取得\_WIN32\_メジャー\_マイナー\_バージョン
description: デバッグ\_要求\_取得\_WIN32\_メジャー\_マイナー\_バージョン
ms.assetid: 3764add2-a96a-41c8-9747-6a1ef3d8b5af
keywords:
- デバッグ DEBUG_REQUEST_GET_WIN32_MAJOR_MINOR_VERSIONS Windows
topic_type:
- apiref
api_name:
- DEBUG_REQUEST_GET_WIN32_MAJOR_MINOR_VERSIONS
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9a905dac30e8584243a4b60e72887aded34503f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349070"
---
# <a name="debugrequestgetwin32majorminorversions"></a>デバッグ\_要求\_取得\_WIN32\_メジャー\_マイナー\_バージョン


デバッグ\_要求\_取得\_WIN32\_メジャー\_マイナー\_バージョン[**要求**](request.md)操作は戻り、現在、ターゲットで実行されている Windows のバージョンです。

**Parameters**

<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
使用されていません。

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
ターゲットで現在実行されている Windows のバージョンとマイナー バージョン番号。 バージョン番号の種類は、2 つの ULONG 値を含む配列配列内の最初の ULONG はメジャー バージョン番号、2 番目のマイナー バージョン番号

次の表は、オペレーティング システムによって、メジャーおよびマイナー バージョン番号を示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Windows のバージョン</th>
<th align="left">メジャー バージョン番号</th>
<th align="left">マイナー バージョン番号</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Windows 2000</p></td>
<td align="left"><p>5</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows XP</p></td>
<td align="left"><p>5</p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Server 2003</p></td>
<td align="left"><p>5</p></td>
<td align="left"><p>2</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**要求**](request.md)

 

 






