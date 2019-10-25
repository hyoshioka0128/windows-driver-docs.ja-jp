---
title: カーネル モードのパフォーマンス カウンターの使用
description: カーネル モードのパフォーマンス カウンターの使用
ms.assetid: b740dd92-ad75-4dea-98d4-dce04b273d2f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae840dc8c6d5703f4a2a5fe0d36c493499e95a3e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839993"
---
# <a name="using-kernel-mode-performance-counters"></a>カーネル モードのパフォーマンス カウンターの使用


カーネルモード PCW は、既存のパフォーマンスカウンターバージョン2プラットフォームの拡張機能であり、カーネルモードコンポーネントがパフォーマンスカウンターを簡単に公開できるようにします。 この新しい拡張機能を組み込むには、バージョン2のカウンターを記述するマニフェストに最小限の追加を加える必要があります。また、カーネルモードのパフォーマンスカウンターインターフェイスを使用する必要があります。

新しいカウンターを開発するには、次の手順に従います。

1.  プロバイダーとそのカウンターセットを記述するマニフェストを記述します。

    マニフェスト内の要素と属性の詳細については、「[パフォーマンスカウンターのスキーマ](https://go.microsoft.com/fwlink/p/?linkid=147029)」を参照してください。 カウンターマニフェストは、パフォーマンスカウンタープロバイダーとそのカウンターセットを定義する XML 形式のファイルです。

    マニフェストは、手動で作成することも、マニフェストジェネレーターツールである Ecmangen を使用して作成することもできます。 このツールは WDK に含まれており、ビルド環境ウィンドウで使用できます (コマンドプロンプトで「 **ecmangen** 」と入力します)。

2.  [Ctrpp ツール](https://go.microsoft.com/fwlink/p/?linkid=144441)を使用して、マニフェストから登録コードと文字列リソースを生成します。

    カウンタプリプロセッサ (CTRPP) ツールは、WDK に含まれており、ビルド環境ウィンドウで使用できます (コマンドプロンプトで「 **ctrpp** 」と入力します)。

3.  カウンターセットの登録と登録解除を行うコードを追加します。

    詳細については、 [**Pcwregister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pcwregister)および[**Pcwregister 解除**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pcwunregister)関数に関する説明を参照してください。

4.  インスタンスを公開するコードを追加します。

5.  新しいコードと文字列リソースを含むバイナリを作成します。

カーネルモード PCW プロバイダーの例については、GitHub の[Windows ドライバーサンプル](https://go.microsoft.com/fwlink/p/?LinkId=616507)リポジトリにある[カーネルカウンターのサンプル (Kcs)](https://go.microsoft.com/fwlink/p/?LinkId=617718)を参照してください。

 

 





