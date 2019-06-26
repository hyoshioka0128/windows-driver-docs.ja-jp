---
title: 先行パラメーターの読み取り
description: 先行読み取りの粒度とパイプライン処理の先読みの先行読み取りのパラメーターです。
ms.assetid: ''
keywords:
- 先行読み取りのパラメーター
topic_type:
- apiref
api_name:
- read_ahead_parame3ters
api_location:
- NtosKrnl.exe
api_type:
- DllExport
ms.author: eliotgra
ms.date: 09/14/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06d82e8441526d3f87d42c636599e8300bd0e160
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385141"
---
# <a name="readaheadparameters-structure"></a>READ_AHEAD_PARAMETERS 構造体

**READ_AHEAD_PARAMETERS**構造体には、一般公開されている読み取り先行パラメーターが含まれています。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _READ_AHEAD_PARAMETERS {

    CSHORT NodeByteSize;
    ULONG Granularity;
    ULONG PipelinedRequestSize;
    ULONG ReadAheadGrowthPercentage;

} READ_AHEAD_PARAMETERS, *PREAD_AHEAD_PARAMETERS;
```

<a name="members"></a>Members
----------

*NodeByteSize* \[で\]  
(バイト単位) のノードのサイズ。

*粒度*\[で\]  
先行読み取りの粒度です。 この値は 2 とより大きい、または PAGE_SIZE 等しくの偶数乗である必要があります。

*PipelinedRequestSize* \[で\]  
要求のサイズ (バイト単位) を実行するときに使用するには、先行読み取りがパイプライン処理します。 各先読みをパイプライン処理要求が小さいに分割**PipelinedRequestSize**要求のサイズします。 これは、1 つの 1 つの主なものではなく複数使いを並列化によって、スループットを向上のために通常使用します。

> [!NOTE]
> 旧バージョンとの互換性のため この値が 0 の場合すべて先行読み取りの要求は、2 つに分割されます。

*ReadAheadGrowthPercentage* \[in\]  
これまでに、アプリケーションで準備済みデータの割合として事前読み取りの増加。 


<a name="remarks"></a>注釈
-------

なし 

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>対象プラットフォーム</p></td>
<td align="left"><a href="https://go.microsoft.com/fwlink/p/?linkid=531356" data-raw-source="[Universal](https://go.microsoft.com/fwlink/p/?linkid=531356)">ユニバーサル</a></td>
</tr>
<tr class="even">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 8 および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h (Ntifs.h を含む)</td>
</tr>
<tr class="even">
<td align="left"><p>Library</p></td>
<td align="left">NtosKrnl.lib</td>
</tr>
<tr class="odd">
<td align="left"><p>DLL</p></td>
<td align="left">NtosKrnl.exe</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**CcSetReadAheadGranularityEx**](CcSetReadAheadGranularityEx.md)

[**CcReadAhead**](https://docs.microsoft.com/previous-versions/ff539191(v=vs.85))

[**CcScheduleReadAhead**](https://msdn.microsoft.com/library/windows/hardware/ff539200)
