---
title: メモリ
description: メモリ
ms.assetid: 4aa5cf2b-e5f8-4358-b2cc-c677cd012f46
keywords:
- デバッガー エンジン、メモリ
- データ領域
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19bd486509ffd580b0be729cba51c670d39e0fca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551086"
---
# <a name="memory"></a>メモリ


[デバッガー エンジン](introduction.md#debugger-engine)直接読み取りし、書き込み先のメイン メモリ、レジスタ、およびその他のデータ領域ことができます。 カーネル モードのデバッグは、すべてのターゲットのメモリは使用できますが、仮想メモリ、物理メモリ、レジスタ、モデル特定登録 (MSRs)、システム バス メモリ、制御領域のメモリおよび I/O メモリを含みます。 ユーザー モードのデバッグ、仮想メモリとレジスタのみが利用できます。

エンジンは、64 ビットのアドレスを使用して、ターゲット内のすべてのメモリは、クライアントに公開されます。 ターゲットは、ターゲットと、クライアントと通信するときに、32 ビットのアドレスを使用している場合、エンジンは自動的に変換 32 ビットおよび 64 ビットのアドレス間で、必要に応じて。 --ターゲットから 32 ビットのアドレスが復旧される場合などメモリやレジスタ--から読み取ることによって、64 ビットの符号拡張前にありますデバッガー エンジン API で使用できます。 符号拡張がによって自動的に実行される、**されるため、** メソッド。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、読み取りと書き込みのメモリは、次を参照してください。[メモリ アクセス](memory-access.md)します。

 

 





