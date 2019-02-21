---
title: デバッガーのデータ モデル - コードの Namespace
description: コードと dissasembly の属性が含まれています。
ms.date: 12/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 268c3439d37765fea71e1068f91e7e597464e101
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532786"
---
> [!IMPORTANT]
>  このインターフェイスは開発と、変更されます。
>
# <a name="the-code-namespace"></a>コードの Namespace

## <a name="summary"></a>概要
コード名前空間には、コードとの逆アセンブルの属性が含まれています。 指定されたアドレスまたは関数の逆アセンブルしたり場合があります、アセンブリに関する詳細情報と、変数またはソース情報を提供するオブジェクトを逆アセンブラーを作成できるように、利用可能な。

## <a name="sample"></a>サンプル
方法のエンド ツー エンドの例についてはこの名前空間およびオブジェクトを使用して、アカウントを github のサンプル https://github.com/Microsoft/WinDbg-Samples/tree/master/CodeFlow 

## <a name="object-methods"></a>オブジェクトのメソッド
|名前|戻り値の型|署名|説明|
|--- |--- |--- |--- |
|CreateDisassembler| [逆アセンブラー](dbgmodel-object-disassembler.md)|CreateDisassembler([architecture])|指定したアーキテクチャの逆アセンブラーを作成します。 アーキテクチャは、"ARM"、"ARM64"、"X64"、または"X86"のいずれかの可能性があります。 アーキテクチャが指定されていない場合は、X64 が使用されます。 |
|TraceDataFlow|[コレクション](dbgmodel-namespace-collections.md)の[手順](dbgmodel-object-instruction.md)|TraceDataFlow([address])|指定した命令を見て*アドレス*(または現在の命令ポインター アドレスが指定されていない場合) とすべてのソース オペランド。 このメソッドは、トレースされる命令のソース オペランドに影響を与えたの任意の命令を探して、関数の制御フローを経て内を後方に向かってについて説明します。 **このメソッドは、見つかった CodeFlow 拡張機能を読み込む必要があります[ここ](https://github.com/Microsoft/WinDbg-Samples/tree/master/CodeFlow)します。**|

## <a name="remarks"></a>注釈
CreateDisassembler の既定値は当面、この動作は、現在のスレッドの命令ポインターでモジュールのアーキテクチャをプルする変更がいくつかの時点では、"X64"です。