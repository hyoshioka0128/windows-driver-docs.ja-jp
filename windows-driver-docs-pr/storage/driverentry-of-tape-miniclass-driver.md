---
title: Tape Miniclass Driver ルーチンの DriverEntry
description: DriverEntry は、tape miniclass ドライバーを初期化します。 このルーチンは必須です。
ms.assetid: dc082f31-5ec5-491e-a347-8f8e485c042b
keywords:
- DriverEntry のルーチンストレージデバイス
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
ms.openlocfilehash: 034bd2fb6c439d722a34c0fa8fad4df60471074d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845168"
---
# <a name="driverentry-of-tape-miniclass-driver-routine"></a>Tape Miniclass Driver ルーチンの DriverEntry


**Driverentry**は、tape miniclass ドライバーを初期化します。 このルーチンは必須です。

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

\] の*引数 1* \[  
テープ miniclass ドライバーが[**TapeClassInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/minitape/nf-minitape-tapeclassinitialize)に渡すドライバーコンテキストへのポインター。 コンテキスト情報の形式は OS 固有であり、ポータブルテープ miniclass ドライバーでは解釈できません。

\] の*引数 2* \[  
Tape miniclass ドライバーが**TapeClassInitialize**に渡す2番目のコンテキスト構造へのポインター。 コンテキスト情報の形式は OS 固有であり、ポータブルテープ miniclass ドライバーでは解釈できません。

<a name="return-value"></a>戻り値
------------

**Driverentry**は、 **TapeClassInitialize**への呼び出しによって返された値を返します。

<a name="remarks"></a>注釈
-------

**Driverentry**は、tape miniclass ドライバーの最初のエントリポイントです。

**TapeClassInitialize**は、必要なドライバーの初期化の大部分を実行するため、tape miniclass ドライバーの**driverentry**ルーチンの主なタスクは、次を使用して、テープ\_INIT\_DATA\_EX 構造体に割り当てて入力することです。ドライバー固有の定数とエントリポイント。

**Driverentry**では、最初に[**TapeClassZeroMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/minitape/nf-minitape-tapeclasszeromemory)を呼び出して、テープ\_INIT\_DATA\_EX 構造体をクリアする必要があります。 **Driverentry**は、構造体の値とポインターを設定します。

**Driverentry**は**TapeClassInitialize**を呼び出し、\_EX\_DATA EX と**Driverentry** (*引数 1*および*引数 2*) に渡された2つのポインターを\_します。 **TapeClassInitialize**はドライバーの初期化を完了し、status を tape miniclass ドライバーの**driverentry**ルーチンに返します。 **Driverentry**は、 **TapeClassInitialize**から受信した状態を返します。

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
<td align="left">Desktop</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Minitape</td>
</tr>
<tr class="odd">
<td align="left"><p>Library</p></td>
<td align="left">Ntoskrnl.exe</td>
</tr>
<tr class="even">
<td align="left"><p>DLL</p></td>
<td align="left">Ntoskrnl.exe</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**TAPE\_INIT\_DATA\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/minitape/ns-minitape-_tape_init_data_ex)

[**TapeClassInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/minitape/nf-minitape-tapeclassinitialize)

[**TapeClassZeroMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/minitape/nf-minitape-tapeclasszeromemory)

[**テープの\_の状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/minitape/ne-minitape-_tape_status)

 

 






