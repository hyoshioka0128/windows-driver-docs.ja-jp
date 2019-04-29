---
title: WDFVERIFY マクロ
description: WDFVERIFY マクロでは、論理式をテストし、式が FALSE に評価される場合は、カーネル デバッガーを中断します。
ms.assetid: 9dc19299-7eda-42fb-811e-ba8dc5c1cdb5
keywords:
- WDFVERIFY マクロ
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2417852f088c947bffb0f7d121327782ce428c3d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385731"
---
# <a name="wdfverify-macro"></a>WDFVERIFY マクロ


\[KMDF にのみ適用されます。\]

**WDFVERIFY**マクロ論理式をテストして、式の評価が**FALSE**、カーネル デバッガーを中断します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
VOID WDFVERIFY(
    exp
);
```

<a name="parameters"></a>パラメーター
----------

*exp 関数*   
WDFVERIFY をテストする論理式。

<a name="return-value"></a>戻り値
------------

なし

<a name="remarks"></a>注釈
-------

コードを**WDFVERIFY**リリース構成またはデバッグ構成で、ドライバーをビルドするときに、ドライバーのバイナリにマクロが含まれます。 場合は、ドライバーのバイナリが含まれています。 **WDFVERIFY**コード、コードはチェック ビルドまたは Microsoft Windows オペレーティング システムのビルドでは、ドライバーが実行される場合に実行されます。

**WDFVERIFY**場合のみカーネル デバッガーにコードでは、 **VerifyOn**レジストリの値を設定します。 ドライバーをデバッグする際のレジストリ エントリの詳細については、次を参照してください。 [Debugging Framework-Based ドライバーのレジストリ エントリ](https://msdn.microsoft.com/library/windows/hardware/ff544573)します。

ドライバーのデバッグの詳細については、次を参照してください。 [KMDF ドライバーをデバッグ](https://msdn.microsoft.com/library/windows/hardware/ff540790)します。

<a name="examples"></a>例
--------

次のコード例は、要求オブジェクトを再利用失敗した場合、デバッガーを中断します。

```cpp
status = WdfRequestReuse(Request, &amp;params);
WDFVERIFY(NT_SUCCESS(status));
```

<a name="requirements"></a>要件
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
<td><p>1.0</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdfassert.h (Wdf.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**VERIFY_IS_IRQL_PASSIVE_LEVEL**](verify-is-irql-passive-level.md)

 

 






