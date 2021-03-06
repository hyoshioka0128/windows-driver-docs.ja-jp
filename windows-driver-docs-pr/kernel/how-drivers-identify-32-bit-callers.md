---
title: ドライバーで 32 ビットの呼び出し元を識別する方法
description: ドライバーで 32 ビットの呼び出し元を識別する方法
ms.assetid: 9bfe9024-60f1-41ad-a034-160caaaa7801
keywords:
- 32 ビットの I/O をサポートして WDK 64 ビット、32 ビットの呼び出し元を識別します。
- 32 ビットの呼び出し元を識別します。
- WDK の 64 ビットの 32 ビットの呼び出し元 id
- WDK の 64 ビットのコードをファイル システムの制御
- FSCTL WDK 64 ビット
- 制御コード WDK 64 ビット
- I/O 制御コード WDK カーネル、64 ビット ドライバーで 32 ビットの I/O
- Ioctl WDK カーネルでは、64 ビット ドライバーで 32 ビットの I/O
- 呼び出し元の id WDK 64 ビット
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c53fbb940efc707b09c9734f4e700892120a2b2a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371868"
---
# <a name="how-drivers-identify-32-bit-callers"></a>ドライバーで 32 ビットの呼び出し元を識別する方法





IOCTL または FSCTL 要求の発信元が 32 ビットまたは 64 ビット アプリケーションであるかどうかを確認するドライバーを 2 つの方法はあります。 まずは、自身を識別するアプリケーションです。 2 つ目は、独自に判断するドライバーによってはアプリケーションは、32 ビットまたは 64 ビットかどうかです。

最初の手法では、IOCTL に FSCTL をコントロールのコードで「64 ビット」フィールドを定義する必要があります。 このフィールドには、64 ビットの呼び出し元にのみ設定される単一のビットが含まれています。 したがって 64 ビットの呼び出し元によって識別このビットが設定されている 64 ビットの制御コードの別のセットを使用します。 32 ビットの呼び出し元をこのビットが設定されていない制御コードのようなセットを使用します。

2 番目の手法では、引き続き IOCTL または FSCTL と同じコードを使用する 32 ビットおよび 64 ビット アプリケーションを許可します。 ドライバーがユーザー モード プロセスは、32 ビットまたは 64 ビットを呼び出すことによって、かどうかを決定する代わりに、 [ **IoIs32bitProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iois32bitprocess)します。

最初の手法は、ドライバーはカーネル モードのルーチンを呼び出す代わりに、ビット フラグをチェックするためより効率的です。 ただし、2 番目の手法には、ユーザー モード コードに変更は必要ありません。 どの技法を使用するには、ドライバーと I/O 要求を送信するアプリケーションの要件によって異なります。

 

 




