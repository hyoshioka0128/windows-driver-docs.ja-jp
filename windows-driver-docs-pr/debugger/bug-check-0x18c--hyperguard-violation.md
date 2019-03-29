---
title: バグ チェック 0x18C HYPERGUARD_VIOLATION
description: HYPERGUARD_VIOLATION のバグ チェックでは、0x0000018C の値を持ちます。 これは、カーネルの重大なカーネル コードまたはデータが壊れていることが検出されたことを示します。
keywords:
- バグ チェック 0x18C HYPERGUARD_VIOLATION
- HYPERGUARD_VIOLATION
ms.date: 01/04/2019
topic_type:
- apiref
api_name:
- HYPERGUARD_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7350bf0b98669a96b18ed13b99e01c942da91b82
ms.sourcegitcommit: ece0a2affa08f1b6446368ede06040b3153aaae2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/23/2019
ms.locfileid: "56743529"
---
# <a name="bug-check-0x18c-hyperguardviolation"></a>バグ チェック 0x18C の。HYPERGUARD\_違反 

HYPERGUARD\_違反のバグ チェックが 0x0000018C の値を持ちます。 これは、カーネルの重大なカーネル コードまたはデータが壊れていることが検出されたことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

> [!NOTE] 
> このバグ コードによって予約されている使用 Hyperguard のみです。  
> データ破損のシナリオでは、その他のコンポーネントで使用するための汎用バグ コードではありません。  
> 代わりに、コンポーネントの一意のバグのコードを定義します。   
> コンポーネントでは、このバグのコードを使用しません。
>

 ## <a name="hyperguardviolation-parameters"></a>HYPERGUARD\_違反パラメーター

| パラメーター | 説明 |
|-----------|-------------|
| 1         | 破損した領域 - 以下に示す値の型。 |
| 2         | エラーの種類の依存情報。 |
| 3         | 予約済み。  |
| 4         | 予約済み。  |


**破損した領域の種類**

     1001 : A generic data region
     1002 : A page hash mismatch
     1004 : A processor IDT
     1005 : A processor GDT
     1007 : Debug routine modification
     1008 : A dynamic code region
     1009 : A generic shareable data region
     100a : A hypervisor overlay region
     100b : A processor mode misconfiguration
     100c : An extended processor control register
     100d : A secure memory region
     100e : A loaded module
     100f : A processor state region
     1010 : The kernel CFG bitmap
     1011 : The virtual address 0 page
     1012 : The alternate inverted function table
     1013 : An on-demand page verification failed
     1016 : A secure image region
     1017 : Kernel virtual address protection inconsistency
     1101 : Internal context corruption
     1102 : IDTR modification
     1103 : GDTR modification



## <a name="cause"></a>原因
-----

カーネルの重大なカーネル コードまたはデータが壊れていることを検出したときに、このバグチェックが生成されます。 一般には、破損の原因が 3 つがあります。

1) ドライバーが誤ってまたは故意にクリティカルなカーネル コードまたは変更データ。 

2) 開発者は、システムが起動したときにアタッチされませんでしたが、カーネル デバッガーを使用して通常のカーネルのブレークポイントを設定しようとしました。 通常のブレークポイントを"bp"ブート時に、デバッガーがアタッチされている場合にのみ設定できます。 ハードウェアのブレークポイント、"ba"、いつでもでも設定できます。

3) 例: カーネル コードまたはデータを保持している RAM 失敗しているハードウェアの破損が発生しました。


## <a name="see-also"></a>関連項目
----------

[バグチェック コード リファレンス](bug-check-code-reference2.md)





