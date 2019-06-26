---
title: テープ Miniclass ドライバーの DriverEntry ルーチン
description: DriverEntry では、テープ miniclass ドライバーを初期化します。 このルーチンが必要です。
ms.assetid: dc082f31-5ec5-491e-a347-8f8e485c042b
keywords:
- DriverEntry ルーチン ストレージ デバイス
topic_type:
- apiref
api_name:
- DriverEntry
api_location:
- NtosKrnl.exe
api_type:
- DllExport
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1407c3fc2fb9035754ae0b72659b3e94ac9bab4a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368260"
---
# <a name="driverentry-of-tape-miniclass-driver-routine"></a>テープ Miniclass ドライバーの DriverEntry ルーチン


**DriverEntry**テープ miniclass ドライバーを初期化します。 このルーチンが必要です。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
ULONG DriverEntry(
  _In_ PVOID Argument1,
  _In_ PVOID Argument2
);
```

<a name="parameters"></a>パラメーター
----------

*[引数 1]* \[で\]  
テープの miniclass ドライバーからに渡されるドライバー コンテキストへのポインター [ **TapeClassInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/minitape/nf-minitape-tapeclassinitialize)します。 コンテキスト情報の形式は、OS 固有で移植可能なテープ miniclass ドライバーによって解釈する必要があります。

*[引数 2]* \[で\]  
テープの miniclass ドライバーからに渡される 2 つ目のコンテキスト構造へのポインター **TapeClassInitialize**します。 コンテキスト情報の形式は、OS 固有で移植可能なテープ miniclass ドライバーによって解釈する必要があります。

<a name="return-value"></a>戻り値
------------

**DriverEntry**呼び出しによって返される値を返します**TapeClassInitialize**します。

<a name="remarks"></a>注釈
-------

**DriverEntry**テープ miniclass ドライバーの最初のエントリ ポイントです。

**TapeClassInitialize** 、必要なドライバーの初期化のテープ miniclass ドライバーの主要なタスクのほとんどを実行**DriverEntry**ルーチンは、テープの入力を割り当てたり\_INIT\_データ\_EX ドライバー固有の定数とエントリ ポイントを含む構造体。

**DriverEntry**最初に呼び出す必要があります[ **TapeClassZeroMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/minitape/nf-minitape-tapeclasszeromemory)テープを消去する\_INIT\_データ\_EX 構造体。 **DriverEntry**構造内の値とポインターを設定します。

**DriverEntry**呼び出し**TapeClassInitialize**し、テープのアドレスを渡します\_INIT\_データ\_EX と 2 つのポインターに渡された**DriverEntry**( *[引数 1]* と *[引数 2]* )。 **TapeClassInitialize**ドライバーの初期化が完了して、テープ miniclass ドライバーの状態を返します**DriverEntry**ルーチン。 **DriverEntry**から受信した状態を返します**TapeClassInitialize**します。

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
<td align="left">Desktop</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Minitape.h</td>
</tr>
<tr class="odd">
<td align="left"><p>Library</p></td>
<td align="left">NtosKrnl.lib</td>
</tr>
<tr class="even">
<td align="left"><p>DLL</p></td>
<td align="left">NtosKrnl.exe</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**テープ\_INIT\_データ\_例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/minitape/ns-minitape-_tape_init_data_ex)

[**TapeClassInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/minitape/nf-minitape-tapeclassinitialize)

[**TapeClassZeroMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/minitape/nf-minitape-tapeclasszeromemory)

[**テープ\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/minitape/ne-minitape-_tape_status)

 

 






