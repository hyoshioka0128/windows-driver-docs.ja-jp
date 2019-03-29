---
title: WdfDeviceResumeIdleWithTag マクロ
description: オブジェクトを指定のフレームワークのデバイスの電源参照カウント WdfDeviceResumeIdleWithTag マクロ デクリメントして、参照に、ドライバーの現在ファイル名と行番号を割り当てます。 マクロは、参照にもタグ値を割り当てます。
ms.assetid: 065393BE-CEDF-4B82-AE43-844DDB932DF0
keywords:
- WdfDeviceResumeIdleWithTag マクロ
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5eaebdc0dcc63907823799e36db3d63d088f07e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572341"
---
# <a name="wdfdeviceresumeidlewithtag-macro"></a>WdfDeviceResumeIdleWithTag マクロ


\[KMDF および UMDF に適用されます。\]

**WdfDeviceResumeIdleWithTag**フレームワークの指定したデバイスの電源参照カウントをデクリメントをマクロはオブジェクトし、参照をドライバーの現在ファイル名と行番号を割り当てます。 マクロは、参照にもタグ値を割り当てます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
VOID WdfDeviceResumeIdleWithTag(
  [in] WDFDEVICE Device,
  [in] PVOID     Tag
);
```

<a name="parameters"></a>パラメーター
----------

*デバイス*\[で\]  
Framework デバイス オブジェクトへのハンドル。

*タグ*\[で\]  
識別タグが電源参照用としてフレームワークを格納するドライバーの定義済みの値。

<a name="return-value"></a>戻り値
------------

なし。

バグ チェックでは、ドライバー、無効なオブジェクトのハンドルを提供する場合に発生します。

<a name="remarks"></a>コメント
-------

前に、オブジェクトが削除されるオブジェクトの参照カウントには、0 になると、 **WdfDeviceResumeIdleWithTag**を返します。

呼び出す**WdfDeviceResumeIdleWithTag**の代わりに[ **WdfDeviceResumeIdle** ](https://msdn.microsoft.com/library/windows/hardware/ff546838)表示できる追加の情報 (タグの値、行番号、およびファイル名) を提供しますマイクロソフトのデバッガーで **WdfDeviceResumeIdleWithTag**ドライバーの現在の行番号とファイル名を使用します。

使用して、タグ、行番号、およびファイル名の値を表示することができます、 [ **! wdfkd.wdftagtracker** ](https://msdn.microsoft.com/library/windows/hardware/ff566126)デバッガー拡張機能。

使用[ **! wdfkd.wdfdevice** ](https://msdn.microsoft.com/library/windows/hardware/ff565703)で詳細なフラグを使用しへのリンクを探します[ **! wdftagtracker** ](https://msdn.microsoft.com/library/windows/hardware/ff566126)出力。

```cpp
kd> !wdfdevice <handle> f 
```

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>対象プラットフォーム</p></td>
<td><a href="https://go.microsoft.com/fwlink/p/?linkid=531356" data-raw-source="[Universal](https://go.microsoft.com/fwlink/p/?linkid=531356)">ユニバーサル</a></td>
</tr>
<tr class="even">
<td><p>最小 KMDF バージョン</p></td>
<td><p>1.15</p></td>
</tr>
<tr class="odd">
<td><p>最小 UMDF バージョン</p></td>
<td><p>2.15</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wdfdevice.h (Wdf.h を含む)</td>
</tr>
<tr class="odd">
<td><p>Library</p></td>
<td>Wdf01000.sys (KMDF)。WUDFx02000.dll (UMDF)</td>
</tr>
<tr class="even">
<td><p>IRQL</p></td>
<td><p>&lt;= DISPATCH_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[WDF で電源参照リークのデバッグ](https://msdn.microsoft.com/library/windows/hardware/dn965441)

[**WdfDeviceResumeIdle**](https://msdn.microsoft.com/library/windows/hardware/ff546838)

[**WdfDeviceStopIdle**](https://msdn.microsoft.com/library/windows/hardware/ff546921)

[**WdfDeviceStopIdleWithTag**](wdfdevicestopidlewithtag.md)

 

 






