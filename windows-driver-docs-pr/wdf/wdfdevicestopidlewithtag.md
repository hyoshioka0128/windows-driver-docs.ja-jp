---
title: WdfDeviceStopIdleWithTag マクロ
description: WdfDeviceStopIdleWithTag マクロは、指定のフレームワークのデバイス オブジェクトの電源の参照カウントをインクリメントし、参照に、ドライバーの現在のファイル名と行番号を割り当てます。 マクロは、参照にもタグ値を割り当てます。
ms.assetid: 792A5EA8-5273-4284-B0EE-01BE1DCB9863
keywords:
- WdfDeviceStopIdleWithTag マクロ
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 437bce066d1e72167a4b340d37a5cc94e355abc8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570479"
---
# <a name="wdfdevicestopidlewithtag-macro"></a>WdfDeviceStopIdleWithTag マクロ


\[KMDF および UMDF に適用されます。\]

**WdfDeviceStopIdleWithTag**マクロが指定のフレームワークのデバイス オブジェクトの電源の参照カウントをインクリメントし、参照に、ドライバーの現在ファイル名と行番号を割り当てます。 マクロは、参照にもタグ値を割り当てます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
NTSTATUS WdfDeviceStopIdleWithTag(
  [in] WDFDEVICE Device,
  [in] BOOLEAN   WaitForD0,
  [in] PVOID     Tag
);
```

<a name="parameters"></a>パラメーター
----------

*デバイス*\[で\]  
Framework デバイス オブジェクトへのハンドル。

*WaitForD0* \[で\]  
タイミングを示すブール値**WdfDeviceStopIdleWithTag**が返されます。 場合**TRUE**、指定されたデバイスには、D0 デバイスの電源状態が入力した後にのみが返されます。 場合**FALSE**メソッドはすぐに返します。

*タグ*\[で\]  
識別タグが電源参照用としてフレームワークを格納するドライバーの定義済みの値。

<a name="return-value"></a>戻り値
------------

操作が成功すると、 **WdfDeviceStopIdleWithTag** STATUS_SUCCESS を返します。 ドライバーを呼び出す場合**WdfDeviceStopIdleWithTag**メソッドが STATUS_SUCCESS を返しますが、電源の参照カウントは増分されません (D0) の作業の状態で、デバイスがある場合。

追加の戻り値は次のとおりです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>リターン コード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>STATUS_PENDING</strong></td>
<td><p>デバイスの電源を非同期的にします。</p></td>
</tr>
<tr class="even">
<td><strong>STATUS_INVALID_DEVICE_STATE</strong></td>
<td><p>ドライバーは、デバイスの電源ポリシーの所有者ではありません。</p></td>
</tr>
<tr class="odd">
<td><strong>STATUS_POWER_STATE_INVALID</strong></td>
<td><p>デバイスの障害が発生し、デバイスが D0 電力状態を入力することはできません。</p></td>
</tr>
</tbody>
</table>

 

その他のメソッドが返す可能性があります[NTSTATUS 値](https://msdn.microsoft.com/library/windows/hardware/ff557697)します。

バグ チェックでは、ドライバー、無効なオブジェクトのハンドルを提供する場合に発生します。

<a name="remarks"></a>コメント
-------

ドライバーを呼び出す場合**WdfDeviceStopIdleWithTag**参照カウントをインクリメントするドライバーを呼び出す必要があります[ **WdfDeviceResumeIdleWithTag** ](wdfdeviceresumeidlewithtag.md)カウントをデクリメントします。

呼び出す**WdfDeviceStopIdleWithTag**の代わりに[ **WdfDeviceStopIdle** ](https://msdn.microsoft.com/library/windows/hardware/ff546921)で表示できる追加の情報 (タグの値、行番号、およびファイル名) を提供しますマイクロソフトのデバッガーです。 **WdfDeviceStopIdleWithTag**ドライバーの現在の行番号とファイル名を使用します。

使用して、タグ、行番号、およびファイル名の値を表示することができます、 [ **! wdftagtracker** ](https://msdn.microsoft.com/library/windows/hardware/ff566126)デバッガー拡張機能。 デバッガー拡張機能では、ポインターと、一連の文字の両方として、タグの値が表示されます。

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

[**WdfDeviceResumeIdleWithTag**](wdfdeviceresumeidlewithtag.md)

[**WdfDeviceStopIdle**](https://msdn.microsoft.com/library/windows/hardware/ff546921)

 

 






