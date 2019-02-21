---
title: CcSetReadAheadGranularityEx ルーチン
description: CcSetReadAheadGranularityEx ルーチンでは、先行読み取りの粒度を設定し、パイプライン処理の先読みのキャッシュされたファイルを使用します。
ms.assetid: D70C3397-CF37-46E5-BA84-819BC984665A
keywords:
- CcSetReadAheadGranularityEx ルーチン インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- CcSetReadAheadGranularityEx
api_location:
- NtosKrnl.exe
api_type:
- DllExport
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bb32271d65c55f031cb288cbfb2491ae0ec6cde
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539172"
---
# <a name="ccsetreadaheadgranularityex-routine"></a>CcSetReadAheadGranularityEx ルーチン


**CcSetReadAheadGranularityEx**日常的な先行読み取りの粒度の設定やパイプライン処理の先読みのキャッシュされたファイルを使用します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
VOID CcSetReadAheadGranularityEx(
  _In_ PFILE_OBJECT FileObject,
  _In_ PREAD_AHEAD_PARAMETERS    ReadAheadParameters
);
```

<a name="parameters"></a>パラメーター
----------

*FileObject* \[in\]  
ファイル オブジェクトへのポインターのキャッシュされたファイルが先行読み取りの粒度を設定するがします。

*ReadAheadParameters* \[in\]  
先行読み取りのパラメーターを指定します。 参照してください[READ_AHEAD_PARAMETERS](read-ahead-parameters.md)詳細についてはします。

<a name="return-value"></a>戻り値
------------

なし

<a name="remarks"></a>注釈
-------

呼び出す**CcSetReadAheadGranularityEx**内のファイル オブジェクトの先行読み取り要求をパイプライン処理が有効になります*FileObject*します。 適切な値を選択する*PipelinedRequestSize*は分割先行読み取りの要求をより小さな複数の並列要求。 呼び出し元**CcSetReadAheadGranularityEx**先行読み取りのパフォーマンスを調整することで調整できる*PipelinedRequestSize*します。

後[ **CcInitializeCacheMap** ](https://msdn.microsoft.com/library/windows/hardware/ff539135)する前に、ファイルをキャッシュするために呼び出される**CcSetReadAheadGranularityEx**はキャッシュされたファイル、既定の先行読み取りの粒度に対して呼び出されますキャッシュされたファイルはページに等しくなります\_サイズ。

<a name="requirements"></a>要件
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


[**CcInitializeCacheMap**](https://msdn.microsoft.com/library/windows/hardware/ff539135)

[**CcReadAhead**](https://msdn.microsoft.com/library/windows/hardware/ff539191)

[**CcScheduleReadAhead**](https://msdn.microsoft.com/library/windows/hardware/ff539200)

[**CcSetAdditionalCacheAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff539203)

 

 






