---
title: ロックの規則セット (KMDF)
description: ドライバーが正しく共有リソースを管理することを確認するのにには、これらの規則を使用します。
ms.assetid: B6DD41A5-E7E5-4070-8752-68E26804A5D5
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: fb8bf5374ac1c57800d68203cbb489e8f58b3eb4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572378"
---
# <a name="locking-rule-set-kmdf"></a>ロックの規則セット (KMDF)


ドライバーが正しく共有リソースを管理することを確認するのにには、これらの規則を使用します。

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="kmdf-parentobjectchecklock.md" data-raw-source="[&lt;strong&gt;ParentObjectCheckLock&lt;/strong&gt;](kmdf-parentobjectchecklock.md)"><strong>ParentObjectCheckLock</strong></a></p></td>
<td align="left"><p><a href="kmdf-parentobjectchecklock.md" data-raw-source="[&lt;strong&gt;ParentObjectCheckLock&lt;/strong&gt;](kmdf-parentobjectchecklock.md)"> <strong>ParentObjectCheckLock</strong> </a>ルールでは、ドライバーを呼び出す必要がありますを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff551171" data-raw-source="[&lt;strong&gt;WdfWaitLockCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551171)"> <strong>WdfWaitLockCreate</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff550042" data-raw-source="[&lt;strong&gt;WdfSpinLockCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550042)"> <strong>WdfSpinLockCreate</strong> </a>親オブジェクトを設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-reqsendwhilespinlock.md" data-raw-source="[&lt;strong&gt;ReqSendWhileSpinlock&lt;/strong&gt;](kmdf-reqsendwhilespinlock.md)"><strong>ReqSendWhileSpinlock</strong></a></p></td>
<td align="left"><p><a href="kmdf-reqsendwhilespinlock.md" data-raw-source="[&lt;strong&gt;ReqSendWhileSpinlock&lt;/strong&gt;](kmdf-reqsendwhilespinlock.md)"> <strong>ReqSendWhileSpinlock</strong> </a>ルールでは、要求が送信されなかったこと、ドライバーは、スピン ロックを保持している間を指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-spinlock.md" data-raw-source="[&lt;strong&gt;Spinlock&lt;/strong&gt;](kmdf-spinlock.md)"><strong>spinlock</strong></a></p></td>
<td align="left"><p><a href="kmdf-spinlock.md" data-raw-source="[&lt;strong&gt;Spinlock&lt;/strong&gt;](kmdf-spinlock.md)"><strong>スピンロック</strong></a>への呼び出し規則を指定<a href="https://msdn.microsoft.com/library/windows/hardware/ff551917" data-raw-source="[&lt;strong&gt;KeAcquireSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551917)"> <strong>KeAcquireSpinLock</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff551928" data-raw-source="[&lt;strong&gt;KeAcquireSpinLockRaiseToDpc&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551928)"> <strong>KeAcquireSpinLockRaiseToDpc</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff553145" data-raw-source="[&lt;strong&gt;KeReleaseSpinlock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553145)"> <strong>KeReleaseSpinlock</strong> </a>厳密な代替構成で使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-spinlockdpc.md" data-raw-source="[&lt;strong&gt;SpinlockDpc&lt;/strong&gt;](kmdf-spinlockdpc.md)"><strong>SpinlockDpc</strong></a></p></td>
<td align="left"><p><a href="kmdf-spinlockdpc.md" data-raw-source="[&lt;strong&gt;SpinlockDpc&lt;/strong&gt;](kmdf-spinlockdpc.md)"> <strong>SpinlockDpc</strong> </a>への呼び出し規則を指定<a href="https://msdn.microsoft.com/library/windows/hardware/ff551917" data-raw-source="[&lt;strong&gt;KeAcquireSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551917)"> <strong>KeAcquireSpinLock</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff551928" data-raw-source="[&lt;strong&gt;KeAcquireSpinLockRaiseToDpc&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551928)"> <strong>KeAcquireSpinLockRaiseToDpc</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff553145" data-raw-source="[&lt;strong&gt;KeReleaseSpinlock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553145)"> <strong>KeReleaseSpinlock</strong> </a>厳密な代替構成で使用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-spinlockrelease.md" data-raw-source="[&lt;strong&gt;SpinlockRelease&lt;/strong&gt;](kmdf-spinlockrelease.md)"><strong>SpinlockRelease</strong></a></p></td>
<td align="left"><p><a href="kmdf-spinlockrelease.md" data-raw-source="[&lt;strong&gt;SpinlockRelease&lt;/strong&gt;](kmdf-spinlockrelease.md)"> <strong>SpinlockRelease</strong> </a>への呼び出し規則を指定<a href="https://msdn.microsoft.com/library/windows/hardware/ff551917" data-raw-source="[&lt;strong&gt;KeAcquireSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551917)"> <strong>KeAcquireSpinLock</strong></a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff551928" data-raw-source="[&lt;strong&gt;KeAcquireSpinLockRaiseToDpc&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551928)"> <strong>KeAcquireSpinLockRaiseToDpc</strong></a>、および<a href="https://msdn.microsoft.com/library/windows/hardware/ff553145" data-raw-source="[&lt;strong&gt;KeReleaseSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553145)"> <strong>KeReleaseSpinLock</strong> </a> KMDF コールバック内でバランスの取れた方法で使用されます。 任意の KMDF コールバック ルーチンの末尾には、ドライバーは、スピン ロックを保持しないようにします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-wdfinterruptlock.md" data-raw-source="[&lt;strong&gt;WdfInterruptLock&lt;/strong&gt;](kmdf-wdfinterruptlock.md)"><strong>WdfInterruptLock</strong></a></p></td>
<td align="left"><p><a href="kmdf-wdfinterruptlock.md" data-raw-source="[&lt;strong&gt;WdfInterruptLock&lt;/strong&gt;](kmdf-wdfinterruptlock.md)"> <strong>WdfInterruptLock</strong> </a>への呼び出し規則の指定、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff547340" data-raw-source="[&lt;strong&gt;WdfInterruptAcquireLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547340)"> <strong>WdfInterruptAcquireLock</strong> </a>メソッドに厳密な代替構成で使用されます呼び出す<a href="https://msdn.microsoft.com/library/windows/hardware/ff547376" data-raw-source="[&lt;strong&gt;WdfInterruptReleaseLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547376)"> <strong>WdfInterruptReleaseLock</strong></a>します。 さらに、任意の KMDF コールバック ルーチンの末尾には、ドライバー保持しないようにする以前の呼び出しで取得した、framework スピン ロック オブジェクト<strong>WdfInterruptAcquireLock</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-wdfinterruptlockrelease.md" data-raw-source="[&lt;strong&gt;WdfInterruptLockRelease&lt;/strong&gt;](kmdf-wdfinterruptlockrelease.md)"><strong>WdfInterruptLockRelease</strong></a></p></td>
<td align="left"><p><a href="kmdf-wdfinterruptlockrelease.md" data-raw-source="[&lt;strong&gt;WdfInterruptLockRelease&lt;/strong&gt;](kmdf-wdfinterruptlockrelease.md)"> <strong>WdfInterruptLockRelease</strong> </a>への呼び出し規則を指定<a href="https://msdn.microsoft.com/library/windows/hardware/ff547340" data-raw-source="[&lt;strong&gt;WdfInterruptAcquireLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547340)"> <strong>WdfInterruptAcquireLock</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff547376" data-raw-source="[&lt;strong&gt;WdfInterruptReleaseLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547376)"> <strong>WdfInterruptReleaseLock</strong> </a> KMDF コールバック ルーチンのバランスの取れた方法で使用されます。 任意の KMDF コールバック ルーチンの末尾には、ドライバー保持しないようにする以前の呼び出しによって取得されたフレームワークのスピン ロック オブジェクト<strong>WdfInterruptAcquireLock</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-wdfspinlock.md" data-raw-source="[&lt;strong&gt;WdfSpinlock&lt;/strong&gt;](kmdf-wdfspinlock.md)"><strong>WdfSpinlock</strong></a></p></td>
<td align="left"><p><a href="kmdf-wdfspinlock.md" data-raw-source="[&lt;strong&gt;WdfSpinlock&lt;/strong&gt;](kmdf-wdfspinlock.md)"> <strong>WdfSpinlock</strong> </a>への呼び出し規則の指定、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff550040" data-raw-source="[&lt;strong&gt;WdfSpinLockAcquire&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550040)"> <strong>WdfSpinLockAcquire</strong> </a> で厳密な代替構成体でメソッドが使用されます<a href="kmdf-wdfspinlockrelease.md" data-raw-source="[&lt;strong&gt;WdfSpinlockRelease&lt;/strong&gt;](kmdf-wdfspinlockrelease.md)"><strong>WdfSpinlockRelease</strong></a>します。 KMDF コールバック ルーチンの末尾には、ドライバー保持しないようにするフレームワーク spinlock オブジェクトを以前の呼び出しによって取得された<strong>WdfSpinLockAcquire</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-wdfspinlockrelease.md" data-raw-source="[&lt;strong&gt;WdfSpinlockRelease&lt;/strong&gt;](kmdf-wdfspinlockrelease.md)"><strong>WdfSpinlockRelease</strong></a></p></td>
<td align="left"><p><a href="kmdf-wdfspinlockrelease.md" data-raw-source="[&lt;strong&gt;WdfSpinlockRelease&lt;/strong&gt;](kmdf-wdfspinlockrelease.md)"> <strong>WdfSpinlockRelease</strong> </a>への呼び出し規則を指定<a href="https://msdn.microsoft.com/library/windows/hardware/ff550040" data-raw-source="[&lt;strong&gt;WdfSpinLockAcquire&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550040)"> <strong>WdfSpinLockAcquire</strong> </a>と<strong>WdfSpinlockRelease</strong> KMDF イベントのコールバック関数内でバランスの取れた方法で使用されます。 ドライバーでは、以前の呼び出しによって取得されたフレームワークのスピン ロック オブジェクトは保持しないようにする、KMDF イベントのコールバック関数が戻るとき<strong>WdfSpinLockAcquire</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-wdfwaitlock.md" data-raw-source="[&lt;strong&gt;WdfWaitlock&lt;/strong&gt;](kmdf-wdfwaitlock.md)"><strong>WdfWaitlock</strong></a></p></td>
<td align="left"><p><a href="kmdf-wdfwaitlock.md" data-raw-source="[&lt;strong&gt;WdfWaitlock&lt;/strong&gt;](kmdf-wdfwaitlock.md)"> <strong>WdfWaitlock</strong> </a>への呼び出し規則を指定<a href="https://msdn.microsoft.com/library/windows/hardware/ff551168" data-raw-source="[&lt;strong&gt;WdfWaitLockAcquire&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551168)"> <strong>WdfWaitLockAcquire</strong> </a>で厳密な代替構成で使用される<a href="kmdf-wdfwaitlockrelease.md" data-raw-source="[&lt;strong&gt;WdfWaitlockRelease&lt;/strong&gt;](kmdf-wdfwaitlockrelease.md)"><strong>WdfWaitlockRelease</strong></a>します。 ドライバーでは、以前の呼び出しによって取得されたフレームワークのスピン ロック オブジェクトは保持しないようにする、KMDF イベントのコールバック関数が戻るとき<strong>WdfWaitLockAcquire</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-wdfwaitlockrelease.md" data-raw-source="[&lt;strong&gt;WdfWaitlockRelease&lt;/strong&gt;](kmdf-wdfwaitlockrelease.md)"><strong>WdfWaitlockRelease</strong></a></p></td>
<td align="left"><p><a href="kmdf-wdfwaitlockrelease.md" data-raw-source="[&lt;strong&gt;WdfWaitlockRelease&lt;/strong&gt;](kmdf-wdfwaitlockrelease.md)"> <strong>WdfWaitlockRelease</strong> </a>への呼び出し規則を指定<a href="https://msdn.microsoft.com/library/windows/hardware/ff551168" data-raw-source="[&lt;strong&gt;WdfWaitLockAcquire&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551168)"> <strong>WdfWaitLockAcquire</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff551173" data-raw-source="[&lt;strong&gt;WdfWaitLockRelease&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551173)"> <strong>WdfWaitLockRelease</strong> </a> KMDF イベントのコールバック関数内でバランスの取れた方法で使用されます。 ドライバーでは、以前の呼び出しによって取得されたフレームワークのスピン ロック オブジェクトは保持しないようにする、KMDF イベントのコールバック関数が戻るとき<strong>WdfWaitLockAcquire</strong>します。</p></td>
</tr>
</tbody>
</table>

 

**ロックの規則を選択するには、次のように設定します。**

1.  Microsoft Visual Studio で、ドライバーのプロジェクト (.vcxProj) を選択します。 **ドライバー**  メニューのをクリックして**Static Driver Verifier を起動しています**.

2.  をクリックして、**ルール**タブ。**規則セット**、**ロック**します。

    Visual Studio の開発者コマンド プロンプト ウィンドウから既定のルールを選択するには、次のように指定します。 **Locking.sdv**で、 **/check**オプション。 以下に例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:Locking.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、次を参照してください。[ドライバーで障害を検出する Static Driver Verifier を使用して](https://msdn.microsoft.com/library/windows/hardware/hh454281)と[Static Driver Verifier のコマンド (MSBuild)](https://msdn.microsoft.com/library/windows/hardware/hh466459)します。

 

 





