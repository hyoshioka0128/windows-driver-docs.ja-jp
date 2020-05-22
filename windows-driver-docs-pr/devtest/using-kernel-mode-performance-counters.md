---
title: カーネル モードのパフォーマンス カウンターの使用
description: カーネル モードのパフォーマンス カウンターの使用
ms.assetid: b740dd92-ad75-4dea-98d4-dce04b273d2f
ms.date: 10/31/2019
ms.localizationpriority: medium
ms.openlocfilehash: 0b1e7822aec5118570f22608714e916620b7c410
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769617"
---
# <a name="using-kernel-mode-performance-counters"></a>カーネル モードのパフォーマンス カウンターの使用

カーネルモード PCW は、既存のパフォーマンスカウンターバージョン2プラットフォームの拡張機能であり、カーネルモードコンポーネントがパフォーマンスカウンターを簡単に公開できるようにします。 この新しい拡張機能を組み込むには、バージョン2のカウンターを記述するマニフェストに最小限の追加を加える必要があります。また、カーネルモードのパフォーマンスカウンターインターフェイスを使用する必要があります。

新しいカウンターを開発するには、次の手順に従います。

1. プロバイダーとそのカウンターセットを記述する[情報マニフェストを記述](https://docs.microsoft.com/windows/win32/wes/writing-an-instrumentation-manifest)します。

    マニフェスト内の要素と属性の詳細については、「[パフォーマンスカウンターのスキーマ](https://docs.microsoft.com/windows/win32/perfctrs/performance-counters-schema)」を参照してください。 カウンターマニフェストは、パフォーマンスカウンタープロバイダーとそのカウンターセットを定義する XML 形式のファイルです。

    マニフェストは、手動で作成することも、WDK に含まれているマニフェストジェネレーターツール**Ecmangen**を使用して作成することもできます。 この[開発者コマンドプロンプト](https://docs.microsoft.com/dotnet/framework/tools/developer-command-prompt-for-vs)は、「 **ecmangen**」と入力すると表示されます。

2.  [Ctrpp ツール](https://docs.microsoft.com/windows/win32/perfctrs/ctrpp)を使用して、マニフェストから登録コードと文字列リソースを生成します。

    カウンタプリプロセッサ (CTRPP) ツールは WDK に含まれており、「 **ctrpp**」と入力することによって[開発者コマンドプロンプト](https://docs.microsoft.com/dotnet/framework/tools/developer-command-prompt-for-vs)で使用できます。

3. カウンターセットの登録と登録解除を行うコードを追加します。

    詳細については、 [**Pcwregister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pcwregister)および[**Pcwregister 解除**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pcwunregister)関数に関する説明を参照してください。

4. インスタンスを公開するコードを追加します。

5. 新しいコードと文字列リソースを含むバイナリを作成します。

カーネルモード PCW プロバイダーの例については、GitHub の[Windows ドライバーサンプル](https://github.com/Microsoft/Windows-driver-samples)リポジトリにある[カーネルカウンターのサンプル (Kcs)](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/perfcounters/kcs)を参照してください。

 

 





