---
title: VERIFY_IS_IRQL_PASSIVE_LEVEL マクロ
description: ドライバーが IRQL PASSIVE_LEVEL で実行されていない場合、VERIFY_IS_IRQL_PASSIVE_LEVEL マクロはカーネルデバッガーに中断します。
ms.assetid: 7f1e25af-df66-46a2-8d27-7924677e4d5d
keywords:
- VERIFY_IS_IRQL_PASSIVE_LEVEL マクロ
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c71abe1e418f6429a500c88e334767764d9e06c
ms.sourcegitcommit: 46853426563bfac36651565181d7edac339f63af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74261435"
---
# <a name="verify_is_irql_passive_level-macro"></a>VERIFY_IS_IRQL_PASSIVE_LEVEL マクロ


[KMDF のみに適用]

ドライバーが IRQL = PASSIVE_LEVEL で実行されていない場合、 **VERIFY_IS_IRQL_PASSIVE_LEVEL**マクロはカーネルデバッガーに中断します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
VOID VERIFY_IS_IRQL_PASSIVE_LEVEL(void);
```

<a name="parameters"></a>パラメーター
----------

このマクロにはパラメーターがありません。

<a name="return-value"></a>戻り値
------------

なし

<a name="remarks"></a>注釈
-------

リリース構成またはデバッグ構成でドライバーをビルドすると、ドライバーのバイナリに**VERIFY_IS_IRQL_PASSIVE_LEVEL**マクロのコードが含まれます。 

次のいずれかに該当する場合は、 **VERIFY_IS_IRQL_PASSIVE_LEVEL**コードがカーネルデバッガーに分割されます。

-   **Dbgbreakonerror**は、レジストリで0以外の値に設定されています。
-   **VerifierOn**が0以外の値に設定され、 **dbgbreakonerror**が設定されていません。
-   ドライバーの検証機能が有効になっています。ドライバーは framework バージョン1.9 以降でビルドされていますが、 **VerifierOn**も**dbgbreakonerror**も設定されていません。

ドライバーのデバッグに使用できるレジストリエントリの詳細については、「[フレームワークベースのドライバーをデバッグするためのレジストリエントリ](https://docs.microsoft.com/windows-hardware/drivers/wdf/registry-values-for-debugging-kmdf-drivers)」を参照してください。

ドライバーのデバッグの詳細については、「 [KMDF ドライバーのデバッグ](https://docs.microsoft.com/windows-hardware/drivers/wdf/debugging-a-wdf-driver)」を参照してください。

<a name="examples"></a>例
--------

ドライバーが IRQL = PASSIVE_LEVEL で実行されていない場合、次のコード例では、カーネルデバッガーが中断されます。

```cpp
VERIFY_IS_IRQL_PASSIVE_LEVEL();
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


[**WDFVERIFY**](wdfverify.md)
