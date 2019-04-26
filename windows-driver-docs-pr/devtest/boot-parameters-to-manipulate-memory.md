---
title: メモリを操作するためのブート パラメーター
description: メモリを操作するためのブート パラメーター
ms.assetid: 04504216-20b5-4c65-a1e2-6eec7480ce17
keywords:
- WDK のメモリに関連するブート オプション
- WDK のブート パラメーター
- ブート エントリ パラメーター WDK
- WDK のメモリのブート パラメーターを操作します。
- メモリの少ない環境 WDK のブート パラメーター
- メモリの少ない環境 WDK のブート パラメーターをシミュレートします。
- WDK のメモリのブート パラメーター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44f681a3c60afec6b3d5d72bb2078d517e70f993
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344922"
---
# <a name="boot-parameters-to-manipulate-memory"></a>メモリを操作するためのブート パラメーター


## <span id="ddk_boot_parameters_to_manipulate_memory_tools"></span><span id="DDK_BOOT_PARAMETERS_TO_MANIPULATE_MEMORY_TOOLS"></span>


コンピューターの物理メモリのサイズを変更することがなくテスト用のメモリの少ない環境をシミュレートすることができます。 使用して、オペレーティング システムで使用できるメモリを制限する代わりに、 **truncatememory**または**removememory**でオプションを[ **BCDedit/set**](https://msdn.microsoft.com/library/windows/hardware/ff542202)コマンド。

**/Maxmem**パラメーターは、Windows で使用できるメモリの最大の容量を指定します。 メガバイト (MB) 単位で調整することには。 値を実際の物理メモリよりも小さいかコンピューターのサイズに設定します。

**/Maxmem**パラメーターが実際に Windows を使用可能な最大のメモリ アドレスを決定します。 Windows の物理メモリのマッピング、ギャップのための値よりもやや少ないメモリを受け取ることがあります **/maxmem**します。 有効桁数の詳細、使用 **/burnmemory**します。

**Truncatememory**または**removememory**オプションは、Windows 7 で使用できる以降。 **Truncatememory**オプションで指定された物理アドレス以上のすべてのメモリは無視されます。 **Removememory**オプションが指定の量 (MB 単位) の Windows を使用可能なメモリを削減します。 両方のオプションの短縮、メモリが、 **removememory**オプションはメモリのギャップの計算中に指定されたメモリを使用するオペレーティング システムを制限することで向上します。

### <a name="span-idbootparameterstotestinalowmemoryenvironmentinwindowsvistaaspanspan-idbootparameterstotestinalowmemoryenvironmentinwindowsvistaaspanboot-parameters-to-test-in-a-low-memory-environment-in-windows"></a><span id="boot_parameters_to_test_in_a_low_memory_environment_in_windows_vista_a"></span><span id="BOOT_PARAMETERS_TO_TEST_IN_A_LOW_MEMORY_ENVIRONMENT_IN_WINDOWS_VISTA_A"></span>Windows でのメモリの少ない環境でテストのブート パラメーター

メモリ不足の環境をシミュレートするには、使用、 [ **BCDedit/set** ](https://msdn.microsoft.com/library/windows/hardware/ff542202)コマンドと**removememory**ブート エントリを変更するオプション。 値を設定**removememory**からこのテストの目的のメモリ サイズを引いた、システム上の物理メモリの量にします。

たとえば、2 GB、512 MB 使用可能なメモリの最大物理メモリの使用のコンピューターのメモリを制限するための値を設定、 **removememory** 1536 (2 GB (2048 MB) - 512 MB = 1536 MB) のパラメーター。

次の例では、指定されたブート エントリのシステムに使用可能な合計から 1536 MB のメモリを削除する BCDEdit のコマンドを示します。

```
bcdedit /set {18b123cd-2bf6-11db-bfae-00e018e2b8db} removememory 1536
```

使用することも、 **truncatememory**オプションは、 **bcdedit/set**同じ結果を実現するためにコマンド。 このオプションを使用する場合、Windows は、指定された物理アドレス以上のすべてのメモリを無視します。 指定、*アドレス*(バイト単位)。 たとえば、次のコマンドは、指定されたブート エントリの 1 GB で、物理アドレスの制限を設定します。 (1073741824) を 10 進数または 16 進数 (0x40000000) アドレスを指定することができます。

```
bcdedit /set {18b123cd-2bf6-11db-bfae-00e018e2b8db} truncatememory Ox40000000
```

**Removememory**オプションではシステム メモリの効率的な使用が、その使用を推奨の代わりに**truncatememory**します。

完了したら削除する、テスト、 **removememory**と**truncatememory**ブート エントリのオプションを使用して、 [ **BCDEdit/deletevalue** ](https://msdn.microsoft.com/library/windows/hardware/jj856916)コマンド。

 

 





