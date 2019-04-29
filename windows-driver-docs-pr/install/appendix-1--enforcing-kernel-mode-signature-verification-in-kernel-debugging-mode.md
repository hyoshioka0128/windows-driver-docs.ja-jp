---
title: カーネル デバッグでカーネル モードの署名の検証を適用します。
description: カーネル デバッガーがアタッチされている場合は、読み込み時の署名の強制を有効にする方法について説明します。
ms.assetid: D7CB436F-4B89-49E7-BB53-101BDA7046F3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 482bf6685c401dba51b1c405448642271aec85f2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385557"
---
# <a name="appendix-1-enforcing-kernel-mode-signature-verification-in-kernel-debugging-mode"></a>付録 1:カーネル デバッグ モードでのカーネルモードの署名の検証の適用


## <a name="enforcing-kernel-mode-signature-verification-in-kernel-debugging-mode"></a>カーネル デバッグ モードでのカーネルモードの署名の検証の適用


*抜粋*[開発およびテスト中に、署名されていないドライバーをインストールする](installing-an-unsigned-driver-during-development-and-test.md):

場合によっては、開発者は、カーネル デバッガーがアタッチされている場合は、読み込み時の署名の強制を有効にする必要があります。 この例では、ドライバー スタックがある未署名のドライバ (フィルター ドライバーの場合) などの読み込みに失敗する可能性がありますスタック全体を無効になる場合です。 デバッガーをアタッチでは、未署名のドライバーを読み込む、ため、デバッガーがアタッチされていると、すぐに消える問題が表示されます。 この種の問題のデバッグは、困難な場合があります。

このような場合のデバッグを容易にするためには、カーネル モード コード署名ポリシーには、次のレジストリ値がサポートされています。

```cpp
HKLM\SYSTEM\CurrentControlSet\Control\CI\DebugFlags
```

このレジストリ値の型は[REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)、次のフラグの 1 つ以上のビットごとの OR に基づいて値を割り当てることができます。

```cpp
0x00000001
```

このフラグの値は、ドライバーが署名されていない場合に、デバッガーを中断するカーネルを構成します。 開発者またはテスターをデバッガー プロンプトで g を入力して、未署名のドライバーをロードを選択できます。

```cpp
0x00000010
```

このフラグの値は、カーネル デバッガーの存在を無視して、常に符号なしのドライバーの読み込みをブロックするを構成します。

このレジストリ値では、レジストリが存在しないか、前に説明したフラグに基づいていない値を持つ場合、カーネルは、カーネル モード ドライバーが署名されているかどうかに関係なくデバッグでのドライバーを常に読み込みます。

**注**  このレジストリ値は既定では、レジストリに存在しません。 カーネル モードの署名の検証をデバッグするには、値を作成する必要があります。

 

 

 





