---
title: IDE コント ローラーのミニドライバーの DriverEntry 関数
description: DriverEntry には、ミニドライバーを初期化します。
ms.assetid: 124f6273-ab15-426b-abce-a4d8e68e09c7
keywords:
- DriverEntry 関数ストレージ デバイス
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
ms.openlocfilehash: 4a62edaf8cce48213db00d6110d825b839330a64
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384837"
---
# <a name="driverentry-of-ide-controller-minidriver-function"></a>IDE コント ローラーのミニドライバーの DriverEntry 関数


**DriverEntry**ミニドライバーを初期化します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
NTSTATUS DriverEntry(
  _In_ PDRIVER_OBJECT  DriverObject,
  _In_ PUNICODE_STRING RegistryPath
);
```

<a name="parameters"></a>パラメーター
----------

*DriverObject* \[in\]  
IDE コント ローラー ミニドライバーのドライバーのオブジェクトへのポインターが含まれています。

*RegistryPath* \[で\]  
ドライバーの構成情報がレジストリにレジストリ パスを示す文字列を指定します。

<a name="return-value"></a>戻り値
------------

**DriverEntry**ステータスを返します\_成功から受け取ったエラー コードを返します。 成功した場合、 [ **PciIdeXInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff563788)ライブラリ ルーチン。

<a name="remarks"></a>注釈
-------

各コント ローラー ミニドライバーは、という名前のルーチンをいる必要があります**DriverEntry**を読み込むためにします。

IDE コント ローラーのミニドライバーの**DriverEntry**ルーチンを呼び出す必要があります、 [ **PciIdeXInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff563788)ライブラリ ルーチン。 **PciIdeXInitialize**コント ローラー ミニドライバーのディスパッチ テーブルを初期化します、拡張機能を割り当て、 *DriverObject*、ドライバー オブジェクトの拡張機能にさまざまな値を格納しているとします。 ドライバー オブジェクトの拡張機能に格納する必要があります値は、ドライバーの拡張機能とコント ローラー ミニドライバーへのポインターのサイズ[ **HwIdeXGetControllerProperties** ](https://msdn.microsoft.com/library/windows/hardware/ff557254)ルーチンを取得します。IDE コント ローラーについて説明します。

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
<td align="left">Ide.h (include Ide.h)</td>
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


[**HwIdeXGetControllerProperties**](https://msdn.microsoft.com/library/windows/hardware/ff557254)

[**IDE\_コント ローラー\_プロパティ**](https://msdn.microsoft.com/library/windows/hardware/ff559076)

[**PciIdeXInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff563788)

 

 






