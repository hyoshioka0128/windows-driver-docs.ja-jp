---
title: 64 ビット Windows は、ドライバーの移植
description: 64 ビット Windows は、ドライバーの移植
ms.assetid: f06e6aae-fc44-481c-a277-1c266d6e6d7b
keywords:
- 64 ビットの WDK カーネル、ドライバーの移植
- 64 ビット Windows に移植ドライバー
- サンクの WDK
- WOW64 サンク レイヤー WDK
- 固定精度の型パラメーターに変換します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cda3cbfe6771a49e8ae899a54cd85918920bd963
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536362"
---
# <a name="porting-your-driver-to-64-bit-windows"></a>64 ビット Windows は、ドライバーの移植





Windows の 64 ビット バージョンは 32 ビットおよび 64 ビット Windows アプリケーションの 1 つのソース コード ベースを使用する開発者が可能に設計されています。 多くの場合、これは 32 ビットおよび 64 ビットの Windows ドライバーの場合は true。 も。

64 ビットの Windows にはユーザー モード アプリケーションでは、Windows (WOW64) 上の Windows が含まれています*サンク レイヤー* 64 ビット バージョンの Windows を (パフォーマンスが低下) で実行するための 32 ビット アプリケーションを有効にします。 これは、32 ビットの関数呼び出しをインターセプトしてポインターの精度パラメーターの型を変換する 64 ビットのカーネルへの移行を行う前に適切な固定精度の型。 この変換プロセスが呼び出されます*サンキング*します。

**注**  32 ビットに対してのみ行われますがこのサンク*アプリケーション*。 32 ビット*ドライバー*は、Windows の 64 ビット バージョンではサポートされていません。

 

 

 




