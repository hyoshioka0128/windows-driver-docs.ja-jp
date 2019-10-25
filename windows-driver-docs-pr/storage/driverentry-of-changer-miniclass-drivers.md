---
title: チェンジャー Miniclass ドライバーのルーチンの DriverEntry
description: Microsoft Windows 2000 では、チェンジャー miniclass ドライバーに DriverEntry ルーチンがありませんが、Windows XP 以降のオペレーティングシステムでは、miniclass ドライバーには次の特性を持つ DriverEntry ルーチンが必要です。
ms.assetid: f7954e15-f995-44da-92fd-979248c69553
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
ms.openlocfilehash: 3b0afece294aa0044e30e1dd2ff6aea78aa3392d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845169"
---
# <a name="driverentry-of-changer-miniclass-drivers-routine"></a>チェンジャー Miniclass ドライバーのルーチンの DriverEntry


Microsoft Windows 2000 では、チェンジャー miniclass ドライバーに**driverentry**ルーチンがありませんが、Windows XP 以降のオペレーティングシステムでは、miniclass ドライバーには次の特性を持つ**driverentry**ルーチンが必要です。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
NTSTATUS DriverEntry(
  _In_ PVOID Argument1,
  _In_ PVOID Argument2
);
```

<a name="parameters"></a>パラメーター
----------

\] の*引数 1* \[  
オペレーティングシステム固有の情報へのポインター。

\] の*引数 2* \[  
オペレーティングシステム固有の情報へのポインター。

<a name="return-value"></a>戻り値
------------

Miniclass ドライバーの**Driverentry**ルーチンは、 [**Changerclassinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mcd/nf-mcd-changerclassinitialize)ルーチンによって返された値を返す必要があります。

<a name="remarks"></a>注釈
-------

パラメーター**引数 1**と**引数 2**はオペレーティングシステム固有の情報を指します。 Miniclass ドライバーは、これらのパラメーターを解釈し*ません*。 代わりに、これらのパラメーターを**Changerclassinitialize**ルーチンに渡す必要があります。

**Changerclassinitialize**は、miniclass ドライバーに必要なほとんどの初期化を実行します。 **Driverentry**ルーチンのミニドライバーの主なタスクは、コマンド処理ルーチンへのエントリポイントを[**MCD\_INIT\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mcd/ns-mcd-_mcd_init_data)構造体に読み込み、この構造体のアドレスを**ChangerClassInitialize**ルーチン。

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
<td align="left">Mcd (Mcd を含む)</td>
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


[**ChangerClassInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mcd/nf-mcd-changerclassinitialize)

[**MCD\_INIT\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mcd/ns-mcd-_mcd_init_data)

 

 






