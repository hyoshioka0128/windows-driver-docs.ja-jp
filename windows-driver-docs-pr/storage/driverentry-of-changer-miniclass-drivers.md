---
title: チェンジャー Miniclass ドライバーの DriverEntry ルーチン
description: Microsoft Windows 2000 では、チェンジャー miniclass ドライバーには、DriverEntry ルーチンはありませんが、Windows XP 以降のオペレーティング システムで miniclass ドライバーは、次の特性を持つ DriverEntry ルーチンをいる必要があります。
ms.assetid: f7954e15-f995-44da-92fd-979248c69553
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
ms.openlocfilehash: dcd9adc72a8a19d5d29d4a4a8efed931a302b062
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368273"
---
# <a name="driverentry-of-changer-miniclass-drivers-routine"></a>チェンジャー Miniclass ドライバーの DriverEntry ルーチン


Microsoft Windows 2000 でチェンジャー miniclass ドライバーがない、 **DriverEntry** miniclass ドライバーが必要で日常的なが Windows xp およびそれ以降のオペレーティング システム、 **DriverEntry**で日常的な次の特性。

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

*[引数 1]* \[で\]  
オペレーティング システムに固有の情報へのポインター。

*[引数 2]* \[で\]  
オペレーティング システムに固有の情報へのポインター。

<a name="return-value"></a>戻り値
------------

Miniclass ドライバーの**DriverEntry**ルーチンによって返される値を返す必要があります、 [ **ChangerClassInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/nf-mcd-changerclassinitialize)ルーチン。

<a name="remarks"></a>注釈
-------

パラメーター **[引数 1]** と **[引数 2]** オペレーティング システムに固有の情報をポイントします。 Miniclass ドライバーにする必要があります*いない*これらのパラメーターを解釈しようとしています。 代わりに、これらのパラメーターを渡すか、 **ChangerClassInitialize**ルーチン。

**ChangerClassInitialize** miniclass ドライバーで必要な初期化の大部分を実行します。 主なタスクのミニドライバーの**DriverEntry**ルーチンは、そのコマンドの処理ルーチンのエントリ ポイントを読み込むには、 [ **MCD\_INIT\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/ns-mcd-_mcd_init_data)構造体し、この構造体のアドレスを渡す、 **ChangerClassInitialize**ルーチン。

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
<td align="left">Mcd.h (Mcd.h を含む)</td>
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


[**ChangerClassInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/nf-mcd-changerclassinitialize)

[**MCD\_INIT\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/ns-mcd-_mcd_init_data)

 

 






