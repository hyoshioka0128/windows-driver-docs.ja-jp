---
title: カーネル モードのパフォーマンス カウンターの使用
description: カーネル モードのパフォーマンス カウンターの使用
ms.assetid: b740dd92-ad75-4dea-98d4-dce04b273d2f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87822a0c19665898549cab5f3ed6b984aa19377c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574109"
---
# <a name="using-kernel-mode-performance-counters"></a>カーネル モードのパフォーマンス カウンターの使用


カーネル モード PCW では、既存のパフォーマンス カウンター バージョン 2 のプラットフォームを使用するパフォーマンス カウンターを簡単に公開するカーネル モード コンポーネントを拡張機能です。 この新しい拡張機能を組み込むには、バージョン 2 のカウンターを記述するマニフェストに最小限の項目を追加する必要があると、カーネル モードのパフォーマンス カウンターのインターフェイスを使用する必要があります。

新しいカウンターを開発するのにには、次の手順を使用します。

1.  プロバイダーとそのカウンターを記述するマニフェストを設定します。

    要素と、マニフェスト内の属性の詳細については、[パフォーマンス カウンター スキーマ](https://go.microsoft.com/fwlink/p/?linkid=147029)を参照してください。 カウンター マニフェストは、パフォーマンス カウンター プロバイダーとそのカウンターを定義する XML フォーマット ファイルを設定します。

    マニフェストを手動で作成または Ecmangen.exe、マニフェスト ジェネレータ ツールを使用して作成できます。 ツールは WDK に含まれているし、ビルド環境ウィンドウにある (型**ecmangen**コマンド プロンプトで)。

2.  使用して、 [CTRPP ツール](https://go.microsoft.com/fwlink/p/?linkid=144441)マニフェストからの登録のコードと文字列リソースを生成します。

    カウンター プリプロセッサ (CTRPP) ツールは WDK に含まれているし、ビルド環境ウィンドウにある (型**ctrpp**コマンド プロンプトで)。

3.  登録およびカウンター セットを登録解除するためのコードを追加します。

    詳細については、次を参照してください。、 [ **PcwRegister** ](https://msdn.microsoft.com/library/windows/hardware/ff550323)と[ **PcwUnregister** ](https://msdn.microsoft.com/library/windows/hardware/ff550326)関数。

4.  インスタンスを公開するコードを追加します。

5.  新しいコードと文字列リソースを含むバイナリをビルドします。

カーネル モード PCW プロバイダーの例は、次を参照してください。、[カーネル カウンター サンプル (Kcs)](https://go.microsoft.com/fwlink/p/?LinkId=617718)で、 [Windows ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub リポジトリにあります。

 

 





