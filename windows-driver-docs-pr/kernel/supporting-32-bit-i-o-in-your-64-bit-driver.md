---
title: 64 ビット ドライバーでの 32 ビット I/O のサポート
description: 64 ビット ドライバーでの 32 ビット I/O のサポート
ms.assetid: c024c74e-0b83-4f86-8370-8269cbf69c9a
keywords:
- 32 ビットの I/O サポート WDK 64 ビット
- 64 ビット WDK カーネルでは、32 ビットの I/O のサポート
- サンクの WDK
- WOW64 サンク レイヤー WDK
- 固定精度の型パラメーターに変換します。
- 32 ビットでの I/O サポート WDK 64 ビット、32 ビットの I/O のサポートについて 64 ビット
- 制御コード WDK 64 ビット
- I/O 制御コード WDK カーネル、64 ビット ドライバーで 32 ビットの I/O
- Ioctl WDK カーネルでは、64 ビット ドライバーで 32 ビットの I/O
- WDK の 64 ビットのコードをファイル システムの制御
- FSCTL WDK 64 ビット
- バッファー ポインター WDK 64 ビット
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1efc744de854ec7b6e64948f65a62c6adc4573d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382969"
---
# <a name="supporting-32-bit-io-in-your-64-bit-driver"></a>64 ビット ドライバーでの 32 ビット I/O のサポート





Windows (WOW64) 上の Windows では、64 ビット Windows で実行するユーザー モード アプリケーションを Microsoft Win32 を使用できます。 これは、Win32 関数呼び出しをインターセプトして、64 ビットのカーネルへの移行を行う前にポインターの有効桁数型からパラメーターを適切な固定精度の型に変換します。 この変換と呼ばれる*サンキング*、1 つの重要な例外を持つ、すべての Win32 関数に自動的に行われます: に渡されるデータ バッファー [ **DeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol). によってポイントされているこれらのバッファーの内容、 *InputBuffer*と*OutputBuffer*の構造がドライバーに固有であるため、パラメーターは thunked いませんが。

**注**  ですが、バッファー*内容*thunked されませんが、バッファー*ポインター* 64 ビット ポインターに変換されます。

 

ユーザー モード アプリケーション呼び出し[ **DeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)指定されたカーネル モード ドライバーに直接 I/O 要求を送信します。 この要求には、I/O 制御コード (IOCTL) またはファイル システムの制御コード (FSCTL) および入力へのポインターが含まれていて、データ バッファーを出力します。 これらのデータ バッファーの形式は、IOCTL または FSCTL、カーネル モード ドライバーで定義されている順番に固有です。 バッファー形式は任意であり、ドライバーと WOW64 ではないことがわかっているので、データをサンクのタスクは、ドライバーにままです。

64 ビット ドライバーは、次のすべてに該当する場合、32 ビット I/O をサポートする必要があります。

-   ドライバーは、IOCTL (または FSCTL) をユーザー モード アプリケーションを公開します。

-   少なくとも 1 つの IOCTL で使用される I/O バッファーには、ポインターの精度のデータ型が含まれています。

-   IOCTL コードは、ポインターの精度のバッファーのデータ型を使用しないように簡単に書き直すことはできません。

 

 




