---
title: Debugger Data Model - コード名前空間
description: コードと dissasembly 属性が含まれています。
ms.date: 12/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: f2c7fdf532d8d7ed2040819297ec6a795c412e7e
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83235340"
---
# <a name="the-code-namespace"></a>コードの名前空間

> [!IMPORTANT]
>  このインターフェイスは、アクティブな開発中であり、変更されます。
>

## <a name="summary"></a>まとめ
コードの名前空間には、コードと逆アセンブリの属性が含まれています。 これにより、指定されたアドレスまたは関数を逆アセンブルできる逆アセンブラーオブジェクトを作成し、そのアセンブリに関する詳細情報と、使用可能な場合は変数またはソース情報を提供できます。

## <a name="sample"></a>サンプル
この名前空間とオブジェクトの使用方法のエンドツーエンドの例については、GitHub のサンプルを確認してください。https://github.com/Microsoft/WinDbg-Samples/tree/master/CodeFlow 

## <a name="object-methods"></a>オブジェクト メソッド
|名前|戻り値の型|署名|説明|
|--- |--- |--- |--- |
|CreateDisassembler アセンブラー| [アセンブリ](dbgmodel-object-disassembler.md)|CreateDisassembler アセンブラー ([アーキテクチャ])|指定されたアーキテクチャの逆アセンブラーオブジェクトを作成します。 アーキテクチャは、"ARM"、"ARM64"、"X64"、または "X86" のいずれかです。 アーキテクチャが指定されていない場合、X64 が想定されます。 |
|TraceDataFlow フロー|[命令](dbgmodel-object-instruction.md)の[コレクション](dbgmodel-namespace-collections.md)|TraceDataFlow フロー ([アドレス])|指定した*アドレス*(または、アドレスが指定されていない場合は現在の命令ポインター) の命令、およびそのすべてのソースオペランドを参照します。 このメソッドは、トレースされた命令のソースオペランドに影響を受ける命令を検索する関数の制御フローを後方にウォークします。 **このメソッドでは、[ここ](https://github.com/Microsoft/WinDbg-Samples/tree/master/CodeFlow)に記載されている CodeFlow 拡張機能を読み込む必要があります。**|

## <a name="remarks"></a>Remarks
CreateDisassembler アセンブラーの既定値は "X64" です。この動作は、現在のスレッドの命令ポインターでモジュールのアーキテクチャをプルするように変更されます。