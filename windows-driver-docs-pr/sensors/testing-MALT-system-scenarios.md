---
title: システムのシナリオのテスト
author: windows-driver-content
description: このテストでは、スリープなどのシステム電源イベントの後に、環境光センサー (ALS) が正常に動作していることを確実にフォーカスがあるか、休止状態します。
ms.assetid: f2778853-ddc8-4118-aa58-9df6dab53b7a
ms.date: 12/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: de2faa4012f6c103ce4a36b64c7b9c35f69d3995
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391553"
---
# <a name="testing-system-scenarios"></a>システムのシナリオのテスト

このテストでは、スリープなどのシステム電源イベントの後に、環境光センサー (ALS) が正常に動作していることを確実にフォーカスがあるか、休止状態します。

## <a name="set-up"></a>設定

目を通してください、[テスト要件](testing-MALT-building-a-light-testing-tool.md)セクションに、テストの要件を満たしていることを確認します。

## <a name="brightness-stress-test-procedures"></a>明るさのストレス テスト手順

1. SUT 実行`MALTUtil.exe /stress`します。
2. お待ちください。 このテストは、約 15 分かかります。 テストは、システムをスリープ状態を送信中に、光源の輝度を調整します。  テストは光とセンサーの値が範囲外の初期化中に生成かどうかの変更に対応するため、システムにかかる時間を検討します。
3. テストの完了後、結果が画面に表示されます。

参照してください[このホワイト ペーパー](https://docs.microsoft.com/windows-hardware/design/whitepapers/integrating-ambient-light-sensors-with-computers-running-windows-10-creators-update)光センサーとアンビエント ライト応答曲線の統合に関する完全なガイダンスについては Microsoft の。
