---
title: 特別なプールを構成します。
description: 特別なプールを構成します。
ms.assetid: a6c90e88-8d67-47e8-8862-b7585a5d8bec
keywords:
- GFlags、カーネルの特別なプールを構成します。
- 特別なプールのカーネル
- 特別なプール
- プール タグと特別なプール
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13439d575fa762306539fe547793a6bba0b55305
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529659"
---
# <a name="configuring-special-pool"></a>特別なプールを構成します。


## <span id="ddk_configuring_kernel_special_pool_dtools"></span><span id="DDK_CONFIGURING_KERNEL_SPECIAL_POOL_DTOOLS"></span>


Gflags*特別なプール*機能に指示予約済みのメモリ プールから Windows がメモリの割り当てを要求するメモリの指定したプール タグを割り当てることがまたはが指定されたサイズの範囲内とします。

この機能の詳細については、[特別なプール](special-pool.md)を参照してください。

Windows Vista および Windows の以降のバージョンでは、特別なプール機能を構成するには、システム全体のレジストリ設定としてまたはカーネルのフラグと設定は再起動は必要ありません。 以前のバージョンの Windows では、特別なプールはレジストリ設定としてのみ使用できます。

Windows Vista および以降のバージョンの Windows では、プールでプールの特殊なタグを要求するのにコマンドラインを使用することもできます。 詳しくは、[ **GFlags コマンド**](gflags-commands.md)を参照してください。

このセクションには、次のトピックがあります。

[プールでプールの特殊なタグを要求します。](requesting-special-pool-by-pool-tag.md)

[特別なプールの割り当てサイズを要求します。](requesting-special-pool-by-allocation-size.md)

[特別なプールの要求をキャンセルします。](canceling-requests-for-special-pool.md)

[アンダーラン オーバーランを検出](detecting-overruns-and-underruns.md)

**注**  使用*Driver Verifier*を特定のドライバーが特別なプールの割り当てを要求します。 詳細については、Windows Driver Kit (WDK) の"Driver Verifier"セクションでは「特別なプール」トピックを参照してください。

 

 

 





