---
title: バグチェック 0x74 BAD_SYSTEM_CONFIG_INFO
description: BAD_SYSTEM_CONFIG_INFO バグチェックの値は0x00000074 です。 このバグチェックは、レジストリにエラーがあることを示します。
ms.assetid: c59ddc44-d860-4fbb-a975-ae7226fdce86
keywords:
- バグチェック 0x74 BAD_SYSTEM_CONFIG_INFO
- BAD_SYSTEM_CONFIG_INFO
ms.date: 03/24/2019
topic_type:
- apiref
api_name:
- BAD_SYSTEM_CONFIG_INFO
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ea373249c79876070cc58c569e9a66295707e01d
ms.sourcegitcommit: 667b4be765b2eac6bc586d39abef3393a718b23f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2019
ms.locfileid: "70025324"
---
# <a name="bug-check-0x74-bad_system_config_info"></a>バグの確認 0x74:\_システム\_CONFIG\_情報が正しくありません

不良\_システム\_CONFIG\_情報バグチェックには、0x00000074 の値が設定されています。 このバグチェックは、レジストリにエラーがあることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="bad_system_config_info-parameters"></a>\_システム\_CONFIG\_の情報パラメーターが正しくありません


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
<td align="left"><p>NT 状態の値/コード (使用可能な場合)</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

システムハイブが破損している場合、不良\_システム\_CONFIG\_情報バグチェックが発生します。 ただし、この破損が発生する可能性はほとんどありません。これは、ブートローダーが hive の読み込み時にハイブが破損していることを確認するためです。

このバグチェックは、いくつかの重要なレジストリキーと値が不足している場合にも発生する可能性があります。 ユーザーが手動でレジストリを編集した場合、またはアプリケーションまたはサービスがレジストリを破損した場合、キーと値が欠落している可能性があります。

パラメーター4で返された NT 状態の値を参照すると、追加情報が提供されます。一覧については、「 [NTSTATUS 値](https://docs.microsoft.com/openspecs/windows_protocols/ms-erref/596a1078-e883-4972-9bbc-49e60bebca55)」を参照してください。 

<a name="resolution"></a>解決方法
----------

Windows システムのイベントログで、レジストリに関連するエラーイベントがあるかどうかを確認します。 イベントに、エラーが発生した hive または特定のキーが表示されているかどうかを確認できます。

! [デバッグ拡張機能の[**分析**](-analyze.md)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。

```dbgcmd
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

! Analyze によって返されたすべての情報を確認して、エラーの詳細を確認します。

パラメーター4の NTSTATUS 値に関する情報を表示するには、 [! error](-error.md)拡張機能を使用します。

```dbgcmd
2: kd> !ERROR ffffffffc000014c
Error code: (NTSTATUS) 0xc000014c (3221225804) - {The Registry Is Corrupt}  The structure of one of the files that contains Registry data is corrupt, or the image of the file in memory is corrupt, or the file could not be recovered because the alternate copy or log was absent or corrupt.
```

レジストリに存在するハイブなど、レジストリに関する情報を表示するには、 [! reg](-reg.md) extenstion を使用します。

```dbgcmd
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

! Reg sys.openkeys コマンドを使用して、どのレジストリキーが開いていたかを確認します。

```dbgcmd
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

<a name="remarks"></a>注釈
----------

セーフモードで起動し、OS を通常どおりに再起動します。 再起動によって問題が解決されない場合は、レジストリの破損が大きすぎます。 次の手順を試してください。

- システムの復元ポイントがある場合は、以前の復元ポイントに復元してみてください。
- PC をリセットします。
- インストールメディアを使用して、PC を復元またはリセットします。
- インストールメディアを使用して Windows を再インストールします。

詳細については、「 [Windows 10 の回復オプション](https://support.microsoft.com/help/12415/windows-10-recovery-options#)」を参照してください。

このサポート記事では、次のバグチェックコードについて説明します:[エラー 0x74: Bad_system_config_info](https://support.microsoft.com/help/4028653/windows-error-0x74-badsystemconfiginfo)
