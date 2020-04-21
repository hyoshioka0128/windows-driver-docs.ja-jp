---
title: IrqlNtifsApcPassive 規則 (wdm)
description: IrqlNtifsApcPassive 規則では、ドライバーが IRQL = PASSIVE_LEVEL または IRQL < = APC_LEVEL のいずれかで実行されている場合にのみ、規則に記載されている DDIs を呼び出すように指定します。
ms.assetid: EDBF30AD-D122-4FF0-ACF9-8701E92B0A06
ms.date: 04/03/2020
keywords:
- IrqlNtifsApcPassive 規則 (wdm)
topic_type:
- apiref
api_name:
- IrqlNtifsApcPassive
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4aaef7f79bd9d2f95e66f90de81f7826f23231ac
ms.sourcegitcommit: 84be9e06fd0886598df77dffcbc75632d613c8f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2020
ms.locfileid: "81219514"
---
# <a name="irqlntifsapcpassive-rule-wdm"></a>IrqlNtifsApcPassive 規則 (wdm)

**Irqlntifsapcpassive**規則では、ドライバーが irql = PASSIVE_LEVEL または irql < = APC_LEVEL のいずれかで実行されている場合にのみ、規則に記載されている DDIs を呼び出すように指定します。

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

|                                   |                                                                                                                                    |
|-----------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー\_VERIFIER\_検出された\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x20024) |

<a name="example"></a>例
-------

次のコードは、このルールに違反しています。

```cpp
//
// KeAcquireSpinLock raises the IRQL to DISPATCH_LEVEL.
//

KeAcquireSpinLock (&Lock, &OldIrql);

//
// ERROR: ZwWriteFile can only be called at IRQL == PASSIVE_LEVEL.
//

ZwWriteFile (Handle,
             NULL,
             NULL,
             NULL,
             IoStatusBlock,
             Buffer,
             BufferLength,
             NULL,
             NULL);

KeReleaseSpinLock (&Lock, OldIrql);
```

IRQL レベルの詳細については、「[ディスパッチルーチンと IRQLs](https://docs.microsoft.com/windows-hardware/drivers/kernel/dispatch-routines-and-irqls) 」および「[ハードウェアの優先順位の管理](https://docs.microsoft.com/windows-hardware/drivers/kernel/managing-hardware-priorities)」を参照してください。

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コンパイル時</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>Irqlntifsapcpassive</strong>規則を指定します。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">コードを準備します (ロールの種類の宣言を使用します)。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">静的ドライバー検証ツールを実行します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">結果を表示して分析します。</a></li>
</ol>
<p>詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">Static Driver Verifier を使用したドライバーの欠陥の検出</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">実行時</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">
<p>1つまたは複数のドライバーについて、nuget.exe コマンドラインを使用して、DDI 準拠-追加の IRQL 規則をアクティブにすることができます。 詳細については、「<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/selecting-driver-verifier-options" data-raw-source="[Selecting Driver Verifier Options](https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking)">ドライバーの検証オプションの選択</a>」を参照してください。 DDI 準拠-追加の IRQL 規則をアクティブ化または非アクティブ化するには、コンピューターを再起動する必要があります。</p>
<p>コマンドライン、DDI 準拠-追加の IRQL チェックは、規則クラス値35で表されます。 例 :</p>
<p><code>verifier /ruleclasses 35 /driver MyDriver.sys</code></p>
<p>または</p>
<p><code>verifier /rc 35 /driver MyDriver.sys</code></p>
<p>PC が再起動されると、追加の IRQL チェックがアクティブになります。</p>
</td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>状態名
----------

NtSetInformationFile

NtWriteFile

NtCreateFile

ZwWriteFile

CcCopyWrite

CcCopyWriteEx

CcDeferWrite

CcFastCopyWrite