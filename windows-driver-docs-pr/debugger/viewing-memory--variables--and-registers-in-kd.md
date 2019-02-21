---
title: 表示と編集 KD のメモリ
description: 表示と編集 KD のメモリ
ms.assetid: 7E40F32F-C7B4-44A2-B3F9-84D673013EB2
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e5f10729960d63ee57d570f4ead32ab083cc2a8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536863"
---
# <a name="viewing-and-editing-memory-in-kd"></a>表示と編集 KD のメモリ


## <a name="span-idviewingandeditingmemoryspanspan-idviewingandeditingmemoryspanspan-idviewingandeditingmemoryspanviewing-and-editing-memory"></a><span id="Viewing_and_Editing_Memory"></span><span id="viewing_and_editing_memory"></span><span id="VIEWING_AND_EDITING_MEMORY"></span>表示とメモリの編集


KD の表示し、入力して、メモリを編集、 [**表示メモリ**](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)コマンドを入力して、メモリを編集できます、 [**入力値**](e--ea--eb--ed--ed--ef--ep--eq--eu--ew--eza--ezu--enter-values-.md)コマンド。 これらのコマンドの詳細については、次を参照してください。[仮想アドレスにアクセスするメモリ](accessing-memory-by-virtual-address.md)と[物理アドレスにアクセスするメモリ](accessing-memory-by-physical-address.md)します。

## <a name="span-idviewingandeditingvariablesspanspan-idviewingandeditingvariablesspanspan-idviewingandeditingvariablesspanviewing-and-editing-variables"></a><span id="Viewing_and_Editing_Variables"></span><span id="viewing_and_editing_variables"></span><span id="VIEWING_AND_EDITING_VARIABLES"></span>表示と変数の編集


KD では、表示し、コマンドを入力して、グローバル変数を編集します。 デバッガーは、仮想アドレスとして、グローバル変数の名前を解釈します。 そのため、すべての記載されているコマンド[仮想アドレスにアクセスするメモリ](accessing-memory-by-virtual-address.md)読み取りまたは書き込みのグローバル変数を使用できます。 表示とグローバル変数を編集する方法の詳細についてを参照してください。[へのアクセスのグローバル変数](accessing-global-variables.md)します。

KD では、表示し、コマンドを入力してローカル変数を編集します。 デバッガーは、アドレスとして、ローカル変数の名前を解釈します。 そのため、すべての記載されているコマンド[仮想アドレスにアクセスするメモリ](accessing-memory-by-virtual-address.md)読み取りまたは書き込みのローカル変数を使用できます。 ただし、シンボルがローカル コマンドに示すために必要な場合は、前にドル記号 ($) とシンボル、感嘆符 (! )、うに`$!var`します。 表示とローカル変数を編集する方法の詳細についてを参照してください。[にアクセスするローカル変数](accessing-local-variables.md)します。

 

 





