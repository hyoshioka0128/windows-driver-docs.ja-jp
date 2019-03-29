---
title: システムで使用するために予約済みの Windows カーネル ルーチン
description: システムで使用するために予約済みの Windows カーネル ルーチン
ms.assetid: 78b0562a-903a-467d-9bf0-f5499ae47063
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ca65deeb98e548fe40020d4113cae56d56d04664
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582204"
---
# <a name="windows-kernel-routines-reserved-for-system-use"></a>システムで使用するために予約済みの Windows カーネル ルーチン


システムの使用は、次のルーチンが予約されています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ルーチン</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>IoAcquireRemoveLockEx</strong></td>
<td><p>参照してください<a href="https://msdn.microsoft.com/library/windows/hardware/ff548204" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548204)"> <strong>IoAcquireRemoveLock</strong></a>します。</p></td>
</tr>
<tr class="even">
<td><strong>IoInitializeRemoveLockEx</strong></td>
<td><p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff549324" data-raw-source="[&lt;strong&gt;IoInitializeRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549324)"> <strong>IoInitializeRemoveLock</strong> </a>代わりにします。</p></td>
</tr>
<tr class="odd">
<td><strong>IoReleaseRemoveLockAndWaitEx</strong></td>
<td><p>参照してください<a href="https://msdn.microsoft.com/library/windows/hardware/ff549567" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLockAndWait&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549567)"> <strong>IoReleaseRemoveLockAndWait</strong></a>します。</p></td>
</tr>
<tr class="even">
<td><strong>IoReleaseRemoveLockEx</strong></td>
<td><p>参照してください<a href="https://msdn.microsoft.com/library/windows/hardware/ff549560" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549560)"> <strong>IoReleaseRemoveLock</strong></a>します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[**IoAcquireRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff548204)  
[**IoInitializeRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff549324)  
[**IoReleaseRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff549560)  
[**IoReleaseRemoveLockAndWait**](https://msdn.microsoft.com/library/windows/hardware/ff549567)  



