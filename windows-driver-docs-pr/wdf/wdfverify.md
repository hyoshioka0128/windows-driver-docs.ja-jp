---
title: WDFVERIFY マクロ
description: WDFVERIFY マクロは論理式をテストし、式が FALSE と評価された場合、カーネルデバッガーを中断します。
ms.assetid: 9dc19299-7eda-42fb-811e-ba8dc5c1cdb5
keywords:
- WDFVERIFY マクロ
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fcd41e199a8bb5a4a18aa8b3787f01754ba0d93
ms.sourcegitcommit: 46853426563bfac36651565181d7edac339f63af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74261411"
---
# <a name="wdfverify-macro"></a>WDFVERIFY マクロ


\[は KMDF にのみ適用され\]

**Wdfverify**マクロは論理式をテストし、式が**FALSE**と評価された場合、カーネルデバッガーを中断します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
VOID WDFVERIFY(
    exp
);
```

<a name="parameters"></a>パラメーター
----------

*exp*   
WDFVERIFY テストを行う論理式。

<a name="return-value"></a>戻り値
------------

なし

<a name="remarks"></a>注釈
-------

**Wdfverify**マクロのコードは、ドライバーをリリース構成またはデバッグ構成でビルドするときに、ドライバーのバイナリに含まれます。

レジストリで**Verifyon**値が設定されている場合にのみ、 **wdfverify**コードがカーネルデバッガーに分割されます。 ドライバーのデバッグに使用できるレジストリエントリの詳細については、「[フレームワークベースのドライバーをデバッグするためのレジストリエントリ](https://docs.microsoft.com/windows-hardware/drivers/wdf/registry-values-for-debugging-kmdf-drivers)」を参照してください。

ドライバーのデバッグの詳細については、「 [KMDF ドライバーのデバッグ](https://docs.microsoft.com/windows-hardware/drivers/wdf/debugging-a-wdf-driver)」を参照してください。

<a name="examples"></a>例
--------

次のコード例は、要求オブジェクトを再利用しようとして失敗した場合に、デバッガーを中断します。

```cpp
status = WdfRequestReuse(Request, &params);
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
<td>Wdfassert .h (Wdf を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**VERIFY_IS_IRQL_PASSIVE_LEVEL**](verify-is-irql-passive-level.md)

 

 






