---
title: Windows 8 用 Windows 用デバッグツール
description: Windows 8 用 Windows 用デバッグツール
ms.assetid: 1AC2595A-800F-4F40-9C9D-61DE5398CBEB
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a15efcf8076792b276b6aa31be2afa9ccc1c963
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534455"
---
# <a name="debugging-tools-for-windows-new-for-windows-8"></a>Debugging Tools for Windows:Windows 8 の新機能

Windows 8 以降では、カーネルモードとユーザーモードの両方のコンポーネントを Microsoft Visual Studio から開発、ビルド、およびデバッグすることができます。 ネットワーク接続または USB 3.0 接続を介したデバッグのサポートが追加され、最適化されたコードとインライン関数のデバッグがサポートされるようになりました。 詳細については、以下のトピックを参照してください。

-   [Visual Studio を使用したデバッグ](debugging-using-visual-studio.md)
-   [ネットワーク接続を手動で設定する](setting-up-a-network-debugging-connection.md)
-   [USB 3.0 接続を手動で設定する](setting-up-a-usb-3-0-debug-cable-connection.md)
-   [最適化されたコードとインライン関数のデバッグ](debugging-optimized-code-and-inline-functions-external.md)

2つの新しいデバッガー拡張機能コマンドセットが含まれています。

-   [USB 3.0 拡張機能](usb-3-extensions.md)
-   [RCDRKD 拡張機能](rcdrkd-extensions.md)

Visual Studio に加えて、windows デバッガーを sse して Windows アプリをデバッグすることもできます。 Windows パッケージ用デバッグツールには、Windows アプリの中断、再開、デバッグ、終了を手動で制御できるようにする[**Plmdebug**](plmdebug.md)が含まれています。

Sos はマネージコードのデバッグに使用されるコンポーネントです。 Windows 8 用デバッグツールのパッケージには、sos は含まれていません。 Sos を取得する方法の詳細については、「[マネージコードのデバッグ](debugging-managed-code.md)」の「 *sos デバッガー拡張 (Sos) の取得*」を参照してください。

## <a name="related-topics"></a>関連トピック

[Windows のデバッグ](index.md)
