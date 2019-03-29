---
title: 割り当てサイズによる特別なプールの要求
description: 割り当てサイズによる特別なプールの要求
ms.assetid: 040d1a1a-1849-4253-8d4b-6c57a8643225
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7196325fc1c0558a210e2827cb0d211b703c7613
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582622"
---
# <a name="requesting-special-pool-by-allocation-size"></a>割り当てサイズによる特別なプールの要求


## <span id="ddk_requesting_special_pool_for_allocations_of_a_specified_size_dtools"></span><span id="DDK_REQUESTING_SPECIAL_POOL_FOR_ALLOCATIONS_OF_A_SPECIFIED_SIZE_DTOOLS"></span>


特別なプール サイズを指定した範囲内の割り当てを要求することができます。

Windows Vista および以降のバージョンの Windows では、プールでプールの特殊なタグを要求するのにコマンドラインを使用することもできます。 詳しくは、次を参照してください。 [ **GFlags コマンド**](gflags-commands.md)します。

**注**  モジュールが、割り当てを要求するドライバーやカーネルに関係なく、指定したサイズのすべてのカーネル プールの要求に影響するので、このメソッドは、ドライバー エラーの診断に役立つことはほとんどありません。

 

### <a name="span-idtorequestspecialpoolbyallocationsizespanspan-idtorequestspecialpoolbyallocationsizespanto-request-special-pool-by-allocation-size"></a><span id="to_request_special_pool_by_allocation_size"></span><span id="TO_REQUEST_SPECIAL_POOL_BY_ALLOCATION_SIZE"></span>特別なプールを割り当てサイズを要求するには

1.  選択、**システム レジストリ**タブまたは**カーネル フラグ**タブ。

    Windows Vista と Windows の以降のバージョンでは、このオプションは両方のタブで使用します。 以前のバージョンの Windows では、上でのみ使用できますが、**システム レジストリ**タブ。

2.  **カーネル特別なプール タグ**セクションで、 **16 進**サイズの範囲を表す 16 進形式で数値を入力し、します。 このサイズの範囲内のすべての割り当ては、特別なプールから割り当てられます。 この番号はページ未満である必要があります\_サイズ。

3.  **[適用]** をクリックします。

    次のスクリーン ショットでは、16 進数の値として入力する割り当てサイズを示します。

    ![16 進数の値として入力する割り当てサイズを示すスクリーン ショット](images/gflags-specialpool-size.png)

 

 





