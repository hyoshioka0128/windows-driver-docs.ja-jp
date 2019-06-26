---
title: バグ チェック 0x74 BAD_SYSTEM_CONFIG_INFO
description: BAD_SYSTEM_CONFIG_INFO のバグ チェックでは、0x00000074 の値を持ちます。 このバグ チェックでは、レジストリにエラーがあることを示します。
ms.assetid: c59ddc44-d860-4fbb-a975-ae7226fdce86
keywords:
- バグ チェック 0x74 BAD_SYSTEM_CONFIG_INFO
- BAD_SYSTEM_CONFIG_INFO
ms.date: 03/24/2019
topic_type:
- apiref
api_name:
- BAD_SYSTEM_CONFIG_INFO
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: eed7367fc820295939ad750c2bb16c2024a9ddfd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361753"
---
# <a name="bug-check-0x74-badsystemconfiginfo"></a>バグ チェック 0x74:不適切な\_システム\_CONFIG\_情報


不適切な\_システム\_CONFIG\_情報のバグ チェックが 0x00000074 の値を持ちます。 このバグ チェックでは、レジストリにエラーがあることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="badsystemconfiginfo-parameters"></a>不適切な\_システム\_CONFIG\_情報パラメーター


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>NT ステータス値/コード (使用可能な場合)</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

不適切な\_システム\_CONFIG\_情報のバグ チェックは、システムのシステム ハイブが壊れている場合に発生します。 ただし、この破損は、ハイブの読み込み時に、ブート ローダーのチェック ハイブが破損していないため、可能性があります。

このバグ チェックは、いくつかの重要なレジストリ キーと値が存在しない場合にも発生します。 ユーザーが手動でレジストリを編集する場合、または、アプリケーションまたはサービスに、レジストリが破損している場合に、キーと値を不足していることがあります。

追加情報を参照してくださいパラメーター 4 で返された NT ステータス値を調べることができます[NTSTATUS 値](https://docs.microsoft.com/openspecs/windows_protocols/ms-erref/596a1078-e883-4972-9bbc-49e60bebca55)一覧についてはします。 

<a name="resolution"></a>解決方法
----------

エラー イベントに関連するかどうかは、任意のレジストリを参照してください。 Windows システム イベント ログで確認します。 ある場合は、hive または特定のキーでエラーが発生したかどうか、イベントが一覧表示を参照してください。

[ **! 分析**](-analyze.md)バグ チェックに関する情報を表示拡張機能をデバッグおよび根本原因を突き止めるに役に立ちます。

```
BAD_SYSTEM_CONFIG_INFO (74)
Can indicate that the SYSTEM hive loaded by the osloader/NTLDR
was corrupt.  This is unlikely, since the osloader will check
a hive to make sure it isn't corrupt after loading it.
It can also indicate that some critical registry keys and values
are not present.  (i.e. somebody used regedt32 to delete something
that they shouldn't have)  Booting from LastKnownGood may fix
the problem, but if someone is persistent enough in mucking with
the registry they will need to reinstall or use the Emergency
Repair Disk.
Arguments:
Arg1: 0000000000000002, (reserved)
Arg2: ffffd481054b49f0, (reserved)
Arg3: 0000000000000004, (reserved)
Arg4: ffffffffc000014c, usually the NT status code.

```

すべてによって返される情報の確認、!、エラーの詳細について分析します。

使用して、 [! エラー](-error.md)パラメーター 4 に NTSTATUS 値に関する情報を表示する拡張機能。

```
2: kd> !ERROR ffffffffc000014c
Error code: (NTSTATUS) 0xc000014c (3221225804) - {The Registry Is Corrupt}  The structure of one of the files that contains Registry data is corrupt, or the image of the file in memory is corrupt, or the file could not be recovered because the alternate copy or log was absent or corrupt.
```

使用して、 [! reg](-reg.md)拡張子レジストリ ハイブが存在する例については、レジストリに関する情報を表示します。

```
!reg hivelist

-------------------------------------------------------------------------------------------------------------------------------------------------------
|     HiveAddr     |Stable Length|    Stable Map    |Volatile Length|    Volatile Map    |MappedViews|PinnedViews|U(Cnt)|     BaseBlock     | FileName 
-------------------------------------------------------------------------------------------------------------------------------------------------------
| ffff95077ea24000 |       1000  | ffff95077ea24588 |          0    |  0000000000000000  |     0| ffff95077ea31000  | <NONAME>
| ffff95077ea3e000 |    12d3000  | ffff95077ea49000 |      21000    |  ffff95077ea3e800  |     0| ffff95077ea40000  | SYSTEM
| ffff95077ea8f000 |      53000  | ffff95077ea8f588 |       9000    |  ffff95077ea8f800  |     0| ffff95077ea91000  | <NONAME>
| ffff9507821c8000 |       7000  | ffff9507821c8588 |          0    |  0000000000000000  |     0| ffff9507821cc000  | kVolume2\EFI\Microsoft\Boot\BCD
| ffff95077f6ae000 |    685c000  | ffff95077f737000 |       6000    |  ffff95077f6ae800  |     0| ffff95077f6b6000  | emRoot\System32\Config\SOFTWARE
-------------------------------------------------------------------------------------------------------------------------------------------------------
```

使用して、! reg openkeys コマンドをどのレジストリ キーが開放されていた。

```
2: kd> !reg openkeys

Hive: \REGISTRY\MACHINE\SYSTEM
===========================================================================================
Index 0:     00000000 kcb=ffffd805e303c728 cell=00000020 f=002c0100 \REGISTRY\MACHINE\SYSTEM
Index 1:     db67f96d kcb=ffffd805e416ed18 cell=00bd0b40 f=00200080 \REGISTRY\MACHINE\SYSTEM\WPA\8DEC0AF1-0341-4B93-85CD-72606C2DF94C-7P-374
Index 3:     db67ee93 kcb=ffffd805e30c5ab8 cell=00bc1550 f=00200080 \REGISTRY\MACHINE\SYSTEM\WPA\8DEC0AF1-0341-4B93-85CD-72606C2DF94C-7P-161
Index 4:     f9909d96 kcb=ffffd805e44bd268 cell=00bf8f50 f=00200000 \REGISTRY\MACHINE\SYSTEM\CONTROLSET001\CONTROL\POWER\PROFILE\EVENTS\{54533251-82BE-4824-96C1-47B60B740D00}\{8BC6262C-C026-411D-AE3B-7E2F70811A13}
Index 5:     e9dd6ce5 kcb=ffffd805e4180e48 cell=00812970 f=00200000 \REGISTRY\MACHINE\SYSTEM\DRIVERDATABASE

...

```


**旅行時間のトレース**

バグ チェックはオンデマンドで再現できる場合は、WinDbg のプレビューを使用してタイム トラベル トレースを取ることの可能性を調査します。 詳細については、次を参照してください。[タイム トラベルのデバッグ - 概要](time-travel-debugging-overview.md)します。


<a name="remarks"></a>注釈
----------

セーフ モードで起動してみてくださいし、通常どおり、OS を再起動します。 再起動に問題が解決しない場合、レジストリの破損があまり広範囲にわたってします。 次の手順を実行してください。

-   システム復元ポイントがある場合は、以前の復元ポイントに復元してみてください。
-   お使いの PC をリセットします。
-   インストール メディアを使用して、復元またはお使いの PC をリセットします。
-   インストール メディアを使用して、Windows を再インストールします。

詳細については、次を参照してください。 [Windows 10 での回復オプション](https://support.microsoft.com/help/12415/windows-10-recovery-options#)します。

このサポートの記事では、このバグ チェック コードについて説明します。[エラー 0x74:Bad_system_config_info](https://support.microsoft.com/en-us/help/4028653/windows-error-0x74-badsystemconfiginfo)

 

 




