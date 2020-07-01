---
title: NDIS のデバッグの概要
description: NDIS のデバッグの概要
ms.assetid: d15e8a0c-e553-4e0d-84ed-5fdc2026a2d3
keywords:
- NDIS のデバッグ, 概要
ms.date: 05/14/2020
ms.localizationpriority: medium
ms.openlocfilehash: 1f93d9b5fb63a2eb086aa2983baff386c176fcea
ms.sourcegitcommit: 8596782b07c8a71adf38fc2c2da68b75ba0a1259
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85593971"
---
# <a name="overview-of-ndis-debugging"></a>NDIS のデバッグの概要

ネットワークドライバーをデバッグするための2つの主要なツールは、デバッグトレースと Network Driver Interface Specification (NDIS) 拡張機能です。 デバッグトレースの詳細については、「 [NDIS デバッグトレースの有効化](enabling-ndis-debug-tracing.md)」を参照してください。 NDIS デバッグ拡張機能の詳細については、「 [Ndis extensions](ndis-extensions--ndiskd-dll-.md)」を参照してください。これにより、拡張モジュール Ndiskd.dll にある拡張機能コマンドの完全な一覧が提供されます。

現在のアダプターとプロトコルを示すビジュアルレポートを生成するには、 [ndiskd netreport](-ndiskd-netreport.md)コマンドを使用します。

![複数のアダプターを示す2つの列を示す ndiskd netreport の色分けされた出力](images/ndis-report.png)

次に、 [ndiskd](-ndiskd-netadapter.md)カーネルデバッガーコマンドを実行して、現在のドライバーのセットの調査を開始することをお勧めします。

```dbgconsole
1: kd> !ndiskd.netadapter
    Driver             NetAdapter          Name
    ffffdf8015a98380   ffffdf8015aa11a0    Microsoft ISATAP Adapter #2
    ffffdf801418d650   ffffdf80140c71a0    Microsoft Kernel Debug Network Adapter
```

ネットワークドライバーをデバッグするための追加ツールとして、通常のデバッグ拡張機能があります。これは、デバッグ情報の取得に役立ちます。 たとえば、「 [! stack 2 ndis!](-stacks.md) 」と入力します。 **ndis!** で始まるスタック内のすべてのスレッドを表示します。 この情報は、デバッグがハングしたり停止したりする場合に役立ちます。 WinDbg の概要については、「 [Windows デバッグの](getting-started-with-windows-debugging.md)概要」を参照してください。

## <a name="driver-verifier"></a>ドライバーの検証ツール

NDIS ドライバーをテストするためのもう1つの便利なツールは、NDIS 検証ツールです。 詳細については、「 [NDIS ドライバー](https://docs.microsoft.com/windows-hardware/drivers/devtest/sdv-rules-for-ndis-drivers)と[静的ドライバーの検証](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)規則」を参照してください。

## <a name="ndis-debugging-resources"></a>NDIS デバッグリソース

デフラグツールのエピソード175では、NDIS のデバッグ-[デフラグツール #175、ネットワークスタックのデバッグ](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)について説明しています。

Ndis チームのブログアーカイブは、 [ndis ブログ](https://docs.microsoft.com/archive/blogs/ndis/)から入手できます。

## <a name="ndis-bug-checks"></a>NDIS のバグチェック

また、NDIS 固有のバグチェックコード、バグチェック 0x7C (バグコード \_ NDIS \_ ドライバー) もあります。 パラメーターの完全な一覧については、「[バグチェック 0x7C](bug-check-0x7c--bugcode-ndis-driver.md)」を参照してください。

一般的な NDIS misbehavior 関連のバグチェックは[バグチェック 0xD1: DRIVER_IRQL_NOT_LESS_OR_EQUAL](bug-check-0xd1--driver-irql-not-less-or-equal.md) 、ドライバーコード自体が原因である可能性があります。 ほとんどの場合、バグまたはメモリの破損が原因で、最終的に不適切なポインターとしてマニフェストが発生します。

もう1つの一般的な問題は、[バグチェック 0x9f: DRIVER_POWER_STATE_FAILURE](bug-check-0x9f--driver-power-state-failure.md)です。

すべてのバグチェックを行う最初の手順は、適切なダンプファイルを探し、それを Windows デバッガーに読み込んで、 [! analyze](-analyze.md)コマンドを使用することです。 詳細については、「 [! Analyze 拡張機能の使用](using-the--analyze-extension.md)」を参照してください。

